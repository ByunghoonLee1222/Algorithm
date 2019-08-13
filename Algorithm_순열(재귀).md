# Algorithm

### 순열(재귀)

* for문

```java
//1,2,3 세 수중 2자리 순열
	//3P2
	public static void main(String[] args) {
		//개수가 고정되어있을때 사용가능  //4개의 수는 반목문 하나 추가해야 함
		for(int i =1;i<=3;++i){//첫번째 수 
			for(int j=1;j<=3;++j){//두번째 수
				if(i!=j) {
					System.out.println(i+" "+j);
				}
				
			}//j end
		}//i end
		//k end
	}	

```

* 재귀함수

```java
/////////////////////////////////////nPn///////////////////////////////////////////	
	private static boolean[] selected;
	private static int[] numbers;
	private static int N; 
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		N= sc.nextInt();
		numbers = new int[N];
		selected = new boolean[N+1];
		permutation(0);
		System.out.println("총 경우의 수 : "+totalCount);
		sc.close();
	}
	private static int totalCount;
	private static void permutation(int index) {
		
		if(index==N) {
			totalCount++;
			System.out.println(Arrays.toString(numbers));
			return;
		}
		//가능한 선택지에 대해 반복(1~N까지 시도)
		for(int i=1;i<=N;++i) {
			//선택지를 사용할수 있는지 기존수들과 중복체크
			if(!selected[i]) {
				selected[i] = true;
				numbers[index]=i;
				permutation(index+1);
				selected[i]=false;
			}
		}
	}
//////////////////////////////////////////nPr//////////////////////////////////////
	private static boolean[] selected;
	private static int[] numbers;
	private static int N,R; 
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		N= sc.nextInt();
		R= sc.nextInt();
		numbers = new int[R];
		selected = new boolean[N+1];
		permutation(0);
		System.out.println("총 경우의 수 : "+totalCount);
		sc.close();
	}
	private static int totalCount;
	private static void permutation(int index) {
		
		if(index==R) {
			totalCount++;
			System.out.println(Arrays.toString(numbers));
			return;
		}
		//가능한 선택지에 대해 반복(1~N까지 시도)
		for(int i=1;i<=N;++i) {
			//선택지를 사용할수 있는지 기존수들과 중복체크
			if(!selected[i]) {
				selected[i] = true;
				numbers[index]=i;
				permutation(index+1);
				selected[i]=false;
			}
		}
	}
```

```java
///////////////////////////////비트연산 사용 ////////////////////////////////////////
	private static int[] numbers;
	private static int N,R; 
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		N= sc.nextInt();
		R= sc.nextInt();
		numbers = new int[R];
		permutation(0,0);
		System.out.println("총 경우의 수 : "+totalCount);
		sc.close();
	}
	private static int totalCount;
	private static void permutation(int index,int flag) {
		
		if(index==R) {
			totalCount++;
			System.out.println(Arrays.toString(numbers));
			return;
		}
		//가능한 선택지에 대해 반복(1~N까지 시도)
		for(int i=1;i<=N;++i) {
			//선택지를 사용할수 있는지 기존수들과 중복체크
			if((flag & 1<<i)==0) { // i가 기존 순열안에서 사용되고 있지 않으면
				numbers[index]=i;
				permutation(index+1,flag | 1<<i);
			}
		}
	}
```



#### NextPermutation

---

1. 뒤부터 교환이 필요한 자리 찾기(꺾이는 위치가 i, i-1과 교환)
   * i == 0 이면 return ( 꺾이는 위치가 X , 내림차순)
2. i-1위치에 다음에 올 큰 수 찾기 (맨뒤에서부터 자기자신보다 큰수 찾기=> j)
3. i-1위치 값과 j 위치 값 교환
4. i부터 오름차순 정렬( 제일 바깥쪽 점끼리 swap 하는 방식)

