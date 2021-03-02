### 생성자 Constructor
* ###### 객체를 생성할 때 new 키워드와 함께 노출 (객체 생성 외에는 호출할 수 없음)
* ###### 인스턴스를 초기화 하는 코드가 구현됨 (주로 멤버 변수 초기화)
* ###### 반환 값이 없음, 상속되지 않음.
* ###### 생성자는 클래스 이름과 동일.   
   
#### **기본생성자(default constructor)**
하나의 클래스에는 반드시 하나 이상의 생성자가 존재해야함.    
프로그래머가 생성자를 구현하지 않으면 컴파일러가 생성자 코드를 넣어줌. => 기본 생성자   
기본 생성자는 매개 변수가 없고, 구현부가 없음   
   
   
**기본 생성자**
```java
public class Student {
  public int studentID;
  public String studentName;
  public String address;
  
  public Student(){}
}
```

**클래스에 다른 생성자가 있는 경우 디폴트 생성자는 제공되지 않음**
```java
public class Student {
  public int studentID;
  public String studentName;
  public String address;
  
  // public Student(){}
  
  public Student(int id, String name){
   studentID = id;
   studentName = name;
  }
}
```
**다른 생성자를 만들경우 main에서의 오류**
```java
public class StudentTest {
  public static void main(String[] args) {
   Student studentLee = new Student(); // 오류지점
   studentLee.studentName = "Jenny";
   studnetLee.address = "한남동";
  }
}
```
**구현할 때 반드시 필요한 메서드가 필요한 경우("이름은 반드시 매번 구현을 할거야")**
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
    
       
       
------------------
### 생성자 오버로딩 Constructor Overroding
* ###### 생성자를 두 개 이상 구현하는 경우
* ###### 사용하는 코드에서 여러 생성자 중 선택하여 사용할 수 있음.
* ###### private 변수도 생성자를 이용하여 초기화를 할 수도 있음(객체 초기화 작업을 할 때 생성자를 가져다 쓰기도 함).

** 생성자 오버로딩 Constructor Overroding**
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







