## :pushpin: 내부클래스 Inner Class
#### 클래스 내부에 구현한 클래스(중첩된 클래스)
 * #### 클래스 내부에서 사용하기 위해 선언하고 구현하는 클래스, 이 클래스를 감싸고 있는 외부 클래스와 밀접한 연관이 있는 경우가 많고, 다른 외부 클래스에서 사용할 일이 거의 없는 경우에 내부 클래스로 선언해서 사용함.
 * #### 주로 외부 클래스 생성자에서 내부 클래스를 생성
 * #### 내부 클래스 유형
<img src="https://user-images.githubusercontent.com/74708028/110409999-856a8880-80cb-11eb-9ad0-aef3625854e5.jpg" width="500" height="400">  

<br>

```java
class OutClass {

	private int num = 10;
	private static int sNum = 20;
	private InClass inClass;
	
	public OutClass(){
		inClass = new InClass(); // 내부 클래스 생성
	}
	
	class InClass{
		
		int inNum = 100;
		//static int sInNum = 200;  //에러 남
		
		void inTest(){
			System.out.println("OutClass num = " +num + "(외부 클래스의 인스턴스 변수)");
			System.out.println("OutClass sNum = " + sNum + "(외부 클래스의 스태틱 변수)");
			System.out.println("InClass inNum = " + inNum + "(내부 클래스의 인스턴스 변수)");
		}
		
	    //static void sTest(){  //에러 남
	    	
	    //}
		
	}
	
	public void usingClass(){
		inClass.inTest(); //내부 클래스 변수를 사용하여 메서드 호출하기
	}
	
	static class InStaticClass{
		
		int inNum = 100;
		static int sInNum = 200;
		
		void inTest(){   //정적 클래스의 일반 메서드
			//num += 10;    // 외부 클래스의 인스턴스 변수는 사용할 수 없음.
			System.out.println("InStaticClass inNum = " + inNum + "(내부 클래스의 인스턴스 변수 사용)"); 
			System.out.println("InStaticClass sInNum = " + sInNum + "(내부 클래스의 스태틱 변수 사용)");
			System.out.println("OutClass sNum = " + sNum + "(외부 클래스의 스태틱 변수 사용)");
		}
		
		static void sTest(){  // 정적 클래스의 static 메서드
			//num += 10;   // 외부 클래스의 인스턴스 변수는 사용할 수 없음.
			//inNum += 10; // 내부 클래스의 인스턴스 변수는 사용할 수 없음
			
			System.out.println("OutClass sNum = " + sNum + "(외부 클래스의 스태틱 변수 사용)");
			System.out.println("InStaticClass sInNum = " + sInNum + "(내부 클래스의 스태틱 변수 사용)");
			
		}
	}	
}

public class InnerTest {

	public static void main(String[] args) {
	/*	OutClass outClass = new OutClass();
		System.out.println("외부 클래스 이용하여 내부 클래스 기능 호출");
		outClass.usingClass();    // 내부 클래스 기능 호출
	    System.out.println();
	    
		OutClass.InClass inClass = outClass.new InClass();   // 외부 클래스를 이용하여 내부 클래스 생성
		System.out.println("외부 클래스 변수를 이용하여 내부 클래스 생성");
		inClass.inTest();
		
		System.out.println();
		*/
		//외부 클래스 생성하지 않고 바로 정적 내부 클래스 생성
		OutClass.InStaticClass sInClass = new OutClass.InStaticClass();  
		System.out.println("정적 내부 클래스 일반 메서드 호출");
		sInClass.inTest();
		System.out.println();
		
		System.out.println("정적 내부 클래스의 스태틱 메소드 호출");
		OutClass.InStaticClass.sTest();
	}

}
```

<br>

#### :triangular_flag_on_post: 내부 클래스유형에 따른 정리

![Chapter 12 내부 클래스, 람다식, 스트림 - 01 내부 클래스_페이지_6](https://user-images.githubusercontent.com/74708028/110410185-d7131300-80cb-11eb-84a9-8097e820de19.png)
![Chapter 12 내부 클래스, 람다식, 스트림 - 01 내부 클래스_페이지_7](https://user-images.githubusercontent.com/74708028/110410192-da0e0380-80cb-11eb-9f18-4de095ca8558.png)
![Chapter 12 내부 클래스, 람다식, 스트림 - 01 내부 클래스_페이지_8](https://user-images.githubusercontent.com/74708028/110410197-dbd7c700-80cb-11eb-8afd-0a97fd23d8ab.png)
