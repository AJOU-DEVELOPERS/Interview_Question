## 트랜잭션

### 개념

- 트랜잭션은 '일 처리 단위'를 위미하여, 논리적 연산 단위
- 한 개 이상의 데이터베이스 조작( 하나 이상의 SQL 문장이 포함)
- 트랜잭션은 '거래'이며 분할할 수 없는 최소 단위
- 결과는 모두 반영되거나 모두 취소되어야 한다
    - 즉 하나의 트랜잭션은 완료(commit) 되거나  복귀(rollback) 되어야 한다
    - 엄격한 거래를 의미

### 특징

- ACID
    - Atomicity(원자성)
    
    → 트랜잭션은 분해가 불가능한 최소단위이다
    
    → 트랜잭션의 작업이 부분적 실행거나 중단되지 않는 것을 보장
    
    → commit되거나 rollback되는 결과만이 존재
    
    - Consistency(일관성)
    
    → 고정 요소는 트랜잭션 실행 전과 후가 같아야 한다는 성질
    
    → 트랜잭션이 성공적으로 완료되면 일관적인 DB 상태를 유지하는 것, 즉 무결성이 유지되고 모순되지 말아야 된다는 성질
    
    → 참조 무결성 기법이 존재
    
    - Isolation(격리성)
    
    → 현재 트랜잭션이 실행되는 중간에는 다른 트랜잭션 연산이 침범하지 못한다는 의미
    
    → 동일한 자원에 대하여 다수의 트랜잭션이 동시에 사용할 수 없다느 성질
    
    → 병행제어 기법이 존재(직렬성을 보장하기 위해 중지, 지연) → Serial Schedule, Serializable
    
    - Durablility(영속성)
    
    → 트랜잭션에 의하여 변화된 상태는 지속적으로 유지될 수 있어야 한다는 성질
    
    → 회복 기법이 존재
    

***

Serial Schedule

- 한번에 하나씩의 트랜잭션만 실행을 했을 때 가능한 결과들의 집합
- 트랜잭션들의 결과의 경우의 수가 N!보다 적거나 같다

Serializable

- 동시에 트랜잭션이 실행되었을 때, 결과물이 Serial Schedule의 부분집합일 경우를 Serializalbe하다고 한다.

***

### 트랜잭션의 상태

- 트랜잭션 상태전이도

![image](https://user-images.githubusercontent.com/64246267/144830885-043aa9ab-f2bd-436f-af0d-ea42ace39151.png)

- 여기서 부분 완료란 트랜잭션의 마지막 연산까지 실행했지만, commit 연산이 실행되기 직전의 상태를 의미

### 트랜잭션의 연산

- Commit 연산
    - 하나의 트랜잭션이 성공적으로 끝나 데이터베이스가 다시 일관된 상태에 있을 때 이 트랜잭션이 행한 연산이 완료된 것을 트랜잭션 관리자에게 알려주는 연산
- Rollback 연산
    - 트랜잭션이 비정상적으로 종료되어 DB의 일관성이 깨졌을 때, 이 트랜잭션이 행한 모든 연산을 취소하는 연산

### 트랜잭션에서 발생할 수 있는 문제들

1. Lost Update Problem(L이라고 말하겠음)
    
    →정의:  2 개 이상의 트랜제션이 동시에 한 아이템의 데이터를 변경했을 발생하는 문제점
    
    → 트랜젝션을 지원하는 데이터베이스에서는 발생하면 안됨 → 데이터베이스들은 절대 지원 안하는데 이 오류가 발생하면 개발자들의 코드 문제
    

1. Dirty Read Problem(D이라고 말하겠음)
    
    → 정의: 한 트랜젝션에서 변경한 값(커밋x)을 다른 트랜젝션에서 읽을 때 발생하는 문제
    
    → 언제나 사용자가 느끼기에는 나 혼자 DB를 독점하는 느낌이 들어야 한다. → 이것을 위반하는게 Dirty Read Problem
    
    → 남이 수정한 값을 내가 읽게 되는 것(Dirty Read Problem)
    
    * 해결 방법: 남의 값 중 commit하지 않은 값은 읽지 않게 한다
    

1. Non-repeatable Read Problem(N이라고 말하겠음)
    - 정의: 한 트랜젝션에서 같은 값을 두 번 읽었을 떄 각각 다른 값이 읽히는 경우(문제 발생)
    - 원인: 누군가 내가 두 번 읽을 사이동안 수정하고 commit한 경우 발생
    
2. Phantom Read Problem(P이라고 말하겠음)
    - 정의: 주로 통계나 분석, aggregation function(평균 등등)을 수행하는 쿼리에서 잘못된 값이 들어오는 경우
    - 없는 값을 읽었다고 해서 Phantom Read Problem이라고 한다
    - 다른 트랜잭션에서 수행한 변경 작업에 의해 레코드가 보였다가 안 보였다가 하는 현상
    - 이를 방지하기 위해서는 쓰기 잠금을 걸어야 한다.
    - 원인: DB의 Lock 관련 때문에 발생한다

### 트랜잭션 격리 수준(isolation level)

- 동시에 여러 트랜잭션이 처리 될 대, 트랜잭션끼리 얼마나 서로 고립되어 있는지를 나타냄
- 크게 4개로 나뉨
- 아래로 내려갈수록 트랜잭션간 고립 정도가 높아지며, 성능이 떨어지는 것이 일반적
- 일반적인 온라인 서비스에서는 READ COMMITED나 REPETABLE READ 중 하나를 사용
1. READ UNCOMMITED
    - 커밋하지 않은 것도 다 읽겠다
    - D, N, P 모두 발생
    - 어플리케이션에 따라서 좋은 방법이 될 수 있다.
2. READ COMMITED
    - 커밋한 것은 다 읽겠다
    - N, P 발생
3. REPETABLE READ
    - 선행 트랜잭션이 읽기 시작한 데이터는 해당 트랜잭션이  종료될 때까지 후행 트랜잭션이 갱신하거나 삭제하는 것을 막음으로써 같이 데이터를 두 번 읽었을 때 일관성 있는 결과를 반환
    - P만 발생
    - 성능과 안정성의 균형
    - 대부분 DB가 default
4. SERIALIZABLE
    - 문제 발생 X
    - 성능에 심각한 문제
    - 읽는 것은 동시에 가능하지만 하나가 쓰거나 수정하면 모두 Lock이 걸린다

## DBMS 트랜잭션 관리

- MySQL과 MS-SQL은 4가지 모두 지원
- MYSQL default: Repeatable Read
- ORACLE은 2가지만 지원한다

### MySQL

- MySQL은 값의 사본을 만들기 때문에(멀티 버전 컨커런시 컨트롤) Repetable Read인데도 Phantom 문제가 발생하지 않는다 → 이게 MVCC
- 데이터에 접근하는 사용자는 접근한 시점에서 데이터베이스의  snapshot을 읽는다.
- 이 snapshot 데이터 변경 사항을 commit하면 데이터베이스를 덮어씌우는게 아니라 Undo 공간에 백업해둔다.
- Undo 공간에 백업
    - 백업된 데이터는 불필요하다고 판단하는 시점에 주기적으로 삭제한다.
    - Undo에 백업된 레코드가 많아지면 MySQL 서버의 처리 성능이 떨어질 수 있다.
- 이러한 변경방식은 [MVCC(Multi Version Concurrency Control)](https://en.wikipedia.org/wiki/Multiversion_concurrency_control)라고 부른다.