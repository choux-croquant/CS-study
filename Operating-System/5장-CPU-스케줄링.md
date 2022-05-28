## CPU 스케줄링
### Scheduling Criteria(성능 척도)

- 시스템 입장의 성능 척도

  - CPU Utilization(이용률) : CPU가 **작업을 처리하는 시간의 비율**, 많이 사용될수록 효율이 좋다.
  - Throughput(처리량) : 주어진 시간 동안 **몇 개의 작업을 처리**하는지에 대한 지표

- 프로세스 입장의 성능 척도

  - Turnaround time(소요 시간, 반환 시간) : 프로세스가 **CPU사용을 요청하고 사용한 뒤 다시 반환할 때 까지**의 시간, Waiting time + CPU burst time

  - Waiting time(대기 시간) : **Ready Queue에서 프로세스가 대기하는 시간의 총합**(burst가 여러번일 경우 모두 더한다.)

  - Response time(응답 시간) : 자원 요청 후 CPU를 **처음 얻기까지 걸리**는 시간(1회)

    

### 알고리즘의 종류

- FCFS(First-come, First-served) 

  - 선입선출, 먼저 온 프로세스가 다 CPU를 사용할 때까지 대기
  - **(Convoy Effect)** CPU를 오래 사용하는 작업이 먼저 올 경우 짧은 작업들이 그만큼 **(평균)대기 시간**이 늘어나게 되므로 효율적이지 못하다. > 즉 어떤 프로세스가 먼저 오느냐에 따라 영향을 매우 크게 받는다.

- SJF(Shortest Job First)

  - CPU burst time이 짧은 프로세스부터 먼저 처리하는 방식, **평균 대기 시간이 가장 짧음(SRTF)**을 보장한다. 두가지 스키마가 존재한다.
  - **Nonpreemptive** - 더 짧은 프로세스가 중간에 들어와도 먼저 작업 중인 프로세스의 작업을 보장하는 방식
  - **Preemptive** - CPU를 얻은 상태여도 더 짧은 작업이 들어오면 CPU를 넘겨주는 방식(SRTF - Shortest Remaining Time First)
  - Starvation 문제 - 사용시간이 짧은 프로세스들을 먼저 처리하면(심지어 남은 시간이 짧은 것 부터 앞으로 옮긴다면)긴 프로세스는? > **시간이 긴 특정 작업이 처리되지 않을 수 있다.**
  - 다음 번 CPU burst time을 알 수 없고, **과거의 사용량으로 추정**만 할 수 있다는 문제점.(exponential averaging...)

- Priority Scheduling

  - 우선 순위가 높은 프로세스부터 처리하는 방식, 일반적으로 우선순위를 정수값으로 표시한다. 역시 두 가지 스키마가 존재
  - **Nonpreemptive** - 우선순위가 더 높은 프로세스가 중간에 들어와도 먼저 작업 중인 프로세스의 작업을 보장하는 방식
  - **Preemptive** - CPU를 얻은 상태여도 우선 순위가 더 높은 작업이 들어오면 CPU를 넘겨주는 방식
  - SJF역시 우선순위 스케줄링의 한 종류이므로, 유사하게 Starvation문제가 존재한다.
  - Starvation문제를 보완하기 위해 **시간이 흐름에 따라 우선 순위를 높여주는 Aging**을 사용할 수 있다.

- RR(Round Robin)

  - 각 프로세스가 **동일한 크기의 할당 시간**을 받고, 할당 시간이 종료되면 **CPU자원을 선점당한 후 Ready Queue의 가장 뒤**로 이동하는 방식, 할당 시간의 존재로 인해 각 프로세스에 대한 **응답 시간이 빨라지는 장점**이 있다.

  - 기다리는 시간이 프로세스의 CPU Burst time에 비례하게 되는 구조를 가지고 있다.(작업 시간이 길면 여러 번 할당 시간을 돌게 되므로)

  - 할당 시간이 매우 길다면 FCFS알고리즘과 유사해진다.

  - 할당 시간이 **매우 짧다면** Context Switch가 빈번하게 발생하므로 **오버헤드가 커진다**.

  - **작업 시간이 비슷한 프로세스**들이 많다면? > 전반적으로 모든 작업들의 처리 시간이 오래 걸리게 되는 문제가 생긴다. (10초 걸리는 작업이 3개 있다면 할당 시간이 1초일 때 3작업 모두 30초 근처에서 비슷하게 된료된다. 반면 FCFS라면 10초 / 20초 / 30초에 완료된다.) 하지만 **일반적으로는 작업 시간이 다른 작업들이 섞여**있기 때문에 **RR방식이 더 효율적인 경우가 대부분**이다.

    

