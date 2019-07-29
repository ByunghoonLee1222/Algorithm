# String

* String s1 ="abc";
* String s2 = new String("abc");
* String s3 = "abc";
  * s1==s2  false (S2 -> Heap에 레퍼런스 저장)
  * s1==s3  true (literal pool 사용 "abc"레퍼런스 동일)



* 스트링 생성자에 char[] , byte[] 을 String 으로 만들어주는 메서드 존재
* 스트링 값 비교 => s1.equals(s2)

Stringbuffer => String 조작 가능