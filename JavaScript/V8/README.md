
---

> # V8 엔진

---
### 특징

- C++로 작성되었다.
- 웹 브라우저 내부에서 자바스크립트 수행 속도의 개선을 목표로 고안되었다.
- JavaScript를 크롬 브라우저에서 돌려주는 엔진
- JavaScript를 Native Code로 컴파일 한다.
- 자바스크립트가 단일 스레드 이기 때문에 V8은 자바스크립트 컨텍스트 당 한 개의 프로세스를 사용한다.
- 서비스 워커를 사용한다면 워커 당 한 개의 새로운 V8 프로세스를 생성한다.
- 프로그램이 실행되면 V8엔진은 프로세스에서 일정량의 메모리를 할당한다. 
=> Resident Set이라 한다.

---

![](https://images.velog.io/images/jinpro/post/cf41c95c-5178-46d0-8c02-c70a0dbb0459/Untitled.png)

### Resident Set

- Stack
- Heap
  - Young generation
    - Semi Space
    - Semi Space
  - Old generation
    - Old Pointer Space
    - Old Data Space

---

### Garbage Collection

- 재사용하기 위해 사용되지 않은 메모리를 회수하는 것
- Young generation과 Old generation으로 나뉘어서 관리된다.
- 새로운 객체는 Young generation에 저장, 2개의 Semi space를 거쳐서 Old generation으로 보낸다.
- 힙 관리가 잘못되면 메모리 누수가 발생할 수 있다.


---

### 마이너 GC ( Scavenger )

- 마이너 GC는 Young generation을 관리한다.
- Cheney의 알고리즘을 사용해 스캐벤져(Scavenger) 과정을 구현하였다.

---

### Scavenger 알고리즘

- Young generation의 Semi Space To 영역에 새로운 객체를 생성
- To 영역에 객체를 저장할 수 없으면 V8은 마이너 GC를 발생시킨다.
- 마이너 GC 들은 객체들을 To 영역에서 From 영역으로 이동시킨다.
- 마이너 GC 들은 객체 그래프를 재귀적으로 순회하면서 메모리 사용 객체를 찾고 To 영역으로 이동시킨다.
- From 영역을 비운다.
- 한번 더 반복이 된다면 살아남은 객체들은 Old 영역으로 이동한다.

---

### 메이저 GC

- 메이저 GC는 Old generation을 관리한다.
- Old generation과 같은 큰 힙 메모리에는 스캐벤저 알고리즘이 적합하지 않다.
- 메모리 오버헤드가 있기때문에 Mark-Sweep-Compact 알고리즘을 사용하여 처리된다.
- Mark-Sweep-Compact 알고리즘

---

### V8 메모리 사용 ( 스택 vs 힙 )

- 스택의 전역프레임에 전역 스코프 보관
- 모든 함수 호출은 스택 메모리에 추가된다.
- 반환 값과 인자를 포함한 모든 지역 변수들은 스택에서 함수 프레임 블록 안에 저장된다.
- 객체 타입의 값은 힙에서 생성되고 스택 포인터를 사용해 힙에서 스택을 참조한다.
- 함수 프레임이 종료되면 스택에서 제거된다.
- 스택관리는 V8엔진이 아닌 운영 체제가 수행한다.

---

- 이벤트 루프
- setTimeout 내부 동작 방식
- Process 노드 모듈
