## :pushpin: Object Class 
 ### 모든 클래스의 최상위 클래스, 객체지향에서의 object처럼 추상적 의미 아님. 
 * #### java.lang.Object 클래스. import하지 않아도 됨.
 * #### 모든 클래스는 사실 Object 클래스에서 암시적으로 상속 받고있음.  

            class A  => 실상은 class A (extends Object) 
 * #### 모든 클래스는 Object 클래스의 메서드를 사용할 수 있음.
 * #### 모든 클래스는 Object 클래스의 일부 메서드를 재정의하여 사용할 수 있음(final로 선언된 메서드 제외하고!)

<br>

#### :round_pushpin: toString()메서드
 
        원형 : getClass().getName().+'@'+Integer.toHexString(hashCode())
 * ##### 어떠한 객체를 문자화시켜주는 메소드       
 * ##### 객체의 정보를 String으로 바꾸어 사용할 때 유용함.
 * ##### 자바 클래스 중에는 이미 정의된 클래스가 많음. 많은 클래스에서 재정의하여 사용
   ##### ex)String, Integer,Calender 등

<br>

#### :round_pushpin: String 참조 자료형의 참조변수 출력하기
```java    
class Book {

	String title;
	String author;
	
	public Book(String title, String author) {
		this.title = title;
		this.author = author;
	}
}
public class ToStringTest{

	public static void main(String[] args) {				
		Book book = new Book("토지","박경리");	
		System.out.println(book);		// 출력 : 'chapter10.Book@54bedef2' 
							//  참조변수를 출력하면 인스턴스의 위치를 나타내는 참조 값이 나옴.
		String str = new String("토지");
		System.out.println(str);		// 출력 : '토지'  얘도 참조변수이긴 마찬가지
	}
}
 ```   
##### :triangular_flag_on_post: 근데 book과 str의 출력 값이 다른 이유?
#####    String 안에 toString이 들어가 있기 때문에, 자동 문자변환이 된다. 
#####    그래서 참조 변수 str에 str.toString메서드를 사용할 수 있게된다. Object의 toString을 재정의 한 것.
##### => book도 문자로 변환하려면, 다음과 같이 Object 클래스가 갖고있는 toString 메소드를 재정의하여 사용하면 된다.

<br>

#### :round_pushpin: 직접만든 참조 자료형의 참조변수 문자형으로 출력하기
```java    
class Book {

	String title;
	String author;
	
	public Book(String title, String author) {
		this.title = title;
		this.author = author;
	}
	
	@Override
	public String toString() {		// toString 메소드 재정의하여 this.title과 this.author 받기
		return author +","+title;
	}
}
public class ToStringTest{

	public static void main(String[] args) {				
		Book book = new Book("토지","박경리");	
		System.out.println(book);	// 출력 : "박경리,"토지"
		
		String str = new String("토지");
		System.out.println(str);	// 출력 : "토지"	
	}
}
 ``` 

<br>

#### :round_pushpin: equals()메서드
* ##### 두 객체의 동일함을 **논리적**으로 재정의 할 수 있음.
* ##### 원시데이터형 비교와 같이 단순비교는 연산자 '=='를 이용 (물리적동일함)
* ##### 물리적 동일함 : 같은 주소를 가지는 객체
* ##### 논리적 동일함 : 같은 학번의 학생, 같은 주문 번호의 주문
 
 ##### => 물리적으로 다른 메모리에 위치한 객체라도 논리적으로 동일함을 구현하기 위해 사용하는 메서드
        Student studentKim = new Student("김우빈");
        Student studentKim2 = studentKim2;
        Student studentKimWooBin = new Student(100,"김우빈");
        
        => studentKim , studentKim2 는 같은 힙 메모리에 저장되지만
           studentKimWooBin은 다른 힙메모리에 저장됨. 
           But, 물리적으로는 다른 위치에 있지만 논리적으로는 같은 학생임.
                 equals로 구현.

<br>

#### :round_pushpin: 이미 equals가 재정의되어있는 String 참조자료형 클래스
##### => String 안에 equals를 재정의함. 클래스 String 이 equals를 오버라이딩해서 재정의를 하게 되면(각각의 클래스에 맞게 재정의하게되면),
#####    String 같은 경우는 "문자열이 같으면 같은 놈이당!!" 라고 true를 반환하게 이미 해놓음. 사용자가 재정의할 필요 없음.
```java    
public class EqualsTest {

	public static void main(String[] args) {
		String str1 = new String("abc");
		String str2 = new String("abc");
		
		System.out.println(str1 == str2);
		System.out.println(str1.equals(str2));
	
	}
}
 ```   
 
 <br>
 
####:round_pushpin: equals재정의가 필요한 일반 참조자료형(Student) 클래스
```java    

class Student {
	int studentNumber;
	String studentName;
	
	public Student (int studentNumber, String studentName) {
		this.studentNumber = studentNumber;
		this.studentName = studentName;
	}
}
public class EqualsTest {

	public static void main(String[] args) {
		Student Kim = new Student(1004,"김순수");
		Student Kim2 = Kim;
		Student Soo = new Student(1004,"김순수");
		
		System.out.println(Kim == Soo);			//false : 물리적으로 동일하지 않음
		System.out.println(Kim == Kim2);		//true 	: 물리적으로 동일함.
		System.out.println(Kim.equals(Soo));		//false : 논리적으로 동일하지 않음 -> 실질적으로는 동일함. 
								//	  입증을 위해 equals재정의필요.
	}
}
 ``` 
 
 <br>
 
