# Algorithm

### Java Preview _day 01

> ***Data Type***

* **Primitive Type**
  * 숫자형
    1. 정수형 : *byte(1), short(2), int(4), long(8)*
    2. 실수형 : *float(4), double(8)*
  * 문자형 : *char(2)*
  * 논리형 : *boolean(1 bit)*
* **Reference Type(non-Primitive)**
  * 4 byte

> ***형변환***  "byte<short, char<int<long<float<double"

* **묵시적 형변환**
  * up casting - 자동으로 수행됨

* **명시적 형변환(직접 형변환 명시)**
  * down casting -  형변환 연산자 사용



> ***Switch***

* switch(표현식) - byte, short, char, int, (String)

>***for***

* 반복문, 횟수를 알때

> ***Enhanced For***

* for( int a : 배열(Iterable)){ }
* for(int []a : arr) { }

> ***while***

* 반복, 횟수를 모를때

> ***break, continue***

* A: for(; ;){ }
  * break A;

#### Array (동형집합, 객체)

> 1. 동일한 타입을 집합으로 관리하기 위해, 한꺼번에 보내주고 받는다.
> 2. 각각의 인덱스를 조정,활용하기 위해

* **Primitive Type Array**

  * Datatype []arr = new Datatype[크기];

  * ``` javascript
    int [] arr = new int[3]; //default 초기화 후 Heap에 생성
    ```

* **Reference Type Array**

  * 2차원 이상의 배열

  * ```  java
    int [][]arr = new int [5][3]; // object 6개 생성
    ```

  * arr[0] = new int [2];

> ***Reference 는 address가 아니다.***
>
> ***Array default - 0, 0.0, False, ' '***



