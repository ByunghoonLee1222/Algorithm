# Greedy

* 그 순간 최적이라고 생각되는 것을 선택해 나가는 방식
* 지역적으로는 최적이지만, 그 선택들을 계속 수집하여 최종적인 해답을 만들었다고 하여, 그것이 최적이라는 보장은 없다.



#### 거스름돈 줄이기

* 가장 큰 동전 단위가 나머지 하위 동전들을 대체할 수 있으면 가장 큰 동전이 최소값
* ex. **500** 100 50 10  - 이경우 greedy적 접근 가능
* ex. **500** ***400*** 100 50 10 - 이경우 400원 대체 불가

```java
public class MinCoinChangeTest {

	public static void main(String[] args) {
		int [] coin = {500,100,50,10};
		int [] result = new int[coin.length];
		
		int money = new Scanner(System.in).nextInt();
		
		for(int i=0; i<coin.length;++i) {
			result[i] = money / coin[i];
			money = money % coin[i];
		}
		System.out.println(Arrays.toString(result));	
	}
}
```



#### Knapsack

---

* **0-1 Knapsack**
  * 배낭에 물건을 통째로 담아야 하는 문제
  * 물건을 쪼갤 수 없는 경우
  * **완전 검색 방법**
    * 모든 부분집합을 구해 무게를 초과하는 집합들은 버리고
    * 나머지 집합에서 총 값이 가장 큰 집합을 선택 (시간복잡도 2^n)
  * **탐욕적 방법**
    1. 값이 비싼 물건부터 채운다 => 결과 최적 아님
    2. 무게가 가벼운 물건부터 채운다 => 최적해 아님
    3. 무게 당 값이 높은 순서로 물건을 채운다 => 최적해 아님
    4. **따라서, 탐욕적 방법으로는 구하기 힘듬**
* **Fractional Knapsack**
  * 물건을 부분적으로 담는 것이 허용되는 문제
  * 물건을 쪼갤 수 있는 경우
  * 이 경우 탐욕적 방법 가능
  * 무게당 값이 높은 순서로 물건을 채운 후 남은 무게를 남은 물건을 짤라서 채운다



#### MeetingRoom 예약

---

1. 종료 시간이 빠른 순서로 정렬
2. 첫 번째 활동을 선택
3. 활동의 종료시간보다 빠른 시작 시간을 가지는 활동을 모두 제거
4. 남은 활동들에 대해 앞의 과정을 반복

```java
///////////////////////////////배열 사용///////////////////////////////
public class ConferenceRoom3 {
	static int T;
	static StringTokenizer st;

	public static void main(String[] args) throws NumberFormatException, IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		T = Integer.parseInt(br.readLine());
		//ArrayList<MeetingRoom> list[] = new ArrayList<MeetingRoom>();
		int list[][] = new int[T][];
		for (int t = 0; t < T; ++t) {
			st = new StringTokenizer(br.readLine());
			list[t] = new int[] {Integer.parseInt(st.nextToken()),Integer.parseInt(st.nextToken()),Integer.parseInt(st.nextToken())};
			
		}
		List<int[]> result = makeSchedule(list);
	//	System.out.println(result.size());
		for(int[] meetingRoom : result) {
			System.out.println(meetingRoom[0]);
		}
	
	}

	private static List<int[]> makeSchedule(int[][] list) {
		List<int[]> result = new ArrayList<int[]>();
		// 자동으로 compareTo 메서드를 불러서 정렬
		Arrays.sort(list, new Comparator<int[]>() {

			@Override
			public int compare(int[] o1, int[] o2) {
				int a = o1[2] - o2[2];
				//종료 시간 같을 시 시작시간 비교
				return a==0? o1[1] - o2[1] : a;
			}
		});
		
		result.add(list[0]);
		for(int i=1; i<list.length;++i) {
			if(result.get(result.size()-1)[2] <= list[i][1]) {
				result.add(list[i]);
			}
		}
		
		return result;
		
	}
}
//////////////////////////////Class 사용///////////////////////////////

public class ConferenceRoom2 {
	static int T, number, min;
	static int con[][];
	static StringTokenizer st;
	static int choice[];

	static class MeetingRoom implements Comparable<MeetingRoom> {
		int no;
		int start;
		int end;
		
		public MeetingRoom(int no, int start, int end) {
			this.no = no;
			this.start = start;
			this.end = end;
		}
		@Override
		public int compareTo(MeetingRoom o) {
			//종료시간 우선 비교
			int a = this.end - o.end;
			//종료 시간 같을 시 시작시간 비교
			return a==0? this.start - o.start : a;
		}

	}

	public static void main(String[] args) throws NumberFormatException, IOException {
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		T = Integer.parseInt(br.readLine());
		//ArrayList<MeetingRoom> list[] = new ArrayList<MeetingRoom>();
		MeetingRoom list[] = new MeetingRoom[T];
		for (int t = 0; t < T; ++t) {
			st = new StringTokenizer(br.readLine());
			int no = Integer.parseInt(st.nextToken());
			int start = Integer.parseInt(st.nextToken());
			int end = Integer.parseInt(st.nextToken());
			list[t] = new MeetingRoom(no, start, end);
		}
		List<MeetingRoom> result = makeSchedule(list);
		System.out.println(result.size());
		
		for(MeetingRoom meetingRoom : result) {
			System.out.println(meetingRoom.no);
		}
	}

	private static List<MeetingRoom> makeSchedule(MeetingRoom[] list) {
		List<MeetingRoom> result = new ArrayList<MeetingRoom>();
		// 자동으로 compareTo 메서드를 불러서 정렬
		Arrays.sort(list);
		result.add(list[0]);
		for(int i=1; i<list.length;++i) {
			if(result.get(result.size()-1).end <= list[i].start) {
				result.add(list[i]);
			}
		}	
		return result;		
	}
}
```

