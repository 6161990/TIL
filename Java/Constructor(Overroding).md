### :pushpin: 생성자 Constructor
* ##### 일반적으로 어디서든 클래스에 대한 객체 생성이 가능하도록 'public'으로 지정.
* ##### 객체를 생성할 때 new 키워드와 함께 노출 (객체 생성 외에는 호출할 수 없음)
* ##### 인스턴스를 초기화 하는 코드가 구현됨 (주로 멤버 변수 초기화)
* ##### 반환 값이 없음(초기화를 목적으로 하기 때문에), 상속되지 않음.
* ##### 생성자는 클래스 이름과 동일.   
   #
   #### :round_pushpin: 기본생성자(default constructor)
   ##### 해당 클래스를 new할 때 사용할 생성자를 뜻함. 
   ##### 기본 생성자의 멤버변수는 생성자가 힙 메모리에 할당이 될 때, JVM이 기본값으로 기본 생성자의 멤버변수를 초기화함.
   ##### 하나의 클래스에는 반드시 하나 이상의 생성자가 존재해야함.    
   ##### 프로그래머가 생성자를 구현하지 않으면 컴파일러가 생성자 코드를 넣어줌. => 기본 생성자   
   ##### 기본 생성자는 매개 변수가 없고, 구현부가 없음   
   
 
##### 기본 생성자
```java
public class Student {
  public int studentID;
  public String studentName;
  public String address;
  
  public Student(){}
}
```
   #
##### 클래스에 다른 생성자가 있는 경우 디폴트 생성자는 제공되지 않음
```java
public class Student {
  public int studentID;          // 여기 변수들은 인스턴스 생성시, 힙 메모리에 할당할 때 자동 초기화된다
  public String studentName;     // 보통 int = 0 , String = null 로.
  public String address;         // 전달받은 값이 있다면 그 값으로. 
  
  // public Student(){}
  
  public Student(int id, String name){
   studentID = id;
   studentName = name;
  }
}
```
   #
##### 다른 생성자를 만들경우 main에서의 오류
```java
public class StudentTest {
  public static void main(String[] args) {
   Student studentLee = new Student(); // 오류지점
   studentLee.studentName = "Jenny";
   studnetLee.address = "한남동";
  }
}
```
   #
##### 구현할 때 반드시 필요한 메서드가 필요한 경우("이름은 반드시 매번 구현을 할거야")
```java
public class Student {
  public int studentID;
  public String studentName;
  public String address;
  
  public Student(String name){
   studentName = name;
  }
  
  public static void main(String[] args) {
   Student studentLee = new Student(Jenny); 
 //studentLee.studentName = "Jenny"; 필요없음. 필수 메소드로 구현해놓았기때문.
   studnetLee.address = "한남동";
  }
}
```
    
       
  -----------------------------------------
### :pushpin: 생성자 오버로딩 Constructor Overroding
#### 클래스에 대한 객체를 new 생성할 때, 초기값을 주는 방법을 다양화시키고 싶을 때 사용한다.
#### 오버로딩의 목적 : 다양한 값의 처리방식을 하나의 이름으로 다루고자 할 때.
* ###### 생성자를 두 개 이상 구현하는 경우
* ###### 기본 생성자, 매개변수 있는 생성자 중복일 때 Overriding 한것임.
  ###### => 매개변수가 반드시 달라야한다. 매개변수의 갯수, 자료형의 순서에 따라 여러개의 생성자를 만들 수있다.
* ###### 사용하는 코드에서 여러 생성자 중 선택하여 사용할 수 있음.
* ###### private 변수도 생성자를 이용하여 초기화를 할 수도 있음(객체 초기화 작업을 할 때 생성자를 가져다 쓰기도 함).

##### 생성자 오버로딩 Constructor Overroding
```java
public class Student {

  public int studentID;
  public String studentName;
  public String address;
  
  public Student(String name){
     studentName = name;
  }
  
  public Student(int id, String name, String address){
     studentID = id;
     studentName = name;
     this.address = address;
  }
  
  public void showStudentInfo(){
     System.out.println(studentName+ "," +address);
  }
  
  public String getStudentName(){
      return studentName;
  }
  
  public static void main(String[] args) {
  
      Student studentKim = new Student("Jenny"); 
    //studentKim.studentName = "Jenny"; 필수메소드로 구현
      studentKim.address = "한남동";
      
      studentKim.showStudentInfo();
      
      
      Student studentBlack = new Student(100,"블랙핑크","합정동"); 
    //studentBlack.studentName = "블랙핑크";  필수메소드로 구현
    //studentBlack.address = "합정동"; 필수메소드로 구현
      
     studentBlack.showStudentInfo();
      
  }
}
```







