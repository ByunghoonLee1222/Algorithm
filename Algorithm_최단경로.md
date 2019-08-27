# 최단경로

* 간선의 가중치가 있는 그래프에서 두 정점 사이의 경로들 중에 간선의 가중치의 합이 최소인 경로
* **하나의 시작 정점에서 끝 정점까지의 최단 경로**
  * ***다익스트라(dijkstra) 알고리즘***
    * 음의 가중치 허용 X
  * ***벨만-포드(Bellman-Ford) 알고리즘***
    * 음의 가중치 허용

* **모든 정점들에 대한 최단 경로**
  * ***플로이드-워샬(Floyd-Warshall) 알고리즘***



#### Dijkstra

---

```java
public class dijkstraTest {

	public static void main(String[] args) throws NumberFormatException, IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		int N = Integer.parseInt(br.readLine());
		int end = N - 1; // 도착점
		int[][] adjMatrix = new int[N][N];
		boolean[] visited = new boolean[N];
		int[] distance = new int[N];
		final int INF = Integer.MAX_VALUE;
		Arrays.fill(distance, INF);

		StringTokenizer st;
		for (int i = 0; i < N; i++) {
			st = new StringTokenizer(br.readLine(), " ");
			for (int j = 0; j < N; ++j) {
				adjMatrix[i][j] = Integer.parseInt(st.nextToken());
			}
		} // i노드에서 j노드들까지 비용 저장

		int min = 0, current = 0;
		distance[0] = 0; // 출발정점 : 0-0까지의 최소비용 0으로 처리
		for (int i = 0; i < N; ++i) {
			// a 단계: 방문하지 않은 정점 중 최소가중치의 정점 선택
			min = INF;
			for (int j = 0; j < N; ++j) {
				if (!visited[j] && distance[j] < min) {
					min = distance[j];
					current = j;
				}
			}	
			visited[current] = true;
			if (current == end)
				break;
			// b 단계: current정점을 경유지로 하여 갈수 있는 다른 방문하지 않은 정점들에 대한 고려
			for (int j = 0; j < N; ++j) {
				if (!visited[j] // 방문하지 않은 j 정점
						&& adjMatrix[current][j] != 0 // current와 인접해 있는 j정점
						&& min + adjMatrix[current][j] < distance[j] // 시작 - current - j 비용 < 시작 - j 비용
				) {
					distance[j] = min + adjMatrix[current][j];
				}
			}
		}
		System.out.println(distance[end]);
	}

}

////////////////////////////최적화 priorityqueue사용//////////////
		distance[0] = 0; // 출발정점 : 0-0까지의 최소비용 0으로 처리

		PriorityQueue<Vertex> queue = new PriorityQueue<Vertex>();
		queue.offer(new Vertex(0, distance[0]));

		while (!queue.isEmpty()) {
			// a 단계: 방문하지 않은 정점 중 최소가중치의 정점 선택
			Vertex current = queue.poll();
			if(visited[current.vertex]) continue;
			
			visited[current.vertex] = true;
			if(current.vertex == end) break;
			
			// b 단계: current정점을 경유지로 하여 갈수 있는 다른 방문하지 않은 정점들에 대한 고려
			for (int j = 0; j < N; ++j) {
				if (!visited[j] // 방문하지 않은 j 정점
						&& adjMatrix[current.vertex][j] != 0 // current와 인접해 있는 j정점
						&& current.weight + adjMatrix[current.vertex][j] < distance[j] // 시작 - current - j 비용 < 시작 - j
																						// 비용
				) {
					distance[j] = current.weight + adjMatrix[current.vertex][j];
					queue.offer(new Vertex(j, distance[j]));
				}
			}
		}
		System.out.println(distance[end]);
	
```

