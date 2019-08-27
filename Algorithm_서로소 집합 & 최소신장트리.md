# 서로소 집합

* 서로 중복 포함된 원소가 없는 집합들
* 집합에 속한 하나의 특정 멤버를 통해 각 집합들을 구분한다
* 이를 **대표자(representative)**라 한다
* **표현방법**
  * 연결 리스트
    * 같은 집합의 원소들은 하나의 연결리스트로 관리
    * 연결리스트의 맨앞의 원소를 집합의 대표
    * 각 원소는 집합의 대표언소를 가리키는 링크를 갖는다
  * 트리
    * 하나의 집합을 하나의 트리로 표현
    * 자식 노드가 부모 노드를 가리키며 루트 노드가 대표자



# 최소신장트리(MST)

* **그래프에서 최소 비용 문제**
  * 모든 정점을 연결하는 간선들의 가중치의 합이 최소가 되는 트리
  * 두 정점 사이의 최소 비용의 경로 찾기
* **신장 트리**
  * n 개의 정점으로 이루어진 무향 그래프에서 n개의 정점과 n-1개의 간선으로 이루어진 트리
* **최소신장트리**
  * 무향 가중치 그래프에서 신장 트리를 구성하는 간선들의 가중치의 합이 최소인 신장 트리

#### Prim

---

```java
	public static void main(String[] args) throws NumberFormatException, IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int N = Integer.parseInt(br.readLine());
		int[][] adjMatrix = new int[N][N]; // 인접행렬
		boolean[] visited = new boolean[N]; // 정점 방문여부
//		ArrayList<Integer> list = new ArrayList<Integer>(); // 방문한 정점번호 리스트 
		// priorityQueue 사용 시 방문한 노드의 모든 간선들이 넣어지고 그중에 최소값이 나오기 때문에 정점번호 리스트가 필요없다
		StringTokenizer st;
		for (int i = 0; i < visited.length; i++) {
			st = new StringTokenizer(br.readLine(), " ");
			for (int j = 0; j < N; ++j) {
				adjMatrix[i][j] = Integer.parseInt(st.nextToken());
			}
		} // i노드에서 j노드들까지 비용 저장

		int result = 0 , count =0;

		PriorityQueue<Vertex> queue = new PriorityQueue<Vertex>();

		// 임의의 정점(0)을 첫정점으로 선택
		queue.offer(new Vertex(0, 0));

		// 기존에 방문한 모든 정점들을 기준으로 최소비용으로 방문가능한 정점 찾기
		while (!queue.isEmpty()) {
			Vertex current = queue.poll(); // 최소비용의 정점 선택
			
			if(visited[current.vertex] == true)
				continue;
			
			result += current.weight;
			visited[current.vertex] = true;
			// 인접 정점들의 비용을 모두 저장하기 때문에 이미 처리된 정점들이 중복해서 나오게 되는 문제 발생
			if(++count == N) break; // 중복 정점 문제 해결
			for (int i = 0; i < N; i++) {
				if(!visited[i]&& adjMatrix[current.vertex][i] != 0) {
					queue.offer(new Vertex(i, adjMatrix[current.vertex][i]));
					
				}
			}
		}
		System.out.println(result);
	}

	static class Vertex implements Comparable<Vertex> {
		int vertex;
		int weight;

		public Vertex(int vertex, int weight) {
			super();
			this.vertex = vertex;
			this.weight = weight;
		}

		@Override
		public int compareTo(Vertex o) {
			return Integer.compare(this.weight, o.weight);
		}

	}
}
```



#### KRUSKAL

---

1. 최초, 모든 간선을 가중치에 따라 오름차순으로 정렬
2. 가중치가 가장 낮은 간선부터 선택하면서 트리를 증가시킴
   * 사이클이 존재하면 다음으로 가중치가 낮은 간선 선택
3. n-1 개의 간선이 선택될 때 까지 2 반복

```java
private static boolean union(int a, int b) {
		int aRoot = find(a);
		int bRoot = find(b);

		if (aRoot != bRoot) {
			parents[bRoot] = aRoot;
			return true;
		}
		return false;
	}

	private static int find(int a) {
		if (parents[a] < 0)
			return a;
		return parents[a] = find(parents[a]);
	}
```