#### :round_pushpin: 일반 참조자료형(Student) 클래스에 equals재정의하기
```java    
class Student {
	int studentNumber;
	String studentName;
	
	public Student (int studentNumber, String studentName) {
		this.studentNumber = studentNumber;
		this.studentName = studentName;
	}
	
	@Override
	public boolean equals(Object obj) {     //여기서 obj는 넘어온 변수(Soo)
		if(obj instanceof Student) {	// A instanceof B : A가 정말 B 타입의 인스턴스 였느냐!
			Student std = (Student)obj;	// 그럼 obj의 다운캐스팅 형변환필요 
			return (this.studentNumber == std.studentNumber);  // => 기준점.equals(넘어온 애)
		}
		return false;
	}
}
public class EqualsTest {

	public static void main(String[] args) {
		Student Kim = new Student(1004,"김순수");
		Student Kim2 = Kim;
		Student Soo = new Student(1004,"김순수");
		
		System.out.println(Kim == Soo);			//false : 물리적으로 동일하지 않음
		System.out.println(Kim == Kim2);		//true 	: 물리적으로 동일함.
		System.out.println(Kim.equals(Soo));		//true : equals 재정의를 통해 논리적 동일함 입증.
	}
}
 ``` 


<br>

#### :round_pushpin: hashCode()메서드
 * ##### hashCode()메서드의 반환 값: 인스턴스가 저장된 가상머신의 주소를 10진수로 반환.  
 
  		System.out.println(Kim);      //chapter10.Student@54bedef2   : 패키지이름.인스턴스 메모리 주소
		
		System.out.println(Kim.hashCode());	//1421795058  : 인스턴스 메모리 주소를 10진수로 반환
		
 * ##### 두 개의 서로 다른 메모리에 위치한 인스턴스가 동일하다는 것은? 
   ##### => 논리적 동일 : equals의 반환값이 true
   ##### => 동일한 hashCode 값을 가짐 = hashCode()의 반환 값이 동일 (!!!실제 메모리 값이 같은 것은 아님!!!!)
   ##### => overriding 재정의를 통해 equals가 true일 때 hashCode도 같은 값이 반환될 수 있도록, 
   #####    일반적으로 equals 오버라이딩할 때 hashCode도 같이 오버라이딩한다.
```java    
class Student {

		//생략..
		
	@Override
	public boolean equals(Object obj) {     
		if(obj instanceof Student) {	
			Student std = (Student)obj;	
			return (this.studentNumber == std.studentNumber);  
		}
		return false;
	}
	
	@Override
	public int hashCode() {
		return studentNumber;		// 일반적으로 equals와 같이 오버라이딩 하는 경우가 많기 때문에,
						// 미리 설정해둔 equals의 멤버를 이용한다. 
	}
	
}
public class EqualsTest {

	public static void main(String[] args) {
		Integer i1 = new Integer(100);
		Integer i2 = new Integer(100);
		
		System.out.println(i1.equals(i2));			//'true'
		System.out.println(i1.hashCode());			//'100'
		System.out.println(i2.hashCode());			//'100'
		
		//진짜 hashCode 알 수 있는 방법 : identityHashCode()
		System.out.println(System.identityHashCode(i1));	//'804564176' 
		System.out.println(System.identityHashCode(i2));	//'1421795058'
	}
}
 ``` 

<br>

#### :round_pushpin: clone()메서드
 * ##### 객체의 복사본을 만듧.
 * ##### protected 속성을 가지고 있음.
 * ##### 기본 틀(prototype)으로 부터 같은 속성 값을 가진 객체의 복사본을 생성할 수 있음.
 * ##### 복제 가능한 인터페이스를 생성하고(java virtual machine에게 알려줘야하니까) 구현해주어야함. 
 * ##### 객체지향 프로그래밍의 정보은닉에 위배되는 가능성이 있으므로 복제할 객체는 clonealbe 인터페이스를 명시해야함.
```java    
class Book implements Cloneable{			// "복제할 수 있다" 달아주기 

	String title;
	String author;
	
	public Book(String title, String author) {
		this.title = title;
		this.author = author;
	}
	@Override
	public String toString() {
		return author +","+title;
	}
	@Override
	protected Object clone() throws CloneNotSupportedException {	
		return super.clone();
	}	
}
public class ToStringTest{

	public static void main(String[] args) throws CloneNotSupportedException {
		Book book = new Book("토지","박경리");
		System.out.println(book);		//'박경리', '토지' 
		
		Book book2 = (Book)book.clone(); //Object에서 Book으로 명시적 형변환필요. 
		System.out.println(book2);		//'박경리', '토지' 
	}
}
 ``` 


<br>

#### :round_pushpin: finalize()
* ##### 객체가 소멸될 때 garbage collector에서 호출하기로 한 메소드.
* ##### 사용가자 부르는 메서드아님. garbage collector가 수행함.
* ##### garbage collection : 인스턴스를 만들고 변수를 사용한 뒤, 더 이상 사용하지 않는다는 것을 인지해서 자동으로 쓰지않는 data를 삭제한다. 
```java    
class Book implements Cloneable{			

	String title;
	String author;
	
	public Book(String title, String author) {
		this.title = title;
		this.author = author;
	}
	@Override
	public String toString() {
		return author +","+title;
	}
	@Override
	protected Object clone() throws CloneNotSupportedException {	
		return super.clone();
	}
	@Override
	protected void finalize() throws Throwable {			//객체가 힙 메모리에서 해제될 때 자동으로 호출.
		// TODO Auto-generated method stub
		super.finalize();
	}
}
}
