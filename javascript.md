### some()

some은 callback이 참을 반환하는 요소를 찾을때까지 배열에 있는 각 요소를 실행한다.
배열안의 객체와 다른배열안의 객체를 비교할때 사용 (ex배열에서 배열빼기)

```
arr.some(callback[,thisArg])
```

#### callback

각 요소를 시험할 함수

- index: 처리할 현재 요소의 익덱스
- array: some을 호출한 배열

#### thisArg

- callback을 실행할 때 this로 사용값

#### 반환값

배열요소에 대해 참 인값을 반환하는 경우
