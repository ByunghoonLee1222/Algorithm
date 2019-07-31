# DP(Dynamic Programming)

* 동적 계획 (상향식)
* 입력 크기가 작은 부분 문제들을 해결한 후에 그 해들을 이용하여 보다 큰 크기의 부분 문제들을 해결

### 구현방식

* Recursive 방식
* iterative 방식

---

* **선형자료구조** - 일렬로 세울수 있음(1:1)

* **비선형자료구조** -일렬로 세울수 없음(1:多,多:多)

  * Tree(1:多)

  * Graph(多:多)
    * Vertex(정점)
    * Edgd(간선)
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

    ```java
    public class AdjMatrixTest {
    	
    	static int[][] matrix;
    	static int totalV;
    	static boolean []visited;
    	
    	public static void dfs1() {
    		Stack<Integer> stack = new Stack<Integer>();
    		boolean []visited = new boolean[totalV];
    		int current = 0;
    		visited[current]=true;
    		System.out.printf(" %c",current+65);
    		do {
    		for(int i=0; i<totalV;i++) {
    			if(matrix[current][i]==1 && !visited[i]) {
    				stack.push(current);  //메소드 call
    				current = i;		  //매개변수 전달
    				visited[current] = true;
    				System.out.printf(" %c",current+65);
    				i = -1;	 //인접정점 방문 시작위해 0으로 만들어지도록 밑작업(for문 다시돌기위해)
    				}
    			}
    		}while(!stack.isEmpty()&& (current=stack.pop())!=-1);
    	}
    	
    	public static void dfs2(int current) {
    		visited[current]=true;
    		System.out.printf(" %c",current+65);
    		for(int i=0;i<totalV;++i) {
    			if(matrix[current][i]==1 && !visited[i]) {
    				dfs2(i);
    			}
    		}
    	}
    	
    	public static void main(String[] args) {
    		totalV = 7;
    		matrix = new int[][]{
    				{0,1,1,0,0,0,0},
    				{1,0,0,1,1,0,0},
    				{1,0,0,0,1,0,0},
    				{0,1,0,0,0,1,0},
    				{0,1,1,0,0,1,0},
    				{0,0,0,1,1,0,1},
    				{0,0,0,0,0,1,0},
    				};
    				visited = new boolean[totalV];
    				dfs1();
    				System.out.println();
    				dfs2(0);
    		}
    	}
    ```

    * **BFS**(너비 우선 탐색)

  