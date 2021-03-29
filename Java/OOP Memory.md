## :pushpin: 객체 지향 언어의 메모리 구조와 특징 OOP Memory 
* ###### 참고 : [객제 지향 언어 OOP](https://github.com/6161990/TIL/blob/main/Java/Object-Oriented%20Programming(OOP).md)
### :round_pushpin: 정적 메모리와 동적 메모리
* ##### 정적 메모리 : 이미 메모리 공간의 크기가 정해져있는 고정적 메모리 영역이다.
    * #####              프로그램 구동 내내 사용할 수 있어서 하나의 정보를 여러 대상이 공유할 목적일 때 사용한다.
    * #####              static이 여기에 해당된다. 
* ##### 동적 메모리 : 유동적으로 메모리 영역에 변화를 줄 수 있으며, 프로그램 실행시 실행되는 메모리 공간이다.
    * #####               HEAP 메모리 쪽에 변수 방을 만들더라도 그 공간은 변수명을 사용하지 못하는 공간이다.
    * #####                즉, 이름으로 접급하는 것이 아니라 그 변수방이 있는 주소로만 접근할 수 있다. 
    * #####                따로 삭제에 대한 코드가 없으며 garbage collection에서 관리한다.
    * #####                HEAP, STACK 메모리가 여기에 해당한다.
  
  
  <br>
  <br>
  
### :round_pushpin: static vs. HEAP vs. STACK

<img width="300" height="400" src="https://user-images.githubusercontent.com/74708028/112102497-b37fba80-8beb-11eb-956e-e0e677971007.jpg"/>

##### 1. static : main()이 start 될 때 static 예약어로 설정된 클래스 변수, 클래스 메소드가 자동 할당되는 공간.
#####            프로그램이 종료될 때 자동소멸되며, 딱 한번에 한 개만 할당되므로 프로그램 구동되는 동안 공유할 대상에 적용되어 이용하는 메모리
#
##### 2. HEAP : new 연산자에 의해 동적 할당하고 생성된 주소(위치정보)로 접근할 수 있는 공간
#####            자바에서는 객체(인스턴스), 배열 공간은 모두 이 메모리 영역에 할당하도록 정해져있음.
#
##### 3. STACK : non_static 메소드 실행시 메소드 호출 스택(method call stack)에 메소드 영역이 할당되며, 
#####            해당 메소드의 지역변수와 매개변수(parameter)가 영역 안에 할당됨. 메소드 리턴(종료)시 자동 소멸됨.

<br>

### :round_pushpin: 객체 할당 메모리 구조 

<img width="600" height="220" src="https://user-images.githubusercontent.com/74708028/112074753-53245500-8bba-11eb-88f8-5d4141f8ee9b.jpg"/>

* ##### 클래스에 선언된 필드들이 선언 순서대로 힙 영역에 배열처럼 연속 할당되며, 생성된 시작 위치(주소)가 스택의 레퍼런스에 저장된다. 

<br>

### :round_pushpin: 메모리 할당에 따른 변수의 종류
 - ##### 지역변수 Local Variable (로컬변수)
   ##### 메소드 실행시 스택 메모리 영역에 할당되며, 메소드 영역 내에서만 사용가능하며, 메소드 종료시 자동 소멸되는 변수
 - ##### 클래스변수 class field (static변수)
   ##### 프로그램 실행시 정적(스태틱) 메모리에 자동 할당되며, 준비된 기본값으로 초기화되고, 프로그램 실행시 소멸되는 필드
   ##### static 변수는 프로그램이 메모리에 있는 동안 계속 그 영역을 차지하므로 너무 큰 메모리를 할당하는 것은 좋지 않다. 
 - ##### 인스턴스 변수 instance field  (멤버변수)
   ##### new에 의해 힙 메모리에 할당되며, 객체 안에 할당되는 멤버변수를 말함. 가비지 콜렉터에 의해 객체 소멸시 함께 삭제되는 필드
   ##### 클래스 내부의여러 메서드에서 사용하는 변수는 멤버변수로 선언하는 것이 좋다. 
   ##### 하지만, 멤버변수가 너무 많으면 인스턴스 생성시 쓸데없는 메모리가 할당된다.
 
<br>

#### :triangular_flag_on_post: 기본형 매개변수와 참조형 매개변수
* ##### 기본형 매개변수 : 값을 읽기만 할 수 있다.

```java
public class ParameterTest {

	public static void main(String[] args) {
		Data d = new Data();
		d.x = 10;
		System.out.println("main:x=" + d.x);
		change(d.x);
		System.out.println("After change(d.x)");
		System.out.println("main:x=" + d.x);
	}
	
	
	//기본형 매개변수 값을 읽기만 할 수 있다. 
	public static void change(int x) {
		x = 1000;
		System.out.println("change(): x="+x);
	}

}
```

* ##### 참조형 매개변수 : 값을 읽고 쓸 수 있다. 

```java
public class ParameterTest2 {

	public static void main(String[] args) {
		Data d = new Data();
		d.x=10;
		System.out.println("main():x"+d.x);
		change(d);
		System.out.println("After change(d.x)");
		System.out.println("main():x="+d.x);
	}

	//참조형 매개변수 변수의 값을 읽고 변경할 수 있다. 
	public static void change(Data d) {
		d.x=1000;
		System.out.println("change():x="+d.x);
	}
}
```

<br>

### :round_pushpin: static 예약어
* ##### 필드와 메소드에 사용할 수 있으며, 같은 타입의 여러 객체가 공유할 목적인 대상에 적용하며, 프로그램 start시에 정적 메모리 영역에 자동 할당된다. 
* ##### {} : 클래스의 멤버 변수를 초기화 시키는 블록.
   * ###### static 필드 초기화, 프로그램 시작시 초기화한다
   * ###### 인스턴스 블록 : 인스턴스변수 초기화, 객체 생성시마다 초기화
```java
접근 제한자 class 클래스명 { 
  접근제한자 static 자료형 필드명; //static
  접근제한자 자료형 필드명; //인스턴스 
  static {필드 : 초기값}; //static
  {필드 : 초기값}  //인스턴스
}
```
* ##### static과 HEAP의 기본값
    ##### JVM에 의해 static메모리와 heap 메모리 영역에 할당되는 필드에 초기값 선언이 없을 시에는 준비된 기본값으로 자동 초기화됨.
     - boolean : false
     - char : '\u0000'
     - byte, short, int, long : 0
     - float, double : 0.0
     - reference : null

---------------------------------------------------------------

<br>

### :pushpin: 기본 자료형 배열[ ], 2차원 배열 메모리구조

<img width="500" height="250" src="https://user-images.githubusercontent.com/74708028/112102753-14a78e00-8bec-11eb-8198-42f2c77c9981.jpg"/>

<img width="500" height="290" src="https://user-images.githubusercontent.com/74708028/112102757-16715180-8bec-11eb-9af5-91ab0a308ce0.jpg"/>

* ##### 배열[][] 의 차원 갯수는 주소를 몇번 참조하느냐!! 다. 
* ##### 2차원 배열은 시작되는 주소값을 0x678(0x698) 레퍼런스에 기록하되, 각 1차원 배열의 주소들을 다시 배열(0x123)로 묶어주는 형태다.
    ##### => 2차원 배열은 레퍼런스(주소) 변수에 대한 배열이다. 
* ##### 변수 arr은 레퍼런스 배열의 시작 위치값을 가질 위치 참조 변수다.
     * ##### 참조 변수 : 주소(위치 정보)를 가지고 힙 영역에 대상 안의 데이터에 접근한다. 
