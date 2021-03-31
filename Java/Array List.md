### :pushpin: Array List
	List<E> list = new ArrayList<E>();
* ##### List의 후손으로 초기 저장용량은 10으로 자동설정되며 따로 지정도 가능하다. 저장용량을 초과한 객체들이 들어오면 자동적으로 늘어나며 고정도 가능하다. 동기화를 제공하지 않는다. 
* ##### 탄생이유 : 일반 배열의 한계에서 탄생, 배열은 차지하는 범위[]를 넘어서는 곳에 값을 추가하려고 할 때, 그 범위를 알지 못하면 사용하기 어려움. 
* ##### Collection Framework에서 Array List 제공. java.util 패키지 안에 Array List 클래스를 import해야 한다. 
* ##### 자바에서 제공되는 객체 배열이 구현된  Array List 클래스. 객체 배열을 사용하는데 필요한 여러 메서드들이 구현되어있음. 객체만 저장하기 때문에 기본 자료형은 Auto Wrapper Boxing 처리된다. 
* ##### 저장 순서가 유지되서 저장한대로 출력이 된다. index를 통해 for로 하나씩 조회하는 것이 가능하며, 순번을 통한 중간 위치 추가와 변경도 가능하다.
	* ##### 주요메서드 : add, int size, get(index), remove(index)
* ##### '제네릭'을 이용해 ArrayList 타입의 인스턴스를 생성할 때, 뒤에 <데이터 타입>을 지정. 
  ##### "변수를 통해 들어오는 값이 <지정한 데이터 타입>이다" 명시해 두었기 때문에 값을 꺼낼 때 데이터타입 (강제변환) 할 필요없다.   
       
<br>

#### ArrayList , 제네릭이용
```java
 public class ArrayListTest {

	public static void main(String[] args) {
		
		ArrayList<String> list = new ArrayList<String>();
		
		list.add("aaa");
		list.add("bbb");
		list.add("ccc");
		
		for(int i=0; i<list.size(); i++) {
			String str = list.get(i);  	//제네릭없이 사용시, String str = (String)list.get(i);
			System.out.println(str);
		}
		
		System.out.println("===================");
		
		for(String str: list) {     	//제네릭없이 사용시, for(Object str: list)
			System.out.println(str);
		}		
	}
}
``` 
   <br>
   
----------------------------------------------------------------------

### :computer: 프로그래밍해보기 
#### ArrayList를 이용해서 성적 산출 프로그래밍(과목 클래스)
```java
public class Subject {

	private String name;
	private int score;
	
	
	public Subject(String name, int score) {
		this.setName(name);
		this.setScore(score);
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public int getScore() {
		return score;
	}

	public void setScore(int score) {
		this.score = score;
	}
}
```

<br>

#### ArrayList를 이용해서 성적 산출 프로그래밍(학생 클래스)
```java
public class Student {
	
	int studentID;
	String studentName;
	ArrayList<Subject> subjectList;
	
	public Student(int studentID, String studentName) {
		this.studentID = studentID;
		this.studentName = studentName;
		
		subjectList = new ArrayList<Subject>();  //객체배열은 이렇게 한다고해서 데이터가 생성된게 아님
																	
	}
	
	public void addSubject(String name, int score) {
		Subject subject = new Subject(name, score); //직접 생성을 해줘야함. (String은 상수풀에 있기 때문에 생성필요없지만!)
		
		subjectList.add(subject); //생성한 뒤에, add.
	}
	
	public void showStudentInfo() {
		int total=0;
		for(Subject subject : subjectList) {
			total += subject.getScore();
			System.out.println
			(studentName+" 학생의 "+subject.getName()+" 과목의 성적은 "+subject.getScore()+" 점 입니다.");
		}
		System.out.println(studentName+" 학생의 총점은 "+total+" 점 입니다." );
	}

}
``` 
<br>

#### ArrayList를 이용해서 성적 산출 프로그래밍(메인 메소드)
```java
public class StudentTest {

	public static void main(String[] args) {
		Student studentLee = new Student(1001,"이말년");
		studentLee.addSubject("국어", 84);
		studentLee.addSubject("수학", 45);
		
		Student studentJu = new Student(1002,"주호민");
		studentJu.addSubject("국어", 74);
		studentJu.addSubject("수학", 65);
		studentJu.addSubject("영어", 98);
		
		studentLee.showStudentInfo();
		System.out.println("======================");
		studentJu.showStudentInfo();
	}

}

``` 
