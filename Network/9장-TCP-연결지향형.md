### [TCP 프로토콜](https://youtu.be/cOK_f9_k_O0?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

- Transmission Control Protocol

- UDP와 마찬가지로 프로세스간 통신을 위한 프로토콜

- UDP와 달리 안정적이고, 순서가 보장된 통신을 보장한다.

- 안정성을 필요로 하지 않을 경우 UDP를 사용하는 것이 속도면에서 이점을 얻을 수 있지만 일반적으로 체감할 정도의 속도 차이가 발생하지는 않는다.

- UDP보다 헤더의 크기가 크기 때문에 네트워크 부하가 조금 더 커질 수 있다.

  ![TCP Header & IP Header](http://www.insecure.in/images/TCP-Header.png)

+ 옵션을 제외하고 20바이트로 이루어진 헤더를 가지고 있다.

+ Source Port & Destination Port : 송신지와 목적지의 포트 번호, 각각 2바이트의 필드

+ Sequence Number : 파편화된 데이터의 순서를 보장하기 위한 필드, 시퀀스 넘버를 통해 세그먼트를 올바른 순서로 재조립한다. 4바이트 필드

+ Acknowledgement Number : 데이터 수신자가 받을 다음 데이터의 시퀀스 번호, 핸드쉐이크 과정에서는 ack = 이전 seq + 1이고 데이터 전달시에는 ack = 이전 seq + data 길이값으로 정해진다. 즉 다음에 받을 데이터가 어디부터 시작하는지 표기하는 값이다.

+ Offset : 헤더가 아닌 데이터가 시작하는 위치를 표시하는 값, 옵션에 따라 헤더의 길이가 달라지기 때문에 존재한다.

+ Reserved : 추후 사용을 위해 예약된 필드 보통 0으로 채워진다. (3it)

+ TCP Flags : TCP프로토콜의 속성 내지는 역할을 표시하는 비트플래그 플래그가 늘어나면 Reserved필드의 비트를 추가로 사용한다. 자세한 내용은 아래의 항목으로 정리

+ Window Size : 한 번에 전송할 수 있는 데이터의 양을 의미하는 필드. 2바이트가 할당되므로 최대 값은 65535이고 64KB에 해당한다. 최근에는 더 많은 데이터를 전달할 수 있게 되어 option의 WSCALE필드를 사용하여 이 필드의 비트를 시프트하는 방식으로 최대 데이터 양을 높일 수 있다.

+ Checksum : 프로토콜 오류 검증을 위해 사용되는 필드

+ Urgent Pointer : 특정 데이터를 우선 처리하기 위해 사용되는 필드. URG플래그가 존재할 때(1일때) 이 필드에서 표시하는 데이터를 우선적으로 처리한다.

  

### TCP 플래그

- 각 비트의 값에 따라 플래그가 표시되며 여러 개가 중복될 수 있다. 목적에 따라 플래그의 종류 추가되기도 한다. 

- URG : Urgent pointer 필드에 값이 있음을 알리는 플래그

- ACK : Acknowledgement 필드에 값이 있음을 알리는 플래그, ACK비트의 값이 0이면 승인 번호 필드가 무시된다.

- PSH : Push, 현재 데이터를 빠르게 프로세스로 전달하라는 의미를 담은 플래그. PSH가 0이면 수신지에서 버퍼가 다 채워질 때까지 기다린다. PSH가 1이면 연결된 세그먼트가 없음을 의미한다고 볼 수 있다.

- RST : Reset, 연결이 수립되어 Established 상태인 상대방에게 연결을 강제로 리셋하도록 하는 요청

- SYN : Syncronize, 상대방과 연결 시 시퀀스 번호의 동기화를 진행하기 위한 세그먼트임을 알리는 플래그

- FIN : Finish, 상대방과 연결을 종료한다는 요청을 담은 플래그

- 다음의 3가지 플래그는 명시적 혼잡통보(Explicit Congestion Notification)을 위한 플래그이다. 처리 속도를 높이기 위한 목적으로 혼잡 상황을 명시한다.

- NS : CWR, ECE 비트가 실수 또는 고의로 은폐되는 경우를 방어하기 위해 추가된 비트

- ECE : ECN Echo, ECE플래그가 1이면서 SYN플래그가 1이면 ECN을 사용할 것임을 상대방에게 알린다. SYN플래그가 0이라면 네트워크 혼잡상황을 알리며 윈도우 사이즈를 줄여달라는 요청을 의미한다.

- CWR : 이미 ECE플래그를 전송 받아서 윈도우 사이즈를 줄였다는 것을 표시하기 위한 플래그.

  

### [TCP 3Way Handshake](https://youtu.be/Ah4-MWISel8?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

- 3 way-handshake connection - 양방향 통신

  1. 클라이언트가 SYN 패킷(연결 요청)을 전송

  2. 서버는 이를 확인하고 ACK(수신 확인 응답)를 포함하여 클라이언트로 SYN 패킷 전송

  3. 서버의 요청에 대해 클라이언트가 ACK를 전송 후 연결 설정 완료.

     

### [TCP를 이용한 데이터 전송 과정](https://youtu.be/0vBR666GZ5o?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

- 1. PSH + ACK 플래그로 구성된 요청을 클라이언트 측에서 송신

  2. 받은 요청의 Seq+data길이를 ACK, ACK를 Sep로 하여 PSH + ACK 플래그로 구성된 요청을 서버측에서 송신

  3. 위와 같은 방식으로  Seq, ACK를 구성하여 ACK플래그가 포함된 요청을 다시 클라이언트 측에서 송신 

     

### [TCP의 연결 상태 변화](https://youtu.be/yY0uQf0BTH8?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

![img](https://mblogthumb-phinf.pstatic.net/20160915_176/ryangjm_1473892285756Dj7E1_PNG/TCP%BB%F3%C5%C2%C3%B5%C0%CC%B5%B5.png?type=w2)

+ TCP의 상태 전이도, 데이터 통신 과정에서 발생하는 이벤트를 관리하는 방식이 정의된 스키마
+ **LISTEN 상태** : 클라이언트의 요청을 지속적으로 듣고있는 상태, 수동적 포트 개방
+ **ESTABLISHED 상태** : TCP연결이 수립된 상태. 3-way handshake가 끝난 후의 상태.

