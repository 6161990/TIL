### :pushpin: 내부클래스 Inner Class
* #### 클래스 내부에 구현한 클래스(중첩된 클래스)
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
```java
class Outer{
	
	int outNum = 100;
	static int sNum = 200;
	
		
	Runnable getRunnable(int i){ //익명 내부 클래스에게 외부 지역 변수 i 는 실상 상수임 final

		int num = 100;  //익명 내부 클래스에게 외부 지역 변수 i 는 실상 상수임 final
		
		class MyRunnable implements Runnable{

			int localNum = 10;
				
			@Override
			public void run() {
				//num = 200;   //에러 남. 지역변수는 상수로 바뀜
				//i = 100;     //에러 남. 매개 변수 역시 지역변수처럼 상수로 바뀜
				System.out.println("i =" + i); 
				System.out.println("num = " +num);  
				System.out.println("localNum = " +localNum);
					
				System.out.println("outNum = " + outNum + "(외부 클래스 인스턴스 변수)");
				System.out.println("Outter.sNum = " + Outer.sNum + "(외부 클래스 정적 변수)");
				}
			}
		 return new MyRunnable();
	}
}

public class LocalInnerTest {

	public static void main(String[] args) {

		Outer out = new Outer();
		Runnable runner = out.getRunnable(10);
		runner.run();
	}
```

<br>

#### :triangular_flag_on_post: 내부 클래스유형에 따른 정리

![Chapter 12 내부 클래스, 람다식, 스트림 - 01 내부 클래스_페이지_6](https://user-images.githubusercontent.com/74708028/110410185-d7131300-80cb-11eb-84a9-8097e820de19.png)
![Chapter 12 내부 클래스, 람다식, 스트림 - 01 내부 클래스_페이지_7](https://user-images.githubusercontent.com/74708028/110410192-da0e0380-80cb-11eb-9f18-4de095ca8558.png)
![Chapter 12 내부 클래스, 람다식, 스트림 - 01 내부 클래스_페이지_8](https://user-images.githubusercontent.com/74708028/110410197-dbd7c700-80cb-11eb-8afd-0a97fd23d8ab.png)


<br>

---

### :pushpin: 익명클래스 
* ##### 익명 내부 클래스를 정의할 때 클래스를 정의하면서 동시에 객체를 생성하여 단 한번만 사용하기 위해서 사용된다. 
* ##### 주로 추상클래스나 인터페이스를 이용해서 객체를 생성할 때 사용된다. 
```java
public interface Command {
	public abstract void execute();
	
}
```
```java
public class CommandProcess {
	public void process(Command command) {  //( Command command = anonymous)
		command.execute();
	}
}
```
```java
public class AnonymousInnerTest {

	public static void main(String[] args) {
		Scanner input = new Scanner(System.in);
		CommandProcess cp = new CommandProcess();
		while(true) {
		System.out.println("1.글쓰기 2. 전체목록");
		int number = input.nextInt();
		if(number==1) {
		cp.process(
				/*
				 * 컴파일러가 여기부터 
				class Anonymous implements Command 
				{

					@Override
					public void execute() {
						// TODO Auto-generated method stub
						
					}
					
				}
				Anonymous anonymous = new Anonymous();
				anonymous.execute();
				
				여기까지 알아서 코딩.(개발자 눈에 보이지 않음. 지워보자.)*/
				new Command() {
				
			@Override
			public void execute() {
				System.out.println("글쓰기");
			}
		}); 
		}
		else if(number == 2) {
		cp.process(new Command() {

			@Override
			public void execute() {
				System.out.println("전체목록");
			}
			
			
		});
		}
		}	
		// Command 같은 인터페이스나 추상클래스는 객체 생성이 불가한데 new로 Command를 어떻게 만들어?
		// 무명클래스로 가능. (단 한번만 사용하고 버려지는 클래스)
		// class Anonymous는 컴파일러가 가지고 있는 내장 클래스 
		// **상속없이 인터페이스나 추상클래스를 사용하기위해 Anonymous 클래스 이용한다.
	}

}

```


