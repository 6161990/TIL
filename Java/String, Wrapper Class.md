## :pushpin: String Class
### String Class 선언하기
  ##### 1. 인스턴스로 생성 (힙 메모리에 저장)
            String str1 = new String("abc");
  ##### 2. 직접 가져다 쓸 때 (상수풀에 있는 문자열을 가리킴)
            String str2 = "abc"
```java
public class StringTest {

	public static void main(String[] args) {

		String str1 = new String("abc");
		String str2 = new String("abc");
		
		System.out.println(str1 == str2);     //false
		
		String str3 = "abc";
		String str4 = "abc";
		
		System.out.println(str3 == str4);   //true
	}

}
```

<br>


##### :round_pushpin: String은 immutable
* ##### 한번 선언되거나 생성된 문자열을 변경할 수 없음 
* ##### String 클래스의 concat()메서드 혹은 "+"를 이용하여 String을 연결하는 경우 문자열은 새로 생성됨.
* ##### concat : 괄호 안 문자열을 전부 결합해서 반환하는 함수
* ##### 합쳐진 String hashCode()확인할 수 없는 이유 : overwrite, 어떤 장소에 기록되어 있는 정보 위에 중복 기록 함으로써
                                              원래의 정보가 소실되어(파괴되어)버리는 기록방법.
```java
public class StringTest2 {

	public static void main(String[] args) {

		String java = new String("java");
		String android = new String("android");
		System.out.println(System.identityHashCode(java));    //'366712642'
		
		java = java.concat(android);        //concat 메서드 
		
		System.out.println(java);           // 'javaandroid'
		System.out.println(System.identityHashCode(java));  //'1829164700'
	}
}
```

##### => java가 합쳐지기 전과 후의 hashCode가 같지 않음. 연결되면 새로운 메모리 값을 가져가기때문.

<br>

#### :round_pushpin: String Builder와 String Buffer
* ##### String immutable이기 때문에 String Builder,Buffer를 씀
* ##### 메모리를 계속 쓰는 게 아니라 처음 것에 연결해서 씀.
* ##### 가변적인 char[] 배열을 멤버변수라 가지고 있는 클래스
* ##### 문자열을 더하거나 빼거나 변경하거나 연결하는 경우 사용하면 편리한 클래스
* ##### String Buffer는 멀티 쓰레드프로그래밍에서 동기화(Synchronization)이 보장됨.
  ##### 단일 쓰레드 프로그래밍에서는 String Builder를 사용하는 것이 더 좋음.
  ##### toString()메서드로 String변환.
```java
public class StringBuilderTest {

	public static void main(String[] args) {
		// 
		String java = new String("java");
		String android = new String("android");
		
		StringBuilder buffer = new StringBuilder(java);
		System.out.println(System.identityHashCode(buffer));    //'366712642'
		buffer.append("android");         //append : 덧붙이다. 첨부하다.
		System.out.println(System.identityHashCode(buffer));   //'366712642'
		
		java = buffer.toString();
	}
}
```

<br>

### :round_pushpin: Wrapper Class
##### boolean -> Boolean
##### byte -> Byte
##### char -> Character
##### short -> Short
##### int -> Integer
##### long -> Long
##### float -> Float
##### double -> Double
