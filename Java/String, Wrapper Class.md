## :pushpin: String Class
* #### 객체 지향의 모든 클래스들은 반드시 new를 통해 해당 클래스에 대한 인스턴스를 heap 메모리에 생성한 후에 레퍼런스에 의해 참조되는 것이 원칙.
* #### But, String  클래스는 예외, 기본 자료형처럼 문자열을 바로 기록할 수 있음. JAVA가 그렇게 허락함.

<br>

### String Class 선언하기
  #### 1. 인스턴스로 생성 (힙 메모리에 저장)
            String str1 = new String("abc");
  #### 2. 직접 가져다 쓸 때 (상수풀에 있는 문자열을 가리킴)
            String str2 = "abc"
* #### 모든 문자열 값을 문자열 저장소에 저장
* #### 문자열 저장소는 중복저장되지 않기 때문에 필요시 그 저장 주소를 내어줌.
* #### String 인스턴스의 위치 정보가 레퍼런스 변수에 기록됨.(직접 가져다 쓸 때의 변수(값은 동일한)와 !== 하는 이유)
* #### 단, 직접 가져다 쓰는 문자열과의 HashCode는 서로 같다.
  #### Why?!!?
  #### 직접 가져다 쓸 때의 변수가 가지고 있는 주소가 나오지 않고 참조하는 문자열(인스턴스로 생성하는 경우의) 위치가 나와???
  #### :triangular_flag_on_post: => HashCode를 String 클래스에서 오버라이딩 했기 때문. 참조하는 문자열의 위치를 return 하도록 오버라이딩 해놓음.
  #### toString도 마찬가지 원리, 클래스 타입과 Hashode를 하나의 문자열로 합쳐서 return함.
  #### => String 레퍼런스를 toString 하게되면 String 클래스에서 toString 메서드를 오버라이딩 했기 때문에 참조하는 문자열 값이 return 되도록해놓았기 때문.
  #### => ***String 클래스에서 참조하는 문자열 메모리 할당구조***

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
  #####                                             원래의 정보가 소실되어(파괴되어)버리는 기록방법.
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
