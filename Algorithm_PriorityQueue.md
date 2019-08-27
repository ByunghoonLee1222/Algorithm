# PriorityQueue

* 최대or 최소값 빨리찾기 (단, 비교 횟수 많을 시)
* 10억정도의 연산중에 30개 정도의 간선만 거치면 찾아진다
* for문 시 10억번의 비교 끝에 찾을 수 있기에 느리다

```java
//		PriorityQueue<Integer> queue = new PriorityQueue<Integer>();
		PriorityQueue<Integer> queue = new PriorityQueue<Integer>(new Comparator<Integer>() {

			@Override
			public int compare(Integer o1, Integer o2) {
				return o1.compareTo(02)*-1; // 최대 힙
			} // 안쓰면 최소 힙 or -1 곱하지 않으면
		});
		queue.offer(10);
		queue.offer(5);
		queue.offer(3);
		queue.offer(20);
		
		System.out.println(queue.poll());
		System.out.println(queue.poll());
		System.out.println(queue.poll());
		System.out.println(queue.poll());
	}
```

