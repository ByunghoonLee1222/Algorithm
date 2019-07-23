# Search(검색)

### 1. 순차 검색(sequential search)

* 일렬로 되어 있는 자료를 **순서대로 검색**하는 방법
* 대상의 수가 많은 경우 수행시간이 길어 비효율적

### 2. 이진 검색(binary search)

* 자료의 가운데에 있는 키 값과 비교하여 다음 검색의 위치를 결정하고 검색을 계속 진행

* 검색 범위를 반으로 줄여가면서 빠르게 검색을 수행

* ***자료가 정렬된 상태여야 한다***

  ```java
      private static int BinarySearch(int arr[],int searchnum) {
  	    int low = 0;
  	    int high = arr.length - 1;
  	   
  	    while(low <= high) {
  	        mid = (low + high) / 2;
  	        if (arr[mid] == searchnum) {
  	        	return mid;
  	        	}
  	        else if (arr[mid] > searchnum) { high = mid - 1;}
  	        else { low = mid + 1;}
  	    }
  	    mid = -1;
  	    return mid;
      }
  ```

  

### 3. 해쉬(hash)