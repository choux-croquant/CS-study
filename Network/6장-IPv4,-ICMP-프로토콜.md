### [IPv4 프로토콜](https://youtu.be/_i8O_o2ozlE?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

+ 네트워트 간 데이터를 교환하기 위한 프로토콜
+ 데이터가 **정확하게 전달**되는 것을 보장하지는 않음, 중복된 패킷을 전달하거나 패킷의 순서를 틀릴 가능성이 존재한다.
+ 데이터의 정확성, 순서의 보장은 상위 프로토콜인 TCP에서 담당한다.

![IPv4 Packet Format - S600-E V200R011C10 Configuration Guide - IP Service -  Huawei](https://download.huawei.com/mdl/image/download?uuid=6e4a16b3531945e1bab99da6b34b74e6)

+ Options를 제외하고 기본 20바이트로 이루어진 헤더를 가지고 있다. 

+ Version : IP프로토콜의 버전을 의미, IPv4는 4버전이므로 4가 오게된다.(4비트)

+ Header Length : 프로토콜의 헤더 길이, 4비트로 표현할 수 있는 범위는 15까지이므로 20~60바이트 길이를 가지는 길이를 **4로 나누어 표기**한다. (4비트)

+ Type of Service : 서비스 유형, 혼잡 알림을 나타내는 역할을 하였으나 현재는 거의 쓰이지 않음 주로 비워서 보내게 된다.(1바이트)

+ Total Lenth : 헤더의 길이 + 데이터의 길이를 모두 합친 프로토콜 전체의 길이(2바이트)

+ Identifier : IP데이터그램을 구분하기 위한 필드, 여러 패킷으로 분리된 데이터를 구별하기 위해 부여한 식별자이다. (2바이트)

+ Flags : 최대 전송 범위를 넘어가는 케이스 등에서 IP데이터그램이 단편화 되었는지를 나타내는 필드, IPv6에서 삭제(3비트)

+ Fragment Offset : 단편화된 데이터그램의 순서를 나타내는 필드(13비트)

+ TTL(Time To Live) : 패킷이 라우터를 최대 몇 번까지 거칠 수 있는지를 나타내는 필드, 라우터를 통과할 때마다 1씩 감소하여 0이되면 패킷이 버려진다.(1바이트)

+ Protocol : IP프로토콜의 데이터에 캡슐화된 상위 계층의 프로토콜을 표시하는 필드.(1바이트)

+ Header Checksum : 헤더필드의 오류 검출을 위한 필드 과거 패킷이 유실되는 경우가 많아 추가적인 오류 검출을 시행하기 위해 포함되었다.(2바이트)

+ Source IP Address : 패킷을 보낸 장치의 IP주소, 즉 4바이트

+ Destination IP Address : 패킷의 목적지가 되는 장치의 IP주소, 역시 4바이트

  

### [ICMP 프로토콜](https://youtu.be/JaBCIUsFE74?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

- Internet Control Message Protocol, 인터넷 제어 메시지 프로토콜

- 네트워크 장치 위에서 실행되는 OS에서 오류 메시지를 전송받는 데 주로 사용되는 프로토콜

- IPv4프로토콜에서 패킷 전달이 실패하는 경우 출발지 호스트에 알릴 수단이 없기 때문에 사용되었다.

  ![파일:ICMP header - General-en.svg - 위키백과, 우리 모두의 백과사전](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e1/ICMP_header_-_General-en.svg/1280px-ICMP_header_-_General-en.svg.png)

+ Type : ICMP프로토콜의 타입을 의미한다. 이 값을 통해 대략적인 오류 원인을 알 수 있다. ex) 8번 - 통신요청, 0번 - 통신에 대한 응답, 3번 - 목적지 도달 실패 11번 - 요청 시간 만료
+ Code : Type에 대한 추가적인 정보를 나타내는 코드,ex) type - 11 code - 0 : TTL expired in transmit
+ Checksum : 패킷의 오류를 체크하는 필드
+ Content : Type과 Code에 따라 추가적인 메시지를 전달하는 가변길이 필드



### [라우팅 테이블](https://youtu.be/CjnKNIyREHA?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

- 네트워크 상의 특정한 목적지까지 도달하는 방식에 대해 정의한 내용을 가지고 있는 테이블. 네트워크의 지도라고 할 수 있다.
- 장치 A에서 다른 네트워크에 존재하는 장치 B와 ICMP 프로토콜 통신을 진행하는 과정
  - 1.  라우팅 테이블을 참조하여 이더넷 + IP + ICMP 구조의 패킷을 목적지(장치 A의 게이트 웨이)에 전달.
    2. 게이트웨이 라우터에서 이터넷 프로토콜>IP 프로토콜 확인 후 자신에게 온 것이 아님을 알고, 이더넷 프로토콜을 자신의 라우팅 테이블에 따라 다시 캡슐화
    3. 위 과정을 장치 B에 도달할 때까지 반복
  - 중간중간 라우팅 테이블에 MAC주소가 없을 경우 ARP 프로토콜 통신도 추가로 진행해야 하므로 훨씬 길어질 수 있다.



### [IPv4 조각화 이론](https://youtu.be/_AONcID7Sc8?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

- 조각화 : IP프로토콜에는 패킷당 데이터 전송량에 제한이 있으므로 큰 IP 패킷들이 MTU(Maximum Transmission Unit)를 갖는 링크를 통해 전송되려면 조각조각 나뉘어야 한다. 패킷을 전송에 적합한 프레임으로 변환하는 것이 조각화
- IPv4에서는 발신지와 중간 라우터에서 IP조각화를 할 수 있고 IPv6에서는 발신지에서만 IP 조각화가 가능하다.
- 패킷의 재조립은 최종 수신지에서만 가능하다.

### [IPv4 조각화 실습](https://youtu.be/QKEL9aBgHtg?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

조각화 예시 

데이터 크기 - 2379바이트, MTU - 980바이트일 경우의 조각화

IPv4만 캡슐화 할 경우 IPv4 프로토콜의 크기가 20바이트 이므로 IPv 420 + Data 960로 구성된 패킷으로 나뉜다.

총 3개의 패킷으로 나뉘며, 마지막 패킷의 데이터 크기는 2379 - (960x2) = 459바이트

각각의 패킷의 IPv4 Flag와 Fragment Offset은 다음과 같고 Identifier는 동일한 값이다.

1 : mf 1, offset = 0

2 : mf 1, offset = 960/8 = 120

3 : mf 0, offset = 1920/8 = 120

