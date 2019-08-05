# Stack

* LIFO(후입-선출)
* 선형구조

Stack< E >  

E = > Object type  /  들어갈 수 있는 type  Byte, Short, Character, Integer

* push => 삽입
* pop => 분출(제거)
* peek => 분출(비제거)

```java
public class Stack {

	private String stack[];
	private int top = -1;
	private final int MAX_STACK_SIZE;

	// 객체 생성이 완료될때 final(상수) 초기화가 완료되어있어야 한다.
	// 선언시 초기화 하지 않으면 생성자에서 초기화 필수
	public Stack() {
		this(5);
	}
	public Stack(int maxSize) {
		MAX_STACK_SIZE = maxSize;
		stack = new String[maxSize];
	}

	public void push(String element) {
		if (top == MAX_STACK_SIZE - 1) {
			System.out.println("스택이 포화상태입니다.");
			return;
		}
		stack[++top] = element;
	}

	public String pop() {
		String result = peek();
		stack[top--]=null;
		//null 값을 넣어 줘야 reference 값을 끊을 수 있다.(객체 스택 시)
		return result;
	}
	
	public String pop2() {
		String result = peek2();
		if(result !=null)
		stack[top--]=null;
		//null 값을 넣어 줘야 reference 값을 끊을 수 있다.(객체 스택 시)
		return result;
	}
	
	public String peek() {
		if (isEmpty()) {
			throw new RuntimeException("스택이 공백상태입니다.");
		}
		return stack[top];
	}
	
	public String peek2() {
		if (isEmpty()) {
			System.out.println("스택이 공백상태 입니다.");
			return null;
		}
		return stack[top];
	}
	
	public int size() {
		return top+1;
	}
	public boolean isEmpty() {
		return top == -1 ? true : false;
	}
}
```

