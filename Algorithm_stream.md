# Algorithm

* comparable - 원소들이 구현 (원소 스스로들이 비교)

* comporator - 비교판단해주는 비교자(별도의 비교자 존재)

* Arrays.fill 

  ```java
  Arrays.fill(arr,0); //arr배열을 0으로 채움
  ```

  

### Stream

> 입력하는 데이터가 많아지면 Scanner 기능 떨어진다.
>
> 

1. **input stream**
   * reader (char 단위 - 2byte)
   * input stream (system.in - byte 단위)
2. **ouput stream**
   * output stream
   * writer

### Scanner

* **nextInt, nextDouble....**(delimiter 자동제거하고 읽어들인다. 개행문자 남음)
* **nextLine**(개행문자를 만날때까지 읽는다. 공백을 읽을 수 있다.)
* **next**(이전 개행 무시. delimiter 전까지 문자를 읽는다. )



### Enhanced for

* 배열의값 읽기만 가능. 쓰기 불가
* 읽어와서 복사본을 수정하는 것은 가능



### Time Complexity(시간 복잡도)

* 상수항, 계수 제거 (ex. O(3n+2) = O(n) )
* O(2n^2+10n+100) = O(n^2)
* O(4) = O(1)