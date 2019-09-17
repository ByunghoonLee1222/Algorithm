# DP(Dynamic Programming)

* 동적 계획 (상향식)
* 입력 크기가 작은 부분 문제들을 해결한 후에 그 해들을 이용하여 보다 큰 크기의 부분 문제들을 해결
* 완전검색을 하는데 좀 스마트하게 하는 방법

### 구현방식

* Recursive 방식

  * Memoization (중복 호출 재사용)
    * 추가적인 메모리 공간 필요

  ```java
  public class FibonacciTest2_Memo {
  
  	static long[] call, result; //call: 호출 횟수를 담는 배열 , result : 계산된 값 저장 배열
  	static long callSum;
  
  	public static long fibo(int n) {
  		++call[n];
  		++callSum;
  
  		if (n <= 1) return n;
  		if (result[n] != 0) return result[n];
  		return result[n] = fibo(n - 2) + fibo(n - 1);
  	}
  
  	public static void main(String[] args) {
  		Scanner sc = new Scanner(System.in);
  		int N = sc.nextInt();
  
  		call = new long[N + 1];
  		result = new long[N + 1]; // memo 배열의 초기값은 메모여부를 판단할 수 있는 값이어야 한다
  
  		System.out.println(fibo(N));
  		
  		for (int i = 0; i <= N; ++i) {
  			System.out.println("fibo(" + i + ") : " + call[i]);
  		}
  		System.out.println(callSum);
  		sc.close();
  	}
  
  }
  ```

* iterative 방식

#### 수학적 귀납법

* ```java
  public class Ex1_아파트칠하기_Fibonacci {
  
  	public static void main(String[] args) {
  		Scanner sc = new Scanner(System.in);
  		int N = sc.nextInt();
  		int[][] D = new int[N + 1][2];
  		// D[i][0] : i층을 노란색으로 색칠할수 있는 경우의수 (i-1층의 노란색의 경우의수 +i-1층의 파란색의 경우의수)
  		// D[i-1][0] + D[i-1][1]
  		// D[i][1] : i층을 파란색으로 색칠할수 있는 경우의수 (i-1층의 노란색의 경우의수)
  		// D[i-1][0]
  		for (int i = 2; i <= N; ++i) {
  			D[i][0] = D[i-1][0] + D[i-1][1];
  			D[i][1] = D[i-1][0];
  		}
  		System.out.println(D[N][0]+D[N][1]);
  		
  		sc.close();
  	}
  }
  //		int [] D = new int[N+1];
  //		D[0] = 1; // 0층도 아무것도 안칠하는 경우의수 1
  //		D[1] = 2; // 1층은 피보나치의 3항과 같다.
  //		for(int i= 2; i<=N; ++i) {
  //			D[i] = D[i-2]+D[i-1];
  //		
  //		System.out.println(D[N]);
  ```



---

* **선형자료구조** - 일렬로 세울수 있음(1:1)

* **비선형자료구조** -일렬로 세울수 없음(1:多,多:多)

  * Tree(1:多)

  * Graph(多:多)
    * Vertex(정점)
    * Edge(간선)
    * ***그래프를 표현하는 방법***(인접=연결되어있다)
      * **인접행렬**(정점 수 적을때)
        * 정점의수 :N -> NxN 행렬
        * 교차위치에 인접여부 체크
        * 방향성 없다 => 양방향 (대각선 기준 복사)
        * 행 1: 진출 / 열 1: 진입
      * **인접리스트**(정점 수 많을때)
        * 각 배열에 링크를 넣어 연결관리

  * **두가지 방법**

    * **DFS**(깊이 우선 탐색)
      * 재귀적
      * 반복적+Stack(후입선출)
        * 최상위 root로 전체 탐색 가능 
        * 직전의 node로 돌아가야 같은 계층의 다른 node로 접근 가능(Stack)
        * 메서드가 메서드를 부르는 것도 Stack의 일종

    * **BFS**(너비 우선 탐색)
  