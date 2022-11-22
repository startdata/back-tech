## blocking vs non-blocking

blocking과 non-bloking은 주로 IO의 읽기, 쓰기에서 사용된다.

### blocking

- 요청한 작업을 마칠 때까지 기다린다.
- 즉시 값을 반환한다.
- 반환값을 받아야 종료된다.
- Thread관점에선 요청된 작업을 마칠때 까지 대기하며 반환값을 받을때 까지 한Thread를 계속 사용/대기 한다.

### non-blocking

- 요청한 작업을 바로 종료할수 없다면 즉시 값을 반환한다.
- 바로 반환하지 않는다.
- Thread관점에서, 하나의 Thread가 여러개의 일을 처리한다.
