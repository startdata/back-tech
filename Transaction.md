# transaction

## 트랜잭션이란

트랜잭션이란 한 번에 처리 되어야 할 작은단위의 논리적 작업단위를 말한다.

> 여러 개의 쿼리들을 하나로 묶는 단위

---

## 트랜잭션 특징(ACID)

### 1)원자성(Atomicty)

- 트랜잭션의 연산 처리가 전체가 처리 되거나 되지 않거나 되야함 (일부 처리는 안된다.)
- 처리 중 일부만 처리되는 경우에는 rollback되어 전체 처리가 되지 않음

#### 커밋

- 쿼리를 실행하고 영구적으로 저장하는 작업

#### 롤백

- 트랜잭션으로 처리한 하나의 묶음 과정을 일어나기 전으로 돌리는 작업

> 커밋과 롤백을 통해 데이터의 무결성을 보장한다.

### 2)일관성(Consistency)

- 트랜잭션 실행 완료후 언제나 일관성 있는 DB상태를 보존
- 허용된 방식으로만 데이터를 변경해야 하는 것을 의미한다.

### 3)고립성(Isolation)

- 트랜잭션 실행 시 다른 트랜잭션의 연산이 끼어들지 못하도록 함(동시에 트랜잭션이 실행되었을때 순서를 정하거나 다른 트랜잭션이 동일한 부분에 실행이 되지 않게 함)

### 4)영속성(Durability)

- 완료된 트랜잭션의 결과는 영구적으로 DB에 저장되어야 함

---

## 트랜잭션 격리 수준

### 1) Read Uncommitted

- 트랜잭션 처리가 완료가 되지않은(commit 되기 전)데이터를 다른 트랜잭션이 읽도록 허용하는 레벨

### 2) Read Committed

- 트랜잭션 처리가 완료(commit 된)데이터만 다른 트랜잭션이 읽도록 허용하는 레벨

### 3) Repeatable Read

- 트랜잭션 중 동일한 쿼리가 여러번 실행 되었을때 첫 번째 쿼리의 레코드가 영향을 받지 않도록 하는 레벨

### 4) Serializable Read

- 트랜잭션 중 동일한 쿼리가 여러번 실행 되었을때 첫 번째 쿼리의 레코드가 영향을 받지 않도록 하고, 새로운 레코드가 나타나지 않도록 하는 레벨

---

## 트랜잭션의 직렬성

동시에 많은 요청을 받는 경우 DBMS에서 트랜잭션이 영향없이 순서대로 실행되도록 보장해야함

### 직렬성을 보장할 수 없을때 문제

> 격리 수준에 따라 발생하는 현상은 Dirty Read, Non-Repeatable Read, Phantom Read

### 1)Dirty Read

commit되지 않은 데이터(불확실한 데이터)를 읽게 되면서 일관성을 유지하지 못함

- 반복 가증하지 않은 조회와 유사하며 한 트랜잭션이 실행 중일 때 다른 트랜잭션에 의해 수정되었지만 아직 '커밋되지 않은'행의 데이터를 읽을 수 있을 때 발생

### 2)Non-Repeatable Read

한 트랜잭션에서 동일한 쿼리를 수행했을 때 결과가 다르게 나오는 문제

- 한 트랜잭션 내의 같은 행에 두 번 이상 조회가 발생했는데, 그 값이 다른 경우를 가리킨다.

### 3)Phantom Read

한 트랜잭션에서 동일한 쿼리를 수행했을 때 첫 번째 쿼리에서 없던 결과가 나타나는 문제

---

## Dead Lock(교착상태)

### 운영체제에서의 교착상태란 ?

각각의 프로세스가 서로의 자원을 점유하기 위해 대기하면서 문제가 발생한다

### 데이터베이스에서의 교착상태란 ?

DB(데이터베이스)에서 교착상태는 여러 개의 트랜잭션(Transaction)들이 실행을 하지 못하고 서로 무한정 기다리는 상태를 의미한다.
(commit이 되지않아 앞의 작업이 끝나지 않거나 동시에 같은 작업을 하는경우에 발생)

> 운영체제와 데이터베이스의 공통점은 대기상태라는 것이다. (서버가 멈춤)

### 해결방법 ?

- commit빈도를 높인다 (작업의 단위를 줄인다)
- 고립 레벨을 높여서 작업이 겹치지 않도록 한다.
- 트랜잭션 코드 안에 조회 부분을 제외한다.
