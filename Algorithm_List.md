# List

* set과 map은 자료의 순서가 없다 ( map도 자료구조가 set으로 이루어짐)

#### LinkedList

* Node의 link(reference)를 따라서 다음 Node로 간다
* Head가 가장 앞의 노드를 가리킨다
* 최종적으로 NULL을 가리키는 Node리스트의 가장 마지막 Node이다
* 노드의 마지막을 찾는 오버헤드 발생 => 마지막을 나타내는 Tail을 만들면 줄일 수 있다

##### 생성방법

* 헤드가 가지고 있는 reference를 첫번째 Node의 링크값에 넣는다

* Node 삭제 시 해당 Node를 Null처리 해준다
* 마지막 Node 삭제 시 이전 Node를 찾아 Null처리 해준다
* 마지막 Node가 한개 있으면 Head를 Null처리 

```java
private static class Node {
		Object data;
		Node link;

		public Node() {

		}

		public Node(Object data) {
			this.data = data;
		}

		public Node(Object data, Node link) {

			this(data);
			this.link = link;
		}
	}

	private Node head; // 첫번째 노드의 포인터 역할
	private int size;

	public void addFisrstNode(Object data) {
		Node newNode = new Node(data, head); // head에 저장된 첫번째 노드를 새노드의 링크로
		head = newNode; // head에 새 노드 연결
		size++;
	}

	public Node getLastNode() {
		Node current = head;
		if (current != null) {
			while (current.link != null) {
				current = current.link;
			}
		}
		return current;
	}
```



> **이전노드 찾기의 어려움을 극복한 이중 연결 리스트**

##### 이중 연결 리스트(Doubly Linked List)

* prev, next 값 가지고 있다

* ```java
  private static class Node {
  		Object data;
  		Node prev, next;
  		
  		public Node() {
  
  		}
  
  		public Node(Object data) {
  			this.data = data;
  		}
  
  		public Node(Object data, Node prev, Node next) {
  			this(data);
  			this.prev = prev;
  			this.next = next;
  		}
  	}
  
  	private Node head; // 첫번째 노드의 포인터 역할
  	private int size;
  
  	public void addFisrstNode(Object data) {
  		Node newNode = new Node(data, null, head); // head에 저장된 첫번째 노드를 새노드의 링크로
  		if (head != null) {
  			head.prev = newNode; // head에 새 노드 연결
  		}
  		head = newNode;
  		size++;
  		
  	}
  ```

  

