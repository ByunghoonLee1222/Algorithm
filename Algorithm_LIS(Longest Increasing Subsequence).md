# LIS(Longest Increasing Subsequence)

* 최장 증가 수열
* 배열 순서를 유지하면서 크기가 점진적으로 커지는 가장 긴 부분수열을 추출하는 문제

```java
public class LISTest {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int N = sc.nextInt();
		int[] arr = new int[N + 1];
		int[] D = new int[N + 1]; // 최장길이 저장

		for (int i = 1; i <= N; i++) {
			arr[i] = sc.nextInt();
		}

		for (int i = 1; i <= N; i++) {// i: 마지막에 붙일 현재 수
			D[i] = 1;
			for (int j = 1; j < i; j++) {// j: i보다 앞선 이전 수들
				if (arr[j] < arr[i] && D[j] + 1 > D[i]) {
					D[i] = D[j] + 1;
				}
			}
		}
		Arrays.sort(D);
		System.out.println(D[N]);
		
		sc.close();
	}
}
```

* 이진 검색 활용
  * (int) Arrays.binarySearch
  * 양수(해당 값이 있는 경우) => 찾은 위치 인덱스
  * 음수(해당 값이 없는 경우) => -insertPoint -1 => 절대값 -1 => 삽입 위치

```java
public class LISTest2_BinarySearch {

	public static void main(String[] args) {
		Scanner s = new Scanner(System.in);
		int N = s.nextInt();
		int[] arr = new int[N];
		int[] LIS = new int[N];
		
		for (int i = 0; i < N; i++) {
			arr[i] = s.nextInt();
		}
		
		int size = 0;
		//subSeq[size++]=arr[0]; // 첫번째 원소는 이전 비교원소가 없으므로 무조건 넣고 시작

        for (int i=0; i < N; i++) {
            int temp = Arrays.binarySearch(LIS, 0, size, arr[i]); // 리턴값 : -insertPoint -1
            temp = Math.abs(temp)-1;//삽입위치
            LIS[temp] = arr[i];// temp 자리에 값을 update 하면 그 의미는 
            					  // 0인덱스 위치부터 temp위치까지의 원소 갯수가  temp위치에 저장된 그 값을 마지막으로 하는 LIS 길이가 됨
            					  // 배열의 원소가 LIS를 이루는 구성요소와는 관계가 없다.

            if (size == temp) {// 삽입위치의 인덱스와 크기가 같으면(결국,마지막이 삽입위치라는 얘기임) 크기 1늘림.
                size++;
            }
        }
        System.out.println(size);
	}
}
```