### Multilevel Queue

+ Ready Queue를 여러 개로 분할하는 방식의 스케줄링 기법

![img](https://velog.velcdn.com/images%2Fgabie0208%2Fpost%2Fdc270a2f-6a8e-4f4b-ab90-f16fa411948f%2F%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202021-10-16%20%EC%98%A4%ED%9B%84%208.30.49.png)

+ 각 **queue별로 다른 알고리즘**을 적용하여 효율적으로 구성할 수 있다. ex)
  + foreground queue(interactive한 작업) - 응답 시간이 짧은 RR알고리즘 사용
  + background queue(interative하지 않은 batch형태의 job) - 오버헤드가 적은 FCFC알고리즘 사용
+ **각각의 queue에 대한 스케줄링**이 필요하다. ex)
  + Fixed Priority Scheduling
    + 우선 순위가 높은 queue에 먼저 작업들을 대기시키는 케이스
    + 우선 순위가 높은 queue가 계속 전부 채워지지 않는 상태라면 우선 순위가 낮은 queue가 영원히 쓰이지 않는 Starvation 문제가 발생할 수 있다.
  + Time Slice
    + 각 큐에 CPU time을 적절한 비율로 할당하여 Starvation을 방지하는 방법
    + ex) CPU time의 80%는 RR알고리즘을 사용하는 foreground queue에 주고, 20%는 FCFS방식의 background queue에 주기



### Multilevel Feedback Queue

+ Multilevel queue인데 **프로세스가 다른 큐로 이동**할 수 있는 방식, Aging을 Multilevel feedback queue로 구현할 수 있다.

+ Multilevel feedback queue schduler의 파라미터

  + Queue의 수
  + 각 queue의 스케줄링 알고리즘
  + Process를 상위 queue로 보내는 기준
  + Precess를 하위 queue로 보내는 기준
  + 프로세스가 CPU서비스를 받으려 할 때 들어갈 큐를 결정하는 기준

+ ex) 처음 들어온 프로세스는 할당 시간이 8인 RR방식의 queue로 보내고 > 할당 시간 내에 작업이 완료되지 않았다면, 할당 시간이 16인 RR방식의 queue로 보내고 > 그래도 완료되지 않았다면 FCFS방식의 queue로 보내는 예시

  ![Difference between Multilevel Queue (MLQ) and Multi Level Feedback Queue  (MLFQ) CPU scheduling algorithms - GeeksforGeeks](https://media.geeksforgeeks.org/wp-content/uploads/20200619201751/mfg.jpg)



### Multiple-Processor Scheduling

+ CPU가 여러 개인 경우의 스케줄링 방식
+ Homogeneous Processor
  + Queue에 작업을 한 줄로 세워 각 프로세서가 가져가도록 하는 방식
  + 반드시 특정 프로세서에서 수행되어야 하는 프로세스가 있는 경우 문제가 복잡해진다.
+ Load Sharing
  + 일부 프로세서에 작업이 몰리지 않도록 부하는 적절히 공유하는 메커니즘 필요
  + 별개의 큐를 두는 방법, 공동 큐를 사용하는 방법 - 선택적 이용
+ Symmetric Multiprocessing(SMP)
  + 각 프로세서가 알아서 스케줄링을 결정하는 방식
+ Asymmetric Multiprocessing
  + 하나의 프로세서가 시스템 데이터의 접근과 공유를 전담하고, 나머지 프로세서는 거기에 따르는 방식



### Real-Time Scheduling

+ Hard real-time systems
  + 반드시 정해진 시간 안에 task가 끝나도록 스케줄링 해야한다.
+ Soft real-time systems
  + 일반 프로세스에 비해 실시간 task에 높은 우선 순위를 주면 된다.



### Thread Scheduling

+ Local Scheduling
  + User level thread의 경우 사용자 수준의 스레드 라이브러리에 의해 어떤 스레드를 스케줄링 할 지 결정
+ Global Scheduling
  + Kernel level thread의 경우 일반 프로세스와 마찬가지로 커널의 단기 스케줄러가 어떤 스레드를 스케줄링 할 지 결정



### Algorithm Evaluation

+ 스케줄링 알고리즘에 대한 평가 방법
+ Queueing Models
  + 확률 분포로 주어지는 arrival rate, service rate등을 통해 각종 performance index값을 계산하는 방식
+ Implementation & Measurement (구현과 측정)
  + 실제 시스템에 알고리즘을 구현한 후 실제 작업에 대해 성능을 측정하여 비교하는 방법
+ Simulation
  + 알고리즘을 모의 프로그램으로 작성한 후 trace(실제 프로그램에서 추출한 input데이터)를 입력으로 하여 결과를 비교하는 방법