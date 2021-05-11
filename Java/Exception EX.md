### :pushpin: 예외(Exception) 처리 예제

<br>

### 💻 점수 입력 프로그래밍해보기
#### Score.java
```java
package oop.exception02;

import java.io.IOException;
import java.util.InputMismatchException;

public class Score {
	
	private String name;
	private int kor,eng,math;
	
	public Score() {}
	
	public Score(String name, int kor, int eng, int math) {
		super();
		this.setName(name); 
		this.setKor(kor); 
		this.setEng(eng);
		this.setMath(math);
	}
	
	public int total() throws Exception {
		return kor+eng+math;
	}

	public int avg() throws Exception {
		return (kor+eng+math)/3;
	}
	public String getName() {
		return name;
	}

	public void setName(String name) {
		
		//예외를 만들 때 Exception은 반드시 던지거나 잡아줘야함 CHECKED EXCEPTION이기때문에 
		try { 
		if(!(name.length() >= 2  && name.length()<=8)) {
			throw new Exception("이름은 두 글자에서 여덟글자 이하로 입력하세요.");
		}
		}catch(Exception e) {
			System.out.println("이름은 두 글자에서 여덟글자 이하로 입력하세요.");
		}
		this.name = name;
	}

	public int getKor() {
		return kor;
	}

	public void setKor(int kor) {
		//예외를 만들 때 Exception은 반드시 던지거나 잡아줘야함 CHECKED EXCEPTION이기때문에 
		//BUT, InputMismatchException은 잡아주지 않아도 됨. UNCHECKED EXCEPTION 이기때문에
		if(!(kor > 0 && kor <= 100)) {
			throw new InputMismatchException("국어점수는 0점이상 100점 이하로 입력하세요");
		}
		this.kor = kor;
	}

	public int getEng() {
		return eng;
	}

	public void setEng(int eng) {
			if(!(eng > 0 && eng <= 100)) {
				throw new InputMismatchException("영어점수는 0점이상 100점 이하로 입력하세요");
			}
		this.eng = eng;
	}

	public int getMath() {
		return math;
	}

	public void setMath(int math) {
			if(!(math > 0 && math <= 100)) {
				throw new InputMismatchException("메세지 없어도됨.");
			}
		this.math = math;
	}
	
	

}

```

<br>

#### Run.java
```java
package oop.exception02;

import java.util.InputMismatchException;
import java.util.Scanner;

public class Run2 {

	public static void main(String[] args) {
			Score score = new Score();
			
		try (Scanner sc = new Scanner(System.in)){
			System.out.println("이름을 입력하세요");
			String name = sc.next();
			score.setName(name);
			
			System.out.println("국어점수 : ");
			int kor = sc.nextInt();
			score.setKor(kor);
			
			System.out.println("영어점수 : ");
			int eng = sc.nextInt();
			score.setEng(eng);
			
			System.out.println("수학점수 : ");
			int math = sc.nextInt();
			score.setMath(math);
			
			System.out.println("이름 : "+ score.getName());
			System.out.println("국어 점수 : "+ score.getKor());
			System.out.println("영어 점수 : "+ score.getEng());
			System.out.println("수학 점수 : "+ score.getMath());
			System.out.println("총점 : "+score.total());
			System.out.println("평균 : "+score.avg());
		}catch(InputMismatchException e) {
			e.printStackTrace();
			System.out.println("예외처리완료");
		}catch(ArithmeticException e) {
			e.printStackTrace();
		}catch(Exception e) {
			e.printStackTrace();
			System.out.println("예외처리완료");
		} 
//		finally {
//			sc.close();
//		}
	}

}
```
