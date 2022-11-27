## HashMap과 HashTable의 차이점

- HashMap은 키값에 Null값을 허용
- HashTable은 키값에 Null값을 허용하지 않는다.
- HashMap은 멀티 쓰레드 환경 미지원
- HashTable은 멀티 쓰레드 환경을 지원
- HashMap은 멀티 쓰레드를 지원하지 않기 때문에 동기화처리를 하지 못한다.
- HashTable은 동기화처리 비용때문에 HashMap에 비해 느리다.
