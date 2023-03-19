# VIEW Table

- 하나의 가상 테이블이라고 생각할수 있다.
- 실제 데이터가 저장되는 것이 아니고, 데이터를 관리하는것을 보여주기만 한다.
- 실제 테이블이 생성되어 테이블에 데이터가 insert가 되는 것이 아닌 SQL만 저장된다.

## 뷰 생성

```sql
CREATE 생략가능[OR REPLACE] 생략가능[FORCE | NOFORCE] VIEW 뷰명 AS (SELECT문)
생략가능[WITH CHECK OPTION 생략가능[CONSTRAINT 제약조건명]]
생략가능[WITH READ ONLY 생략가능[CONSTRAINT 제약조건명]]
```

- OR REPLACE option : 뷰를 수정할 때 DROP 없이 수정 가능
- With Check option : 주어진 제약 조건에 맞는 데이터만 입력 및 수정 가능
- With read only : 조횜 만 가능

## View Table를 사용하는 이유

- 한개의 뷰로 여러 테이블의 데이터를 검색할수 있다.
  - 여러가지 조인을 해서 가져오는 데이터를 묶어서 사용
- 뷰를 통해서만 데이터에 접근하므로 뷰에 없는 데이터를 보호할 수 있다.
