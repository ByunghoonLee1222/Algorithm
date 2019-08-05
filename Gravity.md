# Gravity

* n: 방의 크기
* n개의 상자 높이

test

**--input--**

```
9

7 4 2 0 0 6 0 7 0
```

**--result--**

```
7
```

```java
public class Gravity_이병훈 {
static int arr[][],first[][];
static int down[][];
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		int box[] = new int[9];
		first = new int[9][9];
		arr = new int[9][9];
		down= new int[9][9];
		for (int i = 0; i < 9; ++i) {
			box[i] = sc.nextInt(); // box 길이 입력
		}
		
		//초기 블럭상태
		for (int i = 0; i < 9; ++i) {
			for (int j = 0; j < box[i]; ++j) {
				first[8-j][i] = 1;
			}
		}
		for (int i = 0; i < 9; ++i) {
			System.out.println(Arrays.toString(first[i]));
		}
		
		////우 90도
		System.out.println();
		for (int i = 0; i < 9; ++i) {
			for (int j = 0; j < box[i]; ++j) {
				arr[i][j] = 1;
			}
		}
		for (int i = 0; i < 9; ++i) {
			System.out.println(Arrays.toString(arr[i]));
		}
		System.out.println();
		
		//상자 낙하
		int count;
		for (int i = 0; i < 9; ++i) {
			count = 0;
			for (int j = 0; j < 9; ++j) {
				if (arr[j][i] == 1) {
					count++;
				}
			}
			//아래부터 쌓기
			for (int q = 0; q < count; ++q) {
				down[8-q][i] = 1;
			}
		}
		
		for (int i = 0; i < 9; ++i) {
			System.out.println(Arrays.toString(down[i]));
		}
		
		//최대 낙폭 구하기
		int fall = 0;
		int answer = 0;
		for (int i = 0; i < 9; ++i) {

			for (int j = 0; j < 9; ++j) {
				if(arr[j][i]==1) {
					fall =0;
					for(int k=j+1;k<9;++k) {
						if(arr[k][i]==0) {
							fall++;
						}
					}
				}
				if(fall<9 && fall>answer) {
					answer = fall;
				}
			}

			
	}

		System.out.println("최대 낙폭은"+answer);
		//현재 위치의 낙폭 (0,5의 낙폭?) 
		System.out.println("(0,5)의 낙폭은"+fallvalue(0,5));

	}
	private static int fallvalue(int x, int y) {
		int count =0;
		for(int i = x+1;i<9;++i) {
			if(arr[i][y] == 0) {
				count++;
			}
		}
		return count;
	}
}
```

