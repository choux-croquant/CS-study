### [NAT란?](https://youtu.be/Qle5cfCcuEY?list=PL0d8NnikouEWcF1jJueLdjRIC4HsUlULi)

- Network Address Translation, IP패킷의 4계층 통신 포트 번호와 수신지 및 송신지의 IP주소 등을 변환하고 NAT 테이블에 재기록하면서 네트워크 트래픽을 주고 받는 기술. 

- 패킷의 내용을 변환하는 것이기 때문에 Checksum 등을 다시 계산하여 재기록한다.

- 사설 네트워크에서 외부 네트워크에 접근하기 위해 공인 IP주소로 변환하는 등의 작업에 사용된다.

  

### 포트 포워딩

- 패킷이 라우터/방화벽 등의 네트워크 장비를 지나는 동안 특정 IP주소와 포트 번호의 통신 요청을 특정한 다른 IP와 포트 번호로 넘겨주는 NAT기술의 응용
- 게이트웨이의 반대쪽에 위치하는 사설 네트워크에 상주하는 호스트에 대한 서비스를 생성하기 위해 많이 사용된다.
- 동작 예시에 대한 글 : https://www.stevenjlee.net/2020/07/11/%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0-nat-network-address-translation-%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC-%EC%A3%BC%EC%86%8C-%EB%B3%80%ED%99%98/#:~:text=NAT%20(Network%20Address%20Translation%20%E2%80%93%20%EB%84%A4%ED%8A%B8%EC%9B%8C%ED%81%AC,%EC%A3%BC%EA%B3%A0%20%EB%B0%9B%EA%B2%8C%ED%95%98%EB%8A%94%20%EA%B8%B0%EC%88%A0%EC%9E%85%EB%8B%88%EB%8B%A4.



