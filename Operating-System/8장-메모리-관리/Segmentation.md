### Segmentation

+ 프로그램을 논리적인 의미 단위의 여러 segment로 구성하는 방식의 메모리 관리 기법
  + 작게는 프로그램을 구성하는 함수 하나하나를 세그먼트로 정의한다.
  + 크게는 프로그램 전체를 하나의 세그먼트로 정의할 수도 있다.
  + 일반적으로 code, data, stack이 각각 하나의 세그먼트로 정의된다.
+ 다음과 같은 logical unit들을 segment라고 할 수 있다.
  + main(), function, global variables, stack, symbol table...

### Segmentation Architecture

- Logical address의 구성
  - <segment-number, offset>
- Segment table
  - 각각의 테이블 엔트리는 다음의 요소를 가진다.
  - base - 물리적 주소의 시작 위치
  - limit - 세그먼트의 길이, 세그먼트의 길이가 동일하지 않기 때문에 기록
- Segment-table base register(STBR)
  - 물리적 메모리에서의 segment table의 위치를 저장
- Segment-table length register(STLR)
  - 프로그램이 사용하는 segment의 수를 저장
  - segment number < STLR 여야 유효한 요청을 보낼 수 있음
- Protection
  - 각 세그먼트 별로 protection bit가 존재한다.
  - 각각의 엔트리에서
    - Valid bit = 0이면 illegal segment
    - Read/Write/Read-only등 권한 부여
  - 의미 단위로 protection을 부여할 수 있기 때문에 paging기법에 비해 장점이 있음
- Sharing
  - Shared segment - Same segment number
  - sharing역시 의미 단위로 진행하기 때문에 paging기법보다 효과적이다.
- Allocation
  - first fit / best fit을 사용해야 한다.
  - 이로 인해 external fragmentation발생(가변분할 방식과 마찬가지로 segment의 길이가 동일하지 않기 때문에)

### Segmentation Hardware

- ![Segmentation in OS: Hardware Architecture, Need, Advantages, Disadvantages  with example | Engineer's Portal](https://d3e8mc9t3dqxs7.cloudfront.net/wp-content/uploads/sites/11/2020/04/Hardware-Architecture-of-Segmentation.png)
- segment number s가 STLR보다 작은 경우 Trap발생
- 오프셋 d가 limit보다 큰 경우(프로그램 범위를 넘어가는 경우) 잘못된 접근이므로 Trap발생
- 정상적인 요청의 경우 base + offset(d)으로 주소 변환 시행

### Example of Segmentation

- ![What is Segmentation in OS? Introduction, Implementation, Example - Binary  Terms](https://binaryterms.com/wp-content/uploads/2021/01/Segmentation-table-example.jpg)
- Segmentation은 외부 단편화가 쉽게 일어날 수 있지만 일반적으로 paging에 비해 요소(segment)의 수가 매우 적다.
- 즉, 테이블을 위한 메모리 사용자체는 페이지 당 4KB(나누기에 따라 다름)를 할당하는 paging기법보다는 작다.

### Sharing of Segments

- ![59.305 Course Notes](https://www.massey.ac.nz/~mjjohnso/notes/59305/mod8d12.gif)
- shared segment인 경우(segment 0) 시작 위치와 limit가 동일함을 볼 수 있다.

### Segmentation with Paging

+ Segment하나가 여러 개의 page로 구성되는 방식
+ Segment-table의 엔트리가 segment의 base address를 가지는 것이 아니라 segment를 구성하는 page table의 base address를 가지고 있다.
+ ![Segmentation and Paging | Segmented Paging | Gate Vidyalay](https://www.gatevidyalay.com/wp-content/uploads/2018/11/Segmented-Paging-Translating-Logical-Address-into-Physical-Address-Diagram.png)
+ ![Segmentation and Paging (Topic 6) Segmentation (1) Segmentation (2)  Segmentation (3)](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTc0FEJwzXfjD0pCYgNCgh6oNww0DzncDzDTA&usqp=CAU)
+ Segment table의 엔트리 구성 > segment length + page-table base
+ 세그먼트 번호로 segment table을 조회하여 해당하는 page-table base 탐색
+ page-table base와 offser(d)를 통해 주 메모리에 해당하는 frame탐색
+ 최종적으로 메모리에 데이터가 프레임 단위로 할당되기 때문에 Segmentation의 Allocation시 발생하는 외부 단편화 문제가 일어나지 않음

