### [HTTP 프로토콜](https://youtu.be/TwsQX1AnWJU?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

- HyperText Transfer Protocol, www에서 쓰이는 핵심 프로토콜. 문서의 전송을 위해 고안되었으나 현재 거의 모든 웹 어플리케이션에서 사용되고 있다.

- Request/Response에 기반한 서비스 제공이 특징

- HTTP/0.9 ~ HTTP/3.0 까지 발전해 왔으며 지속적으로 개선 중

- HTTP/0.9

  - 가장 최초의 HTTP프로토콜, 1.0과 분리하기 위해 0.9로 명명되었다.

  - GET메서드만이 존재하며 요청은 단 한줄로 처리.

  - ```
    GET /somepage.html
    ```

- HTTP/1.0

  - 최초로 HTTP헤더 개념이 도입.
  - HTML문서 이외의 데이터를 전송하는 기능이 추가(Content-Type의 추가)
  - 연결 수립, 동작, 연결 해제의 단순한 구조가 특징적이다.
  - 하나의 URL은 하나의 TCP연결으로, HTML문서를 전송 받은 뒤 연결을 끊고 다시 연결하여 데이터 전송
  - 연결(TCP - 3way handshake)>동작(Request, Response)>해제(TCP - 4way handshake) 의 **단순 과정이 너무 많이 반복**되어 **통신 부하**가 발생하는 문제점

