### [ARP 프로토콜](https://youtu.be/LDsp-Xb168E?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

+ Address Resolution Protocol, 주소를 결정하는 프로토콜이다. 
+ 같은 네트워크 상에서 통신을 하기 위해 필요한 **MAC주소**를 IP주소를 통해 알아오는(IP주소와 MAC주소의 바인딩) 프로토콜

![img](http://www.tcpipguide.com/free/diagrams/arpformat.png)

+ 총 28바이트로 이루어진 프로토콜

+ Hardware Type : 2계층에서 사용하는 프로토콜의 타입을 나타내는 2바이트 값,  인터넷 환경에서 주로 이더넷이 오며 0001코드를 가진다. 

+ Protocol Type : 주로 IPv4의 프로토콜 타입인 0800이 오게 된다. 2바이트 필드

+ Hardware Address Length : 하드웨어의 MAC주소 바이트 길이, MAC주소가 6바이트이므로 06을 나타내기 위해 1바이트 할당

+ Protocol Address Length : IP주소의 바이트 길이, IP주소가 4바이트이므로 04을 나타내기 위해 1바이트 할당

+ Opcode : MAC주소를 요청하는지 응답하는지 구별하기 위한 필드, 0001은 MAC주소의 요청 0002는 요청에 대한 응답이다.

+ Source(Sender) Hardware Address : 송신지의 MAC주소를 나타내는 6바이트 필드

+ Source(Sender) Protocol Address : 송신지의 IP주소를 나타내는 4바이트 필드

+ Destination(Target) Hardware Address : 수신지의 MAC주소를 나타내는 6바이트 필드

+ Destination(Target) Protocol Address : 수신지의 IP주소를 나타내는 4바이트 필드

+ ARP 프로토콜에서 사용되는 다양한 파라미터에 대한 추가 정보 : https://www.iana.org/assignments/arp-parameters/arp-parameters.xhtml

  

### ARP 프로토콜의 통신 과정

임의의 장치 A에서 IP주소는 알고 MAC주소는 모르는 B로 요청을 보내는 상황을 가정

1. 이터넷 프로토콜 > 송신지 MAC주소 + 목적지 MAC주소 + 상위프로토콜 코드

2. 목적지의 **MAC주소를 모르기 때문**에 ARP프로토콜 요청해야한다.

3. ARP프로토콜 요청 시 일단 목적지의 MAC주소를 00 00 00 00 00 00으로 비우고 캡슐화

4. 캡슐화 시 이터넷프로토콜의 목적지 MAC주소를 FF FF FF FF FF FF로 설정(모든 값이 1)이는 **브로드 캐스트 주소**를 의미한다. 즉 MAC주소를 모르기 때문에 같은 네트워크 대역 전체에 요청을 보낸다.

5. 스위치(2계층 하드웨어)에 전달된 요청을 역캡슐화 하여 이터넷 프로토콜을 확인

6. 브로드 캐스트 MAC주소로 되어 있으므로 전체에 전달

7. 각각의 호스트는 받은 요청의 이더넷 프로토콜을 다시 역캡슐화

8. 브로드 캐스트 요청이므로 이어서 ARP프로토콜도 역캡슐화, 요청의 대상이 되는 IP주소를 확인

9. 확인한 IP주소가 호스트의 IP주소와 다를 경우 패킷을 버리고 같은 경우 **ARP프로토콜에 대한 응답 ARP프로토콜을 송신**, 이때 호스트의 MAC주소를 포함하여 전달한다.

10. ARP응답 프로토콜을 스위치에 전달하고 스위치는 이더넷프로토콜을 확인한 뒤 다시 A에게 전달

11. A가 응답을 수신한 후 ARP 캐시 테이블에 데이터(IP와 MAC주소가 바인딩된 정보)를 저장

    

### ARP 테이블

- 통신했던 장치들의 IP주소와 MAC주소를 바인딩한 정보를 캐싱한 테이블

