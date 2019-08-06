# Queue

* **선입선출구조** (FIFO : First In First Out)

```java
public class Queue {

	private Object[] queue;
	private final int MAX_SIZE;
	private int front, rear;

	// front: 마지막으로 dequeue된 원소자리
	// rear : 마지막으로 enqueue된 원소자리
	public Queue(int maxSize) {
		MAX_SIZE = maxSize;
		queue = new Object[maxSize];
		front = rear = -1;

	}

	public boolean isEmpty() {
		return front == rear;
	}
	
	public boolean isFull() {
		return rear == MAX_SIZE-1;
	}
	
	public void enQueue(Object item) {
		if(isFull()) throw new RuntimeException("큐가 포화상태입니다.");
		
		queue[++rear]=item;
	}
	
	public Object peek() {
		if(isEmpty()) throw new RuntimeException("큐가 공백상태입니다.");
		
		return queue[front+1];
	}
	
	public Object deQueue() {
		Object result = peek();
		queue[++front]=null;
		return result;
	}
	
}
```

* 선형 큐는 rear가 maxsize-1가 되면 deQueue를 해도 더이상 넣을 수 없는 문제 발생

* 해결 방법

  * 연산이 이루어질 때마다 저장된 원소들을 배열의 앞부분으로 모두 이동시킴( 효율성 떨어짐)
  * 따라서 원형 큐를 통해 문제 해결

  

### 원형 큐

---

* (rear+1)% max_size를 이용하여 다음 배열에 값을 삽입

```java
	// front: 마지막으로 dequeue된 원소자리
	// rear : 마지막으로 enqueue된 원소자리
	public CircularQueue(int maxSize) {
		MAX_SIZE = maxSize;
		queue = new Object[maxSize];
		front = rear = 0; ////////////////////////////// 변경부분

	}

	public boolean isEmpty() {
		return front == rear;
	}

	public boolean isFull() {
		return ((rear + 1) % MAX_SIZE) == front;///////////////////////////
	}

	public void enQueue(Object item) {
		if (isFull())
			throw new RuntimeException("큐가 포화상태입니다.");
		rear = ((rear + 1) % MAX_SIZE);///////////////////////////
		queue[rear] = item;//////////////////////////////////
	}

	public Object peek() {
		if (isEmpty())
			throw new RuntimeException("큐가 공백상태입니다.");

		return queue[((front + 1) % MAX_SIZE)];///////////////////////////////
	}

	public Object deQueue() {
		Object result = peek();
		front = ((front + 1) % MAX_SIZE);//////////////////////////////
		queue[front] = null;////////////////////////////////
		return result;
	}
```





