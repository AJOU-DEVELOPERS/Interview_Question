> # 관찰자 패턴

## Observer 관찰자 패턴

![](https://images.velog.io/images/jinpro/post/5fc802aa-20e6-4ff6-8a5e-4196625de405/%E1%84%83%E1%85%A1%E1%84%8B%E1%85%AE%E1%86%AB%E1%84%85%E1%85%A9%E1%84%83%E1%85%B3.png)

객체의 상태 변화를 관찰하는 Observer 들의 목록을 객체에 등록하여 상태 변화가 있을 때마다 메서드 등을 통해 객체가 직접 목록의 각 옵저버에게 통지하도록 하는 디자인 패턴

#### Observable - Observer // 발행자 - 구독자

---

## Publisher - Subscriber

![](https://images.velog.io/images/jinpro/post/f1c4fa13-3571-4665-b6e1-8ccc4d193d00/Untitled.png)

발행 - 구독 패턴은 구독 객체와 발행 객체 사이에 Center를 배치함으로써 간접적인 연결을 가져갈 수 있다.

### 메시지 큐

프로세스가 req,res가 아닌 데이터를 교환할 때 사용하는 통신방법.

메시지 지향 미들웨어(MOM) 개념을 구현한 시스템으로
비동기 메시지를 사용하는 프로그램 간 데이터 송수신 방법이다.

기존에 분산되어있던 데이터 처리를 한 곳에 집중하면서, 메시지 브로커를 두어 필요한 프로그램에 작업 분산하는 것이 목적이다. 보통 대용량 데이터 처리 배치 작업, 채팅, 알림 등 쓰인다.

---

## Observer VS Publisher-Subscriber

- Observer 패턴은 subject가 직접적으로 observe에게 알림을 준다.
- Publisher-Subscriber는 Pub/Sub 패턴 사이의 채널을 통해 간접적으로 알림을 받는다.
- Pub-Sub 패턴은 직접적인 관계가 아니기 때문에 코드 관리, 재사용성, 안정성이 높다.
