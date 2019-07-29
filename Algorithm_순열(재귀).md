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



### 비트연산자

* ​     1  1  0  0			    1  0  1  0
* **&**  1  0  1  0		    **|**  0  1  1  0                 **~ **1   0

---

​            1  0  0  0			    1  1  1  0                     0  1

* **원하는 비트열을 만들기 위해 사용**

  1. <<    => 0으로 오른쪽 영역
  2. .>>   => 부호bit로 왼쪽 영역
  3. .>>> => 0으로 왼쪽 영역 (음수 유지 x)

* ```java
  1<<0  =>  0001
  1<<1  =>  0010
  1<<2  =>  0100
  
  그 위치가 사용중인지 확인할 때는 & 연산을 통해 확인
  1 0 1 0 의 세번째 자리를 확인하기위해
  & 0 0 1 0 을 연산하여 확인. ( 0 0 1 0 이면 1, 0 0 0 0이면 0)
  
  1 0 1 0 의 두번째 0을 1로 바꾸고 싶을때
  | 0 1 0 0 을 통해 1 1 1 0으로 바꾼다.
  ///////////////////////////////////////////////////////////////////////////////////
  		int i =1,j=6;
  		System.out.println("i: "+Integer.toBinaryString(i));
  		System.out.println("j: "+Integer.toBinaryString(j));
  		System.out.println("i<<2 :"+Integer.toBinaryString(i<<2));
  		//	  j  110   의 첫번째 1이 켜져있는지 꺼져있는지 궁금할때 &	
  		// 1<<0: 001	궁금한 자리가 0이면 꺼짐 1이면 켜짐
  		// 1<<1: 010
  		// 1<<2: 100  
  		System.out.println("j&(1<<2) :"+Integer.toBinaryString(j&(1<<2)));
  		System.out.println("j&(1<<1) :"+Integer.toBinaryString(j&(1<<1)));
  		System.out.println("j&(1<<1) :"+Integer.toBinaryString(j&(1<<0)));
  		//	  j  110   원하는 비트열을 켜기위해 |
  		// 1<<0: 001	
  		// 1<<1: 010
  		// 1<<2: 100  
  		System.out.println("j&(1<<2) :"+Integer.toBinaryString(j|(1<<2)));
  		System.out.println("j&(1<<1) :"+Integer.toBinaryString(j|(1<<1)));
  		System.out.println("j&(1<<1) :"+Integer.toBinaryString(j|(1<<0)));
  ```



* **10 !** 이상은 완전탐색 시 시간 초과 고려