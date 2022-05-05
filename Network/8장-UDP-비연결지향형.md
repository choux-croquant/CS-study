### [UDP 프로토콜](https://youtu.be/3MkI3FBFzX8?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

- User Datagram Protocol

- 단순한 전송 방식을 가지고 있어 서비스 **신뢰성이 낮다**. 데이터 그램의 순서가 바뀌거나 중복되거나 누락될 가능성이 있다.

- 일반적으로 **오류 검사와 수정이 필요 없는 프로그램**에서 수행하는 것을 가정한다.

  ![File:UDP header.png - Wikimedia Commons](https://upload.wikimedia.org/wikipedia/commons/0/0c/UDP_header.png)

+ 8바이트로 적은 크기의 헤더를 가지고 있다.

+ Source Port : 송신지의 포트번호, 0~65535범위를 가지므로 이를 표현하기 위해 2바이트 필드를 가진다. 

+ Destination Port : 목적지의 포트번호로 역시 위와 같은 이유로 2바이트 필드를 가진다.

+ UDP Length : UDP프로토콜의 헤더 + 페이로드의 길이를 나타내는 값, 2바이트 필드

+ UDP Checksum : 헤더 정보의 오류를 검출하기 위한 2바이트 필드, 페이로드의 오류는 검증하지 않음.

  

+ UDP 프로토콜을 사용하는 프로그램

  + DNS 서버 : 도메인에 대한 IP주소를 알려주는 서버
  + tftp 서버 : UDP 프로토콜로 파일을 공유하는 서버
  + RIP 프로토콜 : 동적 라우팅 프로토콜의 한 종류



