### 인터페이스 요소 Interface Elements
* ###### 디폴트 메서드 : 기본 구현을 가지는 메서드. 구현하는 클래스에서 재정의할 수 있음
**사칙연산 로직이 있는 인터페이스 Calc**
```java
 public interface Calc {
	
	double PI = 3.14;
	int ERROR= -9999999;
	
	int add(int num1, int num2);
	int subStract(int num1, int num2);
	int times(int num1, int num2);
	int divide(int num1, int num2);
	
	default void description() {                        //디폴트 메서드 
		System.out.println("정수 계산기를 구현합니다.");
	}
}
```
**그 중 더하기와 빼기만 구현한 추상클래스, Calaulator**
```java   
public abstract class Calculator implements Calc{
	@Override
	public int add(int num1, int num2) {
		return num1 + num2;
	}

	@Override
	public int subStract(int num1, int num2) {
		return num1 - num2;
	}
}
```  
**그 Calculator를 상속받아 나머지 곱하기, 나누기를 구현한 CompleteCalc 클래스**
```java
public class CompleteCalc extends Calculator{

	@Override
	public int times(int num1, int num2) {
		return num1 * num2;
	}
	@Override
	public int divide(int num1, int num2) {
		if( num2 == 0 )
			return ERROR;
		else 
			return num1 / num2;
	}
	@Override
	public void description() {         //디폴트 메서드 오버라이딩(재정의) 
		System.out.println("재정의 한 description");
	}
}
```  
**디폴트 메서드 ; 인터페이스와 재정의한 오버라이딩메서드 중 호출은 재정의한 오버라이딩 인스턴스가 호출**
```java
public class CalcTest {

	public static void main(String[] args) {
		Calc calc = new CompleteCalc();
		int n1 = 10;
		int n2 = 2;
		
		System.out.println(calc.add(n1, n2));
		System.out.println(calc.subStract(n1, n2));
		System.out.println(calc.times(n1, n2));
		System.out.println(calc.divide(n1, n2));
		
		calc.description();  // "재정의 한 description" 출력됨. 
	}
}
  
#
* ###### 정적 메서드 : 인스턴스 생성과 상관없이 인터페이스 타입으로 호출하는 메서드
  ###### 디폴트로 데려다 쓰려면 하나하나 오버라이딩 필요(at. CompleteCalc), 인스턴스 생성도 필요(at. CalcTest)
  ###### static(정적) 메서드 이용하면 static제공으로 인터페이스 타입(Calc)으로 가져다 쓰게 할 수 있음. 
```java
 public interface Calc {
	
	double PI = 3.14;
	int ERROR= -9999999;
	
	int add(int num1, int num2);
	int subStract(int num1, int num2);
	int times(int num1, int num2);
	int divide(int num1, int num2);
	
	default void description() {       //디폴트 메서드
		System.out.println("정수 계산기를 구현합니다.");
  }  
  static int total(int[] arr) {      //정적 메서드
		int total = 0;
		
		for(int i: arr) {
			total += i;
		}
	
		return total;
	}
}
```
```java
public class CalcTest {

	public static void main(String[] args) {
		Calc calc = new CompleteCalc();
		int n1 = 10;
		int n2 = 2;
		
		System.out.println(calc.add(n1, n2));
		System.out.println(calc.subStract(n1, n2));
		System.out.println(calc.times(n1, n2));
		System.out.println(calc.divide(n1, n2));
		
		calc.description();
		

    int[] arr = {1,2,3,4,5};        
		int sum = Calc.total(arr);  //정적 메서드의 효용 : 인스턴스 생성 필요없이 바로 인터페이스 타입으로 가져다 쓸 수 있음 (Cal.total)
		System.out.println(sum);
	}

}
```

* ###### private메서드 : 인터페이스 내에서 사용하기 위해 구현한 메서드. 구현하는 클래스에서 재정의 할 수 없음.
  ###### static private 메서드는 일반 메소드에서 호출할 수 없음. static 메소드는 인스턴스를 생성하지 않으므로. 
  ###### 1. 일반 private
  ###### 2. 정적 private
  
**1. 일반 private**
```java
 public interface Calc {
	
	    //생략...
	
	default void description() {       //디폴트 메서드
		System.out.println("정수 계산기를 구현합니다.");
    myMethod();                      //디폴트 메서드 내에 일반 private메서드 
  }
  
  static int total(int[] arr) {      //정적 메서드
		int total = 0;
		
		for(int i: arr) {
			total += i;
		}
		return total;
	}
  
  private void myMethod() {       //디폴트 메서드로 들어가는 일반 private메서드
		System.out.println("private method");
	}
}
```
**2. 정적 private
```java
 public interface Calc {
	
	    //생략...
	
	default void description() {      //디폴트 메서드
		System.out.println("정수 계산기를 구현합니다.");
    myMethod();                      //1. 디폴트 메서드 내에 일반 private메서드 
  }
  
  static int total(int[] arr) {
		int total = 0;
		
		for(int i: arr) {
			total += i;
		}
    mystaticMethod();             //2. static 메서드 내에 private static 메서드
		return total;
	}
  
  private void myMethod() {       //1. 디폴트 메서드로 들어가는 일반 private메서드
		System.out.println("private method");
	}
  private static void mystaticMethod() {      //2. static 메서드로 들어가는 정적 private 메서드
		System.out.println("private static method");
	}
}
```












