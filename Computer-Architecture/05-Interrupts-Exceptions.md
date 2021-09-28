# Interrupt

제어 흐름 상의 문제, 프로그램이 멈추는 경우를 말한다. internal 한 요인과 external 한 요인이 존재한다.

+ external : 하드웨어적인 문제로 발생하는 interrupt
  + 정전, 파워 고장 등으로 인한 Power fail interrupt
  + CPU 의 기능적 오류로 인한 Machine check interrupt
  + 키보드로 인터럽트 키를 누르거나(Ctrl+Alt+Delete), 외부 장치에서 인터럽트 요청을 하는 경우
  + 입출력 장치가 데이터 전송을 요구하는 경우나, 입출력 데이터에 이상이 있는 경우 I/O Interrupt



+ Internal : 소프트웨어적 문제로 발생하는 인터럽트, Trap 이라고 부른다.
  + Division by Zero, Overflow/Underflow, Exception 등의 Program check interrupt
  + System call : 프로세스 실행/종료 I/O 작업 등 사용자가 다루면 위험한 명령들을 사용하기 위해 OS가 제공하는 명령. folk(새 프로세스 생성), wait(자식 프로세스가 끝날 때까지 대기), exec(다른 프로그램 실행) 등이 존재한다. user mode 에서 system call 을 호출하면 trap 이 발생하며 kernal mode 로 진입, system call 을 수행한 뒤 return-from-trap 을 발생시켜 다시 user mode 로 돌아간다.



**Interrupt handler**

인터럽트 접수에 의해 발생되는 인터럽트에 대응하여 특정 기능을 처리하는 기계어 코드 루틴. 인터럽트 핸들러는 인터럽트 원인에 따라 각각 존재하며 각 핸들러가 작업을 마치는 데 걸리는 시간도 모두 다르다. 커널과 밀접한 관련을 가져서, 일반적으로 커널에만 존재하고 소프트웨어에는 넣지 않음.

