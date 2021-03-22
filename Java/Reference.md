### :pushpin: 참조자료형 reference data type
* #### 클래스를 자료형으로 선언함. 그때의 변수는 레퍼런스(참조) 변수
* #### 기본 자료형은 사용하는 메모리가 정해져 있지만, 참조자료형은 클래스에 따라 다름.
* #### 기본 자료형은 실제 데이터(값)을 저장하지만, 참조자료형은 할당된 객체(인스턴스)의 주소를 저장함.
* #### 기본 자료형은 논리형, 문자형, 정수형, 실수형으로 나눠지고, 8개의 자료형이 있다. 
* #### 참조자료형은 4byte의 공간을 할당하며 정수형 주소만을 저장함(값은 저장하지 못함)

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

