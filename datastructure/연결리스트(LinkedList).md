### 연결리스트
연속적인 메모리 위치에 저장되지 않는 선형 데이터 구조
포인터를 사용해서 연결됨

각 노드는 데이터 필드와 다음 노드에 대한 참조를 포함하는 노드로 구성됨

### 연결리스트 사용이유
1. 배열의 경우 크기가 고정되어 있어 미리 요소의 수에 대해 할당을 받아야함
2. 배열의 경우 새로운 요소를 삽입하는 것은 비용이 많이든다.

+ 장점
  - 동적인 크기를 갖는다
  - 삽입 삭제의 비용이 작다. (탐색비용 제외시 O(1))
    - 포인터로 다음 노드를 가리키고 있어 포인터를 이용한 참조만 고치면됨

+ 단점
  + 탐색에 O(n)의 비용이 든다.
    + 배열과 달리 인덱스로 접근하지 못하고 리스트의 첫노드에서 부터 순차적으로 다음 노드로 가면서 탐색하기 때문
  + 포인터가 차지하는 여분의 메모리 공간이 각 노드에 필요

### 노드 구현
```java
class Node<E> {
    E data;
    Node<E> next;
} 
```

### 연결 리스트 구현
```java
class List<E> {
    Node<E> head = new Node<>();
    Node<E> tail = head;

    // 앞쪽에 노드 추가
    void push(Node<E> node) {
        node.next = head.next;
        head.next = node;

        if (tail == head) {
            tail = node;
        }
    }
    
    // 특정 위치 다음에 추가
    void insrtAfter(int prevPosition, Node<E> node) {
        Node<E> cur = head;

        for (int i = 0; i < prevPosition; i++) {
            if (cur.next == null) {
                throw new RuntimeExceptoin("Position out of bounds");
            }
            cur = cur.next;
        }
        
        node.next = cur.next;
        cur.next = node;

        if (node.next == null) {
            tail = node;
        }
    }
    
    // 끝쪽에 노드 추가
    void insertLast(Node<E> node){
        tail.next=node;
        tail=node;
    }
}
```


