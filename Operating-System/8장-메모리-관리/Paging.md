### Paging Example

- 주 메모리를 사용하기 위해 2차 기억 장치로부터 데이터를  저장하고 검색하는 메모리 관리 기법.
- 가장 **기억장치를 동일한 크기의 블록(page)**으로 나누어 운용한다. 주소 공간을 페이지 단위로 나누고 실제 Physical memory는 **page와 크기가 동일한 frame**으로 나누어 사용한다.
- Page table - 프로세스의 페이지 정보를 저장하는 테이블, 인덱스와 내용(물리 메모리의 시작 주소)로 구성된다.
- ![8-2. 페이징, 세그먼테이션](https://t1.daumcdn.net/cfile/tistory/27649A47590818AA2D)

### Address Translation Architecture

- page table을 통해 frame을 매칭시키고 logical address에 해당하는 값을 옮겨주는 것을 통해 변환이 가능하다.
- ![Address Translation Scheme](data:image/png;base64,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)

### Implementation of Page Table

- Page table은 주 메모리에 상주한다.
- Page table base register(PTBR)는 page table을 가리킨다. 
- Page table length register(PTLR)은 테이블 크기를 보관한다.
- 모든 메모리 접근 연산에는 2번의 메모리 접근이 필요하다.
  - page table접근에 1번, 실제 data/instruction접근에 1번 > 총 2번
- 속도 향상을 위해 associative register또는 translation look-aside buffer(TLB)라고 불리는 고속의 lookup hardware cache를 사용한다.
- TLB
  - **Parallel search가 가능**하다.(한 번에 여러 데이터를 탐색)
  - Address translation
    - page table중 일부가 TLB에 보관되어 있음, 해당 page가 TLB에 있는 경우 바로 대응하는 frame을 얻음
    - 그렇지 않은 경우 주 메모리에 있는 page table로 부터 frame을 얻는다.
    - TLB는 **context switch때 flush**(remove old entries)된다. > 특정 프로세스에 대한 정보이므로 리셋!
- **TLB를 사용하는 경우의 Schema**
- ![Translation lookaside buffer - Wikipedia](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6e/Translation_Lookaside_Buffer.png/373px-Translation_Lookaside_Buffer.png)
- Effective Access Time
  - Associative register lookup time = e(epsilon)
  - memory cycle time = 1
  - Hit ratio(TLB에서 페이지가 탐색되는 비율) = a(alpha) 이라고 하면
  - Effective Access Time(EAT) = hit + miss = (1 + e)a + (2 + e)(1-a) = 2 + e - a
  - 일반적으로 **a가 매우 높고, e가 매우 작기** 때문에 1에 가까운 값이 된다. 
  - 즉, memory table만 있는 경우의 시간인 2에 비해 **매우 적은 탐색 시간이 소요**된다.

### Two-Level Page Table

- Outer page table를 추가하여 Logical address를 여러 테이블로 나눈 구조. 탐색 시간은 더 걸리지만 메모리 공간적 이유를 위해 사용한다.
- ![2 level paging - GATE Overflow for GATE CSE](https://gateoverflow.in/?qa=blob&qa_blobid=14723176181853010891)
- 현대의 컴퓨터는 address space가 매우 큰 프로그램을 지원한다.
  - 32bit address사용 시 2^32B(약 4GB)의 주소 공간이 존재
  - page size가 4KB일 때 1M개의 page table entry가 필요하다.
  - 각 page entry가 4B일 때 프로세스 당 4M의 page table이 필요하다.
  - 대부분의 프로그램은 4GB의 주소 공간 중 **극히 일부만 사용**하므로 page table이 **4MB씩 존재하는 것은 공간이 크게 낭비**되는 것
  - 이러한 문제를 해결하기 위해서 
    - **Page table 자체를 page로 구성**
    - **사용되지 않는** 주소 공간에 대한 **outer page table의 엔트리 값은 NULL**로 설정(대응하는 inner page table이 없다는 의미) > 이 방법으로 인해 공간적 이득을 취할 수 있음
- Address-Translation Scheme
- ![Paging](https://t1.daumcdn.net/cfile/tistory/252B6B345757CEF011)
- Two-Level Paging Example
  - Logical address의 구성(32bit-machine, 4KB page size 기준)
    - 20bit의 page number
      - page table 자체가 page로 구성되기 때문에 다음과 같이 분리
      - 10bit의 page number
      - 10bit의 page offset(1K(2^10)개의 엔트리 위치를 구분하기 위한 오프셋)
    - 12bit의 page offset(4K(2^12)개의 바이트를 구분하기 위한 오프셋)

### Multilevel Paging and Performance

- 

### Valid (v)/ Invalid (i) Bit in a Page Table

- 

### Memory Protection

- 

### Inverted Page Table

- Inverted Page Table Architecture

### Shared Page

- Shared Pages Example