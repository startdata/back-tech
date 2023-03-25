## 인덱스란?

인덱스란 데이트베이스 테이블의 검색 속도를 향상시키기 위한 자료구조 이다.(책 제일 마지막에 있는 색인과 동일)

---

인덱스를 활용하면, SELETE, UPDATE, DELETE의 성능이 함께 향상된다.
찾아서 바꾸고, 지워야 되기 때문에

인덱스를 빈번한 속성에 걸게되면 인덱스의 크기가 커져서 성능이 줄어들수 있다.

---

## 인덱스의 자료구조

### 해시 테이블

해시 테이블은 (key, value)로 데이터를 저장하는 자료구조로 빠른 데이터 검색이 필요할 때 유용하다.
해시가 등호(=)연산에만 특화 되어 있어 사용이 제한 적이고, 부등호 연산이 자주 사용되는 검색을 위해서는 적합하지 않다.

### B+Tree

자식 노드가 2개 이상인 B-Tree를 개선시킨 자료구조

- 리프노드(데이터노드), 인덱스노드
- 데이터노드(인덱스(key) + 데이터(value)), 인덱스노드들은 인덱스(key)만을 갖는다.
- 데이터노드들은 LinkedList로 연결
- 데이터 노드 크기는 인덱스 노드 크기와 같지 않아도 된다.

B+tree의 데이터노드들은 LinkedList로 연결하여 순차검색을 용이하게 하고, 인덱스에 맞게 최적화

### 정리

- 인덱스는 정렬이 된 상태로 저장
- 인덱스를 걸어서 테이블을 생성할때 가상의 테이블이 생성된다고 생각
- 인덱스가 테이블 block의 주소를 가지고있음
- where 절에 자주 쓰이는 컬럼을 인덱스로 지정해 놓으면 효율적
- order by 젏에 자주 쓰이는 컬럼을 인덱스로 지정해 놓으면 효율적
- 결합되는경우 select
- 인덱스가 많은 경우 select는 빨라지지만 insert, update는 속도가 느려짐
- insert,update가 정렬된 장소를 찾아서 저장해야 하고 테이블과 인덱스 둘다 해주어야 하기 때문에 느려짐

---

- where절의 좌변을 변형시키지 않아야 인덱스 사용가능

---

#### 사용법

- create index [인덱스 컬럼명] ON [기존데이터 테이블명](저장할 컬럼)
- show index from [테이블명]목록 보기
- alter table [테이블명] drop INDEX [인덱스 컬럼명]

---

### 인덱스를 사용하면 안되는 경우

1. 데이터의 변경이 많은경우 (추가,수정,삭제가 빈번한 테이블)
2. 데이터가 적은 경우

### 인덱스가 실행되지 않는 케이스

1. 인덱스 컬럼의 변형

```
SELECT * FROM EMP WHERE sal*10> 1000 => index X
SELECT * FROM EMP WHERE sal> 1000/10 => index O
```

2. 내부적인 데이터 변환(컬럼의 데이터 타입과 맞지 않는 경우)

```
SELECT * FROM USER WHERE AGE> '30' => index X
SELECT * FROM USER WHERE AGE> 30 => index O
```

3. NULL조건 사용

```
SELECT * FROM CUSTOMER WHERE AGE IS NULL => index X
SELECT * FROM CUSTOMER WHERE AGE > 0 => index O
```

4. 부정형 조건 사용

```
SELECT * FROM CUSTOMER WHERE AGE != 20 => index X
SELECT * FROM CUSTOMER WHERE AGE < 20 AND AGE > 20 => index O
```

5. LIKE 연산자 사용 (%가 앞으로 오는 경우에 사용불가)

```
SELECT * FROM CUSTOMER WHERE NAME LIKE '%A%' => index X
SELECT * FROM CUSTOMER WHERE NAME LIKE 'A%' => index O
```
### 인덱스 종류
클러스터 인덱스
넌클러스터 인덱스
