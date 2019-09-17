# DP_2



#### 동전 거스름돈 구하기( 최소 개수)

---

* Recursive

  ```java
  public class MinCoinTest2_Recur2_Memo {
  	
  	static int memo[];
      
  	public static void main(String[] args) {
  		Scanner sc = new Scanner(System.in);
  		int money = sc.nextInt();
  		memo = new int[money+1];
  		Arrays.fill(memo, -1);
  		
  		System.out.println(changeCoin(money));
  		System.out.println();
  		sc.close();
  	}	
  	//money 금액으로 교환해줄수 있는 최소 동전수 리턴
  	private static int changeCoin(int money) {
  		if(money == 0) return 0;
  		if(memo[money]!=-1) {
  			return memo[money];
  		}
  		int min = Integer.MAX_VALUE;
  		int temp = 0;
  		//1원
  		if(money>=1 && (temp = changeCoin(money-1)+1)<min) min =temp; 
  		//4원
  		if(money>=4 && (temp = changeCoin(money-4)+1)<min) min =temp;
  		//6원
  		if(money>=6 && (temp = changeCoin(money-6)+1)<min) min =temp;	
  		return memo[money] = min;
  	}
  }
  ```

* DP(상향식)

  * 1차원

  ```java
  public class MinCoinTest3_Dp1 {
      
  	public static void main(String[] args) {
  		Scanner sc = new Scanner(System.in);
  		int money = sc.nextInt();
  		int []D = new int[money+1]; // 각 금액을 만들수 있는 최소동전개수 저장할 동적 테이블
  		int min;
  		
  		for(int i=1; i<=money;++i) {
  			min = Integer.MAX_VALUE;
  			if(i>=1 && D[i-1]<min) min = D[i-1]+1;
  			if(i>=4 && D[i-4]<min) min = D[i-4]+1;
  			if(i>=6 && D[i-6]<min) min = D[i-6]+1;
  			D[i] = min;
  		}
  		System.out.println(D[money]);
  		sc.close();
  	}
  }
  ```

  * 2차원

  ```java
  public class MinCoinTest3_Dp2 {
  
  	// 동전하나를 늘려보면서 최적인 해로 바꾼다
  	public static void main(String[] args) {
  		Scanner sc = new Scanner(System.in);
  		int money = sc.nextInt();
  		int[][] D = new int[3][money + 1];
  		// 각 단위를 고려하여 금액을 만들수 있는 최소동전개수 저장할 동적 테이블
  		int[] coin = { 1, 4, 6 };
  		// 처음동전이 1원이 아닐 경우 비교 배열이 필요하다(max값 초기화된 배열)
  		for(int j =1; j<=money; ++j) {
  			D[0][j] = j;
  		}// 1원 동전만 고려해서 만들수 있는 최소동전개수 처리
  		
  		for(int i=1; i<3; ++i) {// 4, 6원 동전을 차례대로 고려
  			for(int j=1; j<=money;++j) {// 1원 ~ money원 
  				if(coin[i]<=j) {// 현 동전으로 j금액을 만들수 있다면(사용해보는 경우, 사용해 보지 않는 경우 중 최적해)
  					D[i][j] = Math.min(D[i][j-coin[i]]+1, D[i-1][j]);
  				}else { //현 동전으로 j금액을 만들수 없다면
  					D[i][j] = D[i-1][j];
  				}
  			}
  		}
  		System.out.println(D[2][money]);
  		sc.close();
  	}
  }
  ```



#### Knapsack

---

* DP

| 가방무게            | 0    | 1    | 2    | 3    | 4    | 5    | 6    | 7    | 8    | 9    | 10   |
| ------------------- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
| 물건0               | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    | 0    |
| 물건1(무게5,가치10) | 0    | 0    | 0    | 0    | 0    | 10   | 10   | 10   | 10   | 10   | 10   |
| 물건2(무게4,가치40) | 0    | 0    | 0    | 0    | 40   | 40   | 40   | 40   | 40   | 50   | 50   |
| 물건3(무게6,가치30) | 0    | 0    | 0    | 0    | 40   | 40   | 40   | 40   | 40   | 50   | 70   |
| 물건4(무게3,가치50) | 0    | 0    | 0    | 50   | 50   | 50   | 50   | 90   | 90   | 90   | 90   |

```java
public class Knapsack {

	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int N = sc.nextInt(); // 물건 개수
		int W = sc.nextInt(); // 최대 무게
		
		int[] weights = new int[N+1];
		int[] profits = new int[N+1];
		
		int [][] D = new int[N+1][W+1];
		
		for( int i=1; i<=N; ++i){
			weights[i] = sc.nextInt();
			profits[i] = sc.nextInt();
		}
		int itemWeight,itemProfit;
		for (int item = 1; item <= N; item++) {
			itemWeight = weights[item];
			itemProfit = profits[item];
			for (int weight = 1; weight <= W; weight++) {
				if(itemWeight<=weight) {
					D[item][weight] = Math.max(D[item-1][weight-itemWeight]+itemProfit, D[item-1][weight]);
				}else {// 현아이템이 weight 무게를 초과
					D[item][weight] = D[item-1][weight];
				}
			}
		}
		System.out.println(D[N][W]);
	}

}
```



#### P, NP

---

* **P(Polynomial)** : 다차시간 알고리즘이 존재하는 모든 결정 문제들의 집합
* **NP(Nondeterministic Polynomial)** : 다항식 시간 알고리즘을 찾을 수 없고, 다항식 시간 비결정적 알고리즘을 찾으면 NP에 속한다.
