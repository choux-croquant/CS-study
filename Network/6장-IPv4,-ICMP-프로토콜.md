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

- 

### [라우팅 테이블 확인 실습](https://youtu.be/tVntagSJctc?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

- 

### [IPv4 조각화 이론](https://youtu.be/_AONcID7Sc8?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

- 

### [IPv4 조각화 실습](https://youtu.be/QKEL9aBgHtg?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

-