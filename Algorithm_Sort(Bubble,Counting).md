# 정렬

### 버블 정렬(Bubble Sort)

* 첫 원소부터 인접한 언소끼리 계속 자리를 교환하면서 맨 마지막 자리까지 이동

* 한 단계가 끝나면 가장 큰 원소가 마지막 자리로 정렬된다.

* 시간 복잡도 O($n^2$)

  ```java
  		int bubble[] = {55,7,78,12,42};
  		int tmp = 0;
  		// for(int i = bubble.length -1; i>0; --i)
  		//		for(int j=0; j<i; ++j)
  		boolean isSwap = false;
  		for(int i=0;i<bubble.length;++i) {
  			isSwap = false;
  			for(int j=0;j<bubble.length-1-i;++j) {
  				if(bubble[j] > bubble[j+1]) {
  					tmp = bubble[j];
  					bubble[j] = bubble[j+1];
  					bubble[j+1]=tmp;
  					isSwap = true;// 스왑이 한번이라도 발생하면 true
  				}
  			}
  			if(!isSwap) break; //스왑이 한번도 일어나지 않으면 break
  		}
  ```



### 카운팅 정렬(Counting Sort)

* 항목들의 순서를 결정하기 위해 집합에 각 항목이 몇 개씩 있는지 세는 작업***(data 빈도수)***
* **정수**나 정수로 표현할 수 있는 자료에 대해서만 적용 가능
* max값이 크지 않을수록 유리
* 시간 복잡도 O(n+k)

단계

1. Counting(**data 빈도수**)
2. counts 배열 **누적 카운팅**으로 Update
3. 누적 counting을 활용해서 원소 자기자리 꽂아주기 

```java
	public static void main(String[] args) {
		int data[] = {0,4,1,3,1,2,4,1};
		//카운팅
		System.out.println(Arrays.toString(countingSort(data)));

	}
	private static int[] countingSort(int[] data) {
		//카운트 세기
		int counts[] = new int[5];
		
		for(int i =0;i<data.length;++i) {
			counts[data[i]]++;
		}
		//누적 카운팅
		for(int i =1;i<counts.length;++i) {
			counts[i] = counts[i-1]+counts[i];
		}
		System.out.println(Arrays.toString(counts));
		//누적 count 이용하여 각 원소 자기자리 꽂아주기
		int [] newArr = new int[data.length];
		
		for(int i =data.length-1;i>=0;--i) {
			newArr[counts[data[i]]-1]=data[i];
			counts[data[i]]--;
			//newArr[--counts[data[i]]]=data[i];
		}
		return newArr;
	}
```



### 지그재그 순회

```java
int i,j;
for(i=0;i<n-1;++i){
	for(j=0;j<m-1;++j){
		Array[i][j+(m-1-2*j)*(i%2)]; //i%2 짝수일때 무시, 홀수일때만 적용
	}
}
```



### 삽입 정렬(Insertion Sort)

```java
	public static void insertionSort(int list[]) {
		final int SIZE = list.length;
		for( int i = 1; i<SIZE; ++i) { // U집합
			int temp = list[i];
			for (int j = 0; j < i; j++) { // S 집합 j: 0~ i-1
				if(temp <list[j]) { // 삽입 위치
					for(int k = i-1; k>=j ;k--) {//S집합 끝부터 하나씩 삽입위치 원소까지 
                       							 // 뒤로 이동
						list[k+1]= list[k];
					}
					list[j]=temp;
					break;
				}
				
			}
		}
	}
```

