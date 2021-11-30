## OSI 7 계층 구조

- 7계층을 나누는 이유는 통신이 일어나는 과정을 단계별로 알 수 있고, 특정한 곳에 이상이 생기면 그 단계만 수정할 수 있기 때문이다

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1ee96930-35c8-4b09-b164-b48c7d8bb362/Untitled.png)

### 각 계층 별 헤더

### 1. Physical Layer(물리 계층)

- 하드웨어 전송기술로 구성
- 물리적으로 연결된 두 대의 컴퓨터가 0과 1의 나열을 전기적 신호로 변환하여 주고받을 수 있게 해주는 레이어
    - 01010 → 아날로그 신호 : 인코딩
    - 아날로그 신호 → 010101 : 디코딩
- 주요 프로토콜 : [X.21](https://itwiki.kr/index.php?title=X.21&action=edit&redlink=1), [RS-232](https://itwiki.kr/index.php?title=RS-232&action=edit&redlink=1) 등
- 단위 : 비트

### 2. Data Link Layer(데이터링크 계층)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/101068ec-d886-4045-9d09-fc5d35bbd7f5/Untitled.png)

- 만약 물리 계층만 존재했을 때, 여러 대의 컴퓨터가 전선으로 연결되어 있으면, 하나의 컴퓨터에게 여러대의 컴퓨터가 동시에 데이터를 보내면 데이터가 뒤섞일 위험이 존재
- 데이터 링크 계층은 이를 위해 데이터의 앞, 뒤에 데이터임을 구분해주는 패킷을 추가하여 데이터를 구분하게 해주는 게층
- 네트워크 카드의 MAC 주소를 통해 목적지를 찾아간다
- 주요 프로토콜 : [HDLC](https://itwiki.kr/w/HDLC), [X.25](https://itwiki.kr/w/X.25), [Ethernet](https://itwiki.kr/index.php?title=Ethernet&action=edit&redlink=1), [TokenRing](https://itwiki.kr/index.php?title=TokenRing&action=edit&redlink=1), [DFFI](https://itwiki.kr/index.php?title=DFFI&action=edit&redlink=1), [FrameRelay](https://itwiki.kr/index.php?title=FrameRelay&action=edit&redlink=1) 등
- 단위 : 프레임

### 3. Network Layer(네트워크 계층)

- 스위치, 라우터를 사용하여 하나의 네트워크에서 다른 네트워크와의 연결을 하기 위한 계층
- 수많은 네트워크들의 연결 속에서 목적지 컴퓨터의 IP번호를 패킷에 붙여 목적지로 데이터를 보낼 수 있게 함
    - IP 주소를 이용해서 길을 찾는 것을 routing
    - 자신 다음의 라우터에게 데이터를 넘겨주는 것을 forwarding
    - 상대방의 IP 번호를 찾는 방법은 라우팅 공부(라우팅 알고리즘)
- 주요 프로토콜 - IP, ARP, ICMP, IGMP, RIP, RIP v2, OSPF, IGRP, EIGRP, BGP 등
- 단위: 패킷

### 4. Transport layer(전송 계층)

- 목적지로 보낸 데이터가 어떤 프로세스에 할당받아야 하는지에 대한 패킷을 붙이는 계층
- 프로세스의 고유 번호도 보내는 쪽에서 알고 있어야 한다.
- 포트를 열어두고 프로그램들이 전송을 할 수 있도록 제공
- 주요 프로토콜 - TCP, UDP
- 단위: 세그먼트

### 5. Session layer(세션 계층)

- 데이터가 통신하기 위한 논리적 연결을 담당
    - TCP/IP 새션을 만들고 없애는 역할 보유
- 단위: 데이터 또는 메시지

### 6. Presentation layer(표현 계층)

- 데이터 표현에 대한 독립성을 제공하고 암호화하는 역할 담당
- 파일 인코딩, 명령어 포장, 등
- 단위: 데이터

### 7. Application layer(응용 계층)

- 데이터의 최종 목적지로 응용 프로세스와 직접 관계하여 일반적인 응용 서비스루 수행
- 단위: 데이터

## OSI 7계층, TCP 계층, TCP updated 계층

- OSI 7계층은 계층이 너무 많아 복잡하여 시장 싸움에서 TCP/IP 계층이 승리
- 최근 TCP/IP updated 모델이 등장 → OSI 7계층에서 5,6,7계층만 합친 형태로 볼 수 있게 되었다.

![https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e5ea693c-d7ea-4cbc-ae7c-fdc855a83a45/Untitled.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e5ea693c-d7ea-4cbc-ae7c-fdc855a83a45/Untitled.png)