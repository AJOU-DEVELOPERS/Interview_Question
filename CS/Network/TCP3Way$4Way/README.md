## 3 Way handshake & 4 way handshake
- 네트워크간 연결 및 헤제 과정

### 3 Way handshake
- 네트워크 연결
- TCP는 장치들 사이에서 논리적인 연결을 성립하기 위해 3 Way handshake를 사용
![image](https://user-images.githubusercontent.com/64246267/143972994-84fb8f00-2033-4a55-aaa9-6f5e71f51b2a.png)

- 과정
  1. Client가 Server에게 SYN 패킷을 보냄(sequence:x)
  2. Sever가 SYN(x) 패킷을 받고 Client에게 ACK(x+1)와 SYN(y) 패킷을 보냄(sequence: y, ACK: x+1)
  3. Client는 Server로부터 ACK(x+1)와 SYN(y)를 받고 다시 서버에게 받았다는 의미의 패킷인 ACK(y+1)을 보냄

- 위의 과정 이후엔 연결이 성립


### 4 Way handshake
- 네트워크 연결 헤제
![image](https://user-images.githubusercontent.com/64246267/143973591-29ea29d3-d983-4415-94ac-ddfedae3ab0e.png)

- 과정
  1. Clinet가 서버에게 연결을 종료한다는 의미의 FIN 플래그를 보냄
  2. Server는 FIN 플래그를 받고 확인했다는 ACK 패킷을 Client에게 보냄 ( 이때 모든 데이터를 보내기 위해서 Server는 CLOSE_WAIT 상태가 된다)
  3. Server는 데이터를 모두 보내면 FIN 플래그를 Client에게 보냄
  4. Client는 FIN 플래그를 받고 확인했다는 ACK 패킷을 Server에게 보냄(이때 아직 서버로부터 못 받은 데이터가 있을 수 있기 때문에 TIMW_WAIT으로 기다린다)

- 위의 과정 이후엔 ACK을 받은 Server는 소캣을 닫는다
- TIME_WAIT 시간이 지나면 Client도 닫는다.