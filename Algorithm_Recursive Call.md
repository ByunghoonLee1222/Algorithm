# Recursive Call(재귀 호출)

* 재귀의 끝이 있어야 한다

* 어떻게 끝낼것인가 생각하기

  * **Sum, Factorial**

  ```java
  	public static int sum(int n) {
  		if(n==1) return 1;
  		
  		return n+sum(n-1);
  		
  	}
  	public static int factorial(int n) {
  		if(n==1) return 1;
  		
  		return n*factorial(n-1);
  		
  	}
  ```

  * **Fibonacci**

  ```java
  //////////////////////////하향식//////////////////
  	public static int fibonacci(int n) {
  		if(n==1||n==2) return 1;
  		
  		return fibonacci(n-1)+fibonacci(n-2); 
  	}
  ///////////////////////////상향식////////////////
  	public static int fibonacci(int count,int before,int current) {
  		if(count == 1) return current;
  		return fibonacci(--count, current, before+current);
  	}
  	public static void main(String[] args) {
  		Scanner sc = new Scanner(System.in);
  		int N = sc.nextInt();
  		System.out.println(fibonacci(N,0,1));
  		sc.close();
  	}
  ```

  * **Printstar**

  ```java
  	//정수 N 입력받고
  	//N:3
  	//*
  	//**
  	//***
  	public static void starprint(int n) {
  		
  		//맨 아래단을 제외한 직각삼각형 찍기
  		//맨 아래단 N개 '*'찍기
  		if(n ==0) return; //기저조건
  		
  		starprint(n-1);
  		for(int i =0; i<n;++i) {
  			
  			System.out.print("*");
  		}
  		System.out.println();
  	}
  ```

* **Memoization**

  * 재귀 함수 호출 시 이전에 호출되었던 값을 기억해서 쓴다

  * 동일한 계산의 반복 수행을 제거

    ```java
    	static int memo[];
    	public static int fibonacci(int n) {
    		if(n==1||n==2) return 1;
    		if(memo[n] == 0) {
    			memo[n] = fibonacci(n-1)+fibonacci(n-2); 
    		}
    		return memo[n];
    	}
    	public static void main(String[] args) {
    		Scanner sc = new Scanner(System.in);
    		int N = sc.nextInt();
    		memo = new int[N+1];
    		System.out.println(fibonacci(N));
    		sc.close();
    	}
    ```

* **Combination**

  ```java
  	// n개 수중 k개를 조합할수 있는 경우의 수
  	// nCk
  
  	public static int combination(int n, int k) {
  		if(n==k||k==0)return 1;
  		
  		return combination(n - 1, k) + combination(n - 1, k - 1);
  	}
  ```

  