### :pushpin: static 변수
* ###### 참고 : [객제 지향 언어 OOP](https://github.com/6161990/TIL/blob/main/Java/Object-Oriented%20Programming(OOP).md), [객제 지향 언어의 메모리 구조와 특징](https://github.com/6161990/TIL/blob/main/Java/OOP%20Memory.md)
* #### 클래스 소속 변수 "해당 변수를 모든 인스턴스에서 공유한다."

<br>

#### :round_pushpin: 사용이유   
1. #####  인스턴스마다 변하지 않는 값이 필요한 경우.   
	#####  static 변수는 처음 프로그램이 로드될 때 데이터 영역 메모리에 생성됨.   
	#####  인스턴스의 생성과 상관없이 사용할 수 있으므로 클래스 이름으로 참조. 그래서 클래스 변수, 정적 변수라고도 함. 
2. #####  인스턴스를 생성할 필요가 없는 값을 class에 저장하고 싶은 경우.
3. #####  값의 변경사항을 모든 인스턴스가 공유해야하는 경우.      

   <br>
   
#### static변수를 이용한 학생 id값 부여하기   


```java
public class Student {
	public static int serialNum =1000; // 1000을 기준으로 
	private int studentID;
	public String studentName;
	public String address;
  
  public Student(String name){
	studentName = name;
	serialNum++;           // 한번 생성자가 생성될 때마다 기준치에서 +1 하기로 설정.
	studentID = serialNum; // 그 값을 id로. 
  }
  
  public Student(int id, String name){
  	studentID= id;
	studentName =name;
	address = "주소 없음";
	serialNum++;             // 한번 생성된 생성자에서 +1
	studentID = serialNum;  // 그 값을 id로. 
  }
  public int getStudentID(){
    return studentID;
  }  
}
```
```java
public class  StudentTest {

	public static void main(String[] args) {
		Student studentLee = new  Student("Lee"); // 생성자 생성 할 때마다 static을 이용해 그 기준치에서 +1 (1001) 
		System.out.println(studentLee.serialNum);
		
		Student studentYun = new  Student(25,"Yun");// 두 번째 생성자 생성, 기준치에서 +2 (1002)
		
		Student studentKim = new  Student(20,"Kim");// 세 번째 생성자 생성, 기준치에서 +3 (1003)
		System.out.println(studentKim.serialNum);
		
		System.out.println(studentLee.getStudentID()); // id = 1001
		System.out.println(studentYun.getStudentID()); // id = 1002
		System.out.println(studentKim.getStudentID()); // id = 1003
  }
}   
```     
<br>

#### static변수는 객체 생성과 상관없기 때문에 객체 생성시 나오는 참조변수가 아니라 ***클래스 이름으로 접근***
   
```java
public class  StudentTest {

	public static void main(String[] args) {
		Student studentLee = new  Student("Lee"); 
		System.out.println(Student.serialNum); // 참조변수가 아닌, 클래스 이름 Student로 접근 Student.serialNum;
		
		Student studentYun = new  Student(25,"Yun");
		
		Student studentKim = new  Student(20,"Kim");
		System.out.println(Student.serialNum); // 참조변수가 아닌, 클래스 이름 Student로 접근 Student.serialNum;
		
		System.out.println(studentLee.getStudentID()); // id = 1001
		System.out.println(studentYun.getStudentID()); // id = 1002
		System.out.println(studentKim.getStudentID()); // id = 1003
  }
}
```    
 
##### but, 이 경우. 메인 메소드에서 
##### System.out.println(Student.serialNum++); 해버리면 원하는 기준값 적용이 안됨. 
##### :round_pushpin: 그래서 static은 private으로 설정하는 게 좋음. 
	```java
 	public class Student {
  	//public static int serialNum =1000;
  	private static int serialNum =1000;
 	}
	``` 

<br>
   
#### static변수를 private으로 설정했을 때 메인메소드에서 쓸 수 있도록 get,set설정(static 메소드)

```java
public class Student {
  public static int serialNum =1000; // 1000을 기준으로 
  private int studentID;
  public String studentName;
  public String address;
	
	//생략 ..

public static int getSerialNum() {
	return serialNum;
}
public static void setSerialNum(int serialNum) {
	Static.serialNum = serialNum;
}
```   
 <br>
 
### :pushpin: method 메서드 
#### 작업을 수행하기 위한 명령문의 집합
* ##### 수학의 함수와 비슷하여 호출을 통해 사용한다. 전달 값이 없는 상태로 호출을 하거나, 어떤 값을 전달하여 호출을 하면, 
* ##### 함수 내에 작성된 연산을 수행하거나 수행 후 결과값을 반환하는 것을 말한다. 즉, 클래스의 소속된 함수를 ***메소드***라한다.

<br>

#### :round_pushpin: 메소드 표현식
```java
[접근제한자] [예약어] 반환명 메소드명 {
     실행내용작성;
}
```
##### 일반적으로 캡슐화된 객체지향일때는 메소드를 public 형으로 만들어서, 외부에서 메소드를 사용하도록 하고 
##### 메소드가 접근 못하는, private된 필드의 값을 처리하는 구조로 되어있는 것이 메소드 

<br>

#### :triangular_flag_on_post: 메소드 예약어
* ##### static : static 영역에 할당하여 객체 없이 사용함
* ##### final : 종단의 의미, 상속시 오버라이딩 불가능
* ##### abstract : 미완성된, 상속하여 오버라이딩으로 완성시켜 사용해야함.
 	#####	   메소드 내용(body)이 없으며, 클래스에도 abstract명시해야한다. 
* ##### syncronized : 동기화처리, 공유 자원에 한 개의 쓰레드만 접근가능함
* ##### static final : static , final 의미를 둘 다 가진다. => static 메모리에, 상속 할 수 없게.

<br>

#### :triangular_flag_on_post: return
##### STACK 메모리 안에서 호출되면 들어와(push) 자신을 호출한 메소드에게 return 값을 주고 메모리공간을 나간다(pop)
##### => 해당 메소드를 종료하고, 자신을 호출한 메소드로 돌아가는 예약어. 
##### => 반환값(리턴값)을 가지고 자신을 호출한 메소드로 돌아갈 수 있다. 

<br>

#### :round_pushpin: static 메서드
* #### static 변수를 위한 기능을 제공하는 static 메서드 
* #### static 메서드에서는 인스턴스 변수를 사용할 필요 없음 
	* #####  static은 인스턴스 생성과 상관 없이 사용되고, 인스턴스는 new 되어야 생성되기 때문에 static메서드 안에서 인스턴스 변수 사용불가
	* #####  but! 일반 메소드 안에서 static 변수 사용할 수 있음. static 변수는 그 전에 생성되기 때문에 (로드될 때)
* #### 클래스 이름으로 참조하여 사용하는 메서드 (클래스 메서드, 정적 메서드라고도 함)

<br>

#### :round_pushpin: setter와 getter 메소드 
* ##### setter 필드에 변경할 값을 전달 받아서 필드값을 변경하는 메소드 , 필드 값 변경이 목적이다.
######   this ? 매개변수를 가지는 생성자에서 매개변수명이 필드명과 같을 경우,
######  매개변수의 변수명이 우선하기 때문에 this객체를 활용해서 대입되는 변수가 필드라는 것을 구분해준다.
```java
접근제한자 void set 필드명 (자료형 변수) {
	(this.)필드명 = 자료형 변수.
}
```
#
* ##### getter 필드에 기록된 값을 읽어서 요구하는 쪽으로 읽은 값을 넘기는 메소드 표현식
```java
접근제한자 반환형 get필드명() {
	return 필드명;
}
```
