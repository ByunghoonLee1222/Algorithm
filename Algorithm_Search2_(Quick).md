# Quick Sort

* 주어진 배열을 두 개로 분할하고, 각각을 정렬한다
* 기준 아이템(pivot item)중심으로, 이보다 작은 것은 왼편, 큰 것은 오른편에 위치시킨다
  * L => 피봇보다 같거나 큰것을 찾아 우측으로 이동
  * R => 피봇보다 작은것을 찾아 좌측으로 이동
  * L, R이 교차하면 R과 피봇을 교환 
  * 피봇을 교환하면 자리 고정
  * 반복 하여 더이상 나눌수 없을때 까지 진행한다
  * *피봇은 보통 최좌측이나 최우측부터 시작한다*

```java
	public static int fixPivot(int[] arr, int begin, int end) {
		int tmp;
		int pivot = begin;
		int left = begin + 1;
		int right = end;
		do {
			// left : 피봇보다 같거나 큰 값 찾아 움직임(작으면 계속 오른쪽으로..)
			while (left < end && arr[left] < arr[pivot]) left++;
			// right : 피봇보다 작은값 찾아 움직임(같거나 크면 계속 왼쪽으로..)
			while (right > begin && arr[right] >= arr[pivot]) right--;
			if (left < right) {
				tmp = arr[right];
				arr[right] = arr[left];
				arr[left] = tmp;
			}
		} while (left < right);

		tmp = arr[pivot];
		arr[pivot] = arr[right];
		arr[right] = tmp;
		return right;

	}

	public static void quicksort(int[] arr, int begin, int end) {

		if (begin < end) { // 집합의 크기(원소개수)가 2이상일 경우만 정렬 시도
			// 피봇위치 확정
			int p = fixPivot(arr, begin, end);
			// 피봇왼쪽집합 정렬
			quicksort(arr, begin, p - 1);
			// 피봇오른쪽 집합 정렬
			quicksort(arr, p + 1, end);
		}
	}

	public static void main(String[] args) {
		int[] arr = { 69, 10, 30, 2, 16, 8, 31, 22 };
		quicksort(arr, 0, 7);
		System.out.println(Arrays.toString(arr));
	}
```

