# Merge Sort(병합 정렬)

* 집합의 크기 >=2

* 쪼갠다(반으로)

* 합치면서 정렬

  ```java
  	public static void mergeSort(int[] list, int start, int end) {
  		// 현집합을 반으로 나누어 정렬
  		if (start == end)
  			return;
  
  		int half = (start + end) / 2;
  		// 왼쪽집합 정렬해오기
  		mergeSort(list, start, half);
  		// 오른쪽집합 정렬해오기
  		mergeSort(list, half + 1, end);
  		// 정렬된 두 집합 이용하여 합치기
  		merge(list, start, half, end);
  	}
  
  	private static void merge(int[] list, int start, int half, int end) {
  		int newArr[] = new int[end - start + 1];
  		int left = start, right = half + 1;
  		int i = 0; // newArr을 채울 index
  
  		// 순차적으로 비교해서 새 배열에 대입
  		do {
  			if (list[left] < list[right]) {
  				newArr[i++] = list[left++];
  			} else {
  				newArr[i++] = list[right++];
  			}
  		} while (left <= half && right <= end);
  
  		// 왼쪽 집합이 남은 경우
  		while (left <= half) {
  			newArr[i++] = list[left++];
  		}
  		// 오른쪽 집합이 남은 경우
  		while (right <= end) {
  			newArr[i++] = list[right++];
  		}
  
  		System.arraycopy(newArr, 0, list, start, newArr.length);
  	}
  
  	public static void main(String[] args) {
  		int list[] = { 2, 3, 10, 4, 13, 22, 10, 9 };
  		System.out.println(Arrays.toString(list));
  		mergeSort(list, 0, list.length - 1);
  		System.out.println(Arrays.toString(list));
  	}
  ```

  