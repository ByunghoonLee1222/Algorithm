# 비트 연산자

- ​     1  1  0  0			    1  0  1  0
- **&**  1  0  1  0		    **|**  0  1  1  0                 **~ **1   0

------

​            1  0  0  0			    1  1  1  0                     0  1

- **원하는 비트열을 만들기 위해 사용**

  1. <<    => 0으로 오른쪽 영역
  2. .>>   => 부호bit로 왼쪽 영역 채움
  3. .>>> => 0으로 왼쪽 영역 채운다 (음수 유지 x)

- ```java
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

#### 부동소수

------

- **IEEE754**
  - **single** (32bit)
    - 부호비트 1bit , 지수비트 8bit , 가수부비트 23bit  => 32bit
    - 단정도 실수
  - **double**(64bit)
    - 부호비트 1bit , 지수비트 11bit , 가수부비트 52bit  => 64bit
    - 배정도 실수(정확도가 더 높다)
- **정규화**
  - 소수점의 위치 고정
  - 실수의 대소비교에 용이 
  - 소수점 앞에 0이아닌 수 한개
  - 하나의 기준점을 정해 양수인지 음수인지 판단









- **10 !** 이상은 완전탐색 시 시간 초과 고려