- HTTP/1.1

  - Persistent Connection의 추가로 일정 시간동안 커넥션을 닫지 않고 유지할 수 있게 되었다.

  - 연결(TCP - 3way handshake)>동작(Request, Response)*N times>해제(TCP - 4way handshake)의 구조

  - 파이프라이닝 기법이 도입되어 Multiple Request의 처리가 가능해졌다. 응답을 기다리지 않고 연속적으로 요청을 보내어 **순서에 맞게 응답**을 받을 수 있게 되었다.

  - 위의 이유로, **HOL(Head Of Line Blocking) 문제**가 등장, 순서에 맞에 응답을 받아야 하기 때문에 특정 패킷에 대한 응답이 늦어지면 전체 응답 큐 자체가 늦어질 수 있다.

    ![Evolution of HTTP — HTTP/0.9, HTTP/1.0, HTTP/1.1, Keep-Alive, Upgrade, and  HTTPS | by Thilina Ashen Gamage | Platform Engineer | Medium](https://miro.medium.com/max/1000/1*hr47CCH4G0B6z24i0w-fsg.gif)

- HTTP/2.0

  - **바이너리 프레이밍 계층** 도입 - 기존의 요청 메시지를 작은 프레임으로 분리하였다. 이 때부터 header와 data의 분리가 발생한 것. 요청 메시지를 바이너리 인코딩을 통해 최적화하여 파싱 및 전송 속도의 향상을 이루었고, 오류 발생 확률도 줄었다.

    ![img](https://velog.velcdn.com/images%2Fseeker1207%2Fpost%2Fa93c6db4-ba95-48e3-8807-30cdadfdc0e7%2Fimage.png)

  + **멀티플렉싱**의 도입 - 하나의 커넥션으로 여러 응답/요청을 할 수 있었던 1.1에서 추가로 응답의 순서를 지켜야 하는 부분을 개선하여 **HOL문제를 해결**하였다. 각각의 스트림에서 분리된 프레임들을 인터리빙하여 구현하였다.

    ![img](https://velog.velcdn.com/images%2Fseeker1207%2Fpost%2F5e6a2ea2-e171-41ef-8658-fe681a1d3208%2Fimage.png)

  + Stream Priortization - 리소스간 의존 관계가 있는 파일들의 우선 순위를 설정할 수 있도록 추가된 기능 

  + Server Push - 클라이언트 측에서 기본 리소스만 받은 후 추가적인 리소스를 따로 요청하지 않고 서버측에서 전달할 수 있게하는 기능, 기본 리소스로 빠르게 화면을 렌더한 뒤 무거운 추가 리소스를 나중에 받아서 보여주는 식으로 UX개선 가능(Lazy Loading)

    ![Cycle about HTTP part 5. I'm hungry — eats heading HTTP | by Mariusz  Milewczyk | Escolasoft | Medium](https://miro.medium.com/max/585/0*iIHxCcucW5FPNFRi)

  + Header Compression - 헤더 정보를 압축하는 기능의 도입, 1.x버전에서는 중복된 헤더를 그대로 전송하지만 2.0에서는 중복되지 않은 정보만을 허프먼 인코딩한 데이터로 전송한다. 이를 통해 헤더의 크기를 대폭 줄여 페이지 로드 시간을 줄일 수 있었다. 압축에는 HPACK 압축 방식을 사용

    + HPACK : Static Dictionary(자주 사용되는 헤더필드를 미리 정의한 딕셔너리) + Dynamic Dictionary(통신 과정에서 실제로 등장하는 헤더) + Huffman Encoding의 세 가지 방법으로 구현된 압축방식
    + HPACK방식 압축 예시 : https://luavis.me/http2/http2-header

- HTTP/3.0 - QUIC 기반

  - 이전의 HTTP프로토콜들은 TCP기반의 연결이므로 신뢰성을 보장하는 TCP프로토콜에서 패킷이 유실되는 등의 문제가 생기면 연결 자체가 중단되는 HOL문제가 발생하였다. 이를 UDP기반의 QUIC 프로토콜을 적용하는 것을 통해 해결. (클라이언트 - 서버 TCP통신의 멀티플렉싱)

  - QUIC(Quick UDP Internet Connections) 

    - UDP프로토콜을 기반으로 하여 TCP의 3-way handshake과정을 하나의 패킷으로 처리, 추가적으로 연결 설정을 캐싱하여 이후 연결 시 핸드셰이킹 과정없이 연결이 수립될 수 있도록 함

      ![img](https://blog.kakaocdn.net/dn/WduEO/btqv5VHWiVk/7vlRRZap7ON5YFC6iDyJoK/img.png)

    - TLS 암호화의 기본 적용 - IP Spoofing/Replay Attack 방지

      

### [HTTP 요청 프로토콜](https://youtu.be/rxaBwwI_JnI?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

- Request Line + Header + 공백 + Body의 구조를 가지고 있다.

- Request Line

  - 요청타입 + 공백 + URI + 공백 +HTTP버전 으로 구성
  - 요청타입이 흔히 볼 수 있는 GET, POST, PUT 등등의 값.

- Header

  - 요청에 대한 부가적인 정보의 전송을 위한 필드
  - [General header](https://developer.mozilla.org/ko/docs/Glossary/General_header): 요청과 응답 모두에 적용되지만 바디에서 최종적으로 전송되는 데이터와는 관련이 없는 헤더.
  - [Request header](https://developer.mozilla.org/ko/docs/Glossary/Request_header): 페치 될 리소스나 **클라이언트 자체에 대한 자세한 정보**를 포함하는 헤더. 쿠키 세선 등의 정보가 포함
  - [Response header](https://developer.mozilla.org/ko/docs/Glossary/Response_header): **위치 또는 서버 자체에 대한 정보**(이름, 버전 등)와 같이 응답에 대한 부가적인 정보를 갖는 헤더.
  - [Entity header](https://developer.mozilla.org/ko/docs/Glossary/Entity_header): 콘텐츠 길이나 MIME 타입과 같이 엔티티 바디에 대한 자세한 정보를 포함하는 헤더.

- HTTP Method 설명 중 GET, POST만 사용해야 한다고 하지만 개발자 입장에서 RESTful API 개발시 PUT, DELETE도 사용하는게 원칙

  

### [URL, URI란?](https://youtu.be/2ikhZ_fNP5Y?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

- URI(Uniform Resource Identifier) - 인터넷 상에서 특정한 자원을 나타내는 유일한 주소를 의미한다.
  - URI 구조 - Scheme://host{:port}{/path}{?query}
  - Scheme - 요청의 형식을 의미 ftp, http, https 등등
  - host, port - IP주소와 포트번호
  - path - 요청하는 파일의 파일명 또는 폴더에 해당하는 값
  - query - 요청에 담을 수 있는 변수값



### [HTTP 응답 프로토콜](https://youtu.be/kuucNF4Zvbs?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

- Status Line + Headers + 공백 + Body 구조로 이루어짐
- Status Line - 서버의 응답코드 : https://ko.wikipedia.org/wiki/HTTP_%EC%83%81%ED%83%9C_%EC%BD%94%EB%93%9C
- Headers
  - General Header : 요청/응답이 이루어지는 시간 등 일반적인 정보가 담긴 헤더
  - Response Header : 웹서버가 브라우저에 응답하는 콘텐츠가 포함된 헤더, Location, Server, Age, Set-Cookie 등의 정보 포함
  - Entity Header : 주고받은 데이터의 본문에 대한 정보가 담긴 헤더

