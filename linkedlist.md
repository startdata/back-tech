## linked list

- 배열에서 임의의 위치에 요소를 삽입하거나, 임의의 위치에서 요소를 삭제하는 작업은 해당 위치 뒤에 있는 요소들을 하나씩 뒤칸 혹은 앞칸으로 옮겨야 하기 때문에 시간이 너무 오래걸린다.
- 연결리스트는 특정위치에 요소의 삽입과 삭제를 배열보다 빠른 시간에 처리할 수 있다.
- 데이터와 포인터가 한 쌍으로 구성됨 일반적으로 데이터와 포인터를 노드라고 부른다
- 노드들이 메모리상에서 연속해서 저장되지 않는다.
- 배열과 다르게 메모리상의 공간을 미리 예약할 필요없이 언제든 메모리 공간을 만들수 있따.
- 노드의 논리적 순서와 메모리의 물리적 순서가 동일하지 않다.
- 이전 노드와 다음 노드를 가리키는 포인터를 가지고 있는 연결 리스트를 양방향 연결 리스트라고 한다.
- 다음 노드를 가리키는 포인터만 가지는 연결 리스트를 단방향 리스트라고 한다.
- 노드의 포인터 필드는 연결 리스트에서 다음 노드가 저장되어 있는 메모리 주소를 저장합니다. 이 주소를 이용하여 다음 노드를 찾는다.
- 첫 번째 노드(머리)와 마지막 노드(꼬리)에 대한 포인터 변수만을 가진 구조체나 클래스로 구현된다.
- 마지막 노드의 포인터는 더 이상 가리킬 노드가 없기 때문에 null로 표현