### :pushpin: 참조자료형 reference data type
* #### 클래스형으로 변수를 선언함.
* #### 기본 자료형은 사용하는 메모리가 정해져 있지만, 참조자료형은 클래스에 따라 다름.

<br>
   
   #### :round_pushpin: 참조자료형 직접 만들어 사용하기
   ##### 학생클래스Student 에 있는 과목 이름, 과목 성적 속성을 과목 클래스Subject 로 분리하고   
   ##### Subject 참조 자료형 멤버변수를 Student에 정의하여 사용함.
   
<br>

#### 과목 클래스
```java
public class Subject {

  public int SubjectID;
  public String SubjectName;
  public int score;
  
}
```
<br>

#### 학생클래스
```java
public class Student {

   public int studentID;
   public String studentName;
 
   Subject korea;
   Subject math;
 
 public Student(int id, String name){
    studentId = id;
    studentName = name;
    
    korea = new Subject();
    math = new Subject();
 }
 
 public void setKoreaSubject(String name, int score){
    korea.SubjectName = name;
    korea.score = score;
 }
 
 public void setMathSubject(String name, int score){
    math.SubjectName = name;
    math.score = score;
 }
 
 public void showStudentScore(){
    int total = korea.score +  math.score;
    System.out.println(studentName + "학생의 총점은" + total + "점 입니다.");
 }
  
}
```
<br>

#### 성적 테스트
```java
public class StudentTest {

 	public static void main(String[] args) {
   	   Student studentLee = new Student(101, "이말년")
     	   studentLee.setKoreaSubject("국어", 75);
           studentLee.setMathSubject("수학", 65);
      
           studentLee.showStudentScore();
		
           Student studentKim = new Student(102, "김풍");
	   studentKim.setKoreaSubject("국어", 50);
	   studentKim.setMathSubject("수학", 38);
		
	   studentKim.showStudentScore();
      
      }
  
  
  
}
```

