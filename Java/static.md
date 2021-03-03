### static 변수, 메서드
* ###### 클래스 소속 변수 "해당 변수를 모든 인스턴스에서 공유한다."
#####사용이유
 ###### 1. 인스턴스마다 변하지 않는 값이 필요한 경우.   
 ######  static 변수는 처음 프로그램이 로드될 때 데이터 영역 메모리에 생성됨.   
 ######  인스턴스의 생성과 상관없이 사용할 수 있으므로 클래스 이름으로 참조. 그래서 클래스 변수, 정적 변수라고도 함. 
 ###### 2. 인스턴스를 생성할 필요가 없는 값을 class에 저장하고 싶은 경우.
 ###### 3. 값의 변경사항을 모든 인스턴스가 공유해야하는 경우.   
 
 
**static변수를 이용한 학생 id값 부여하기 **   


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

**static변수는 객체 생성과 상관없기 때문에 객체 생성시 나오는 참조변수가 아니라 클래스 이름으로 접근 **   
   
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

but, 
//이 경우. 메인 메소드에서 
System.out.println(Student.serialNum++); //해버리면 원하는 기준값 적용이 안됨. 
//그래서 static은 private으로 설정하는 게 좋음. 
 public class Student {
  //public static int serialNum =1000;
  private static int serialNum =1000;
```
