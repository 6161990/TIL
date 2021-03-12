## :pushpin: Abstract 추상클래스, 메소드 
* #### 추상 : 실체가 없다. <-> concreat class
* #### 추상 메소드 : 구현 코드가 없이 선언부만 있는 메서드 
* #### 추상 클래스 : 추상 메서드를 내포하고 있는 클래스

#### 추상클래스
```java    
public abstract class Car {
	
	public abstract void drive();         // 바디구현부 없음 
	public abstract void stop();
	
	public void startCar() {
		System.out.println("시동을 켭니다.");       // 일반 클래스는 바디구현부 존재
	}
	public void turnOff() {
		System.out.println("시동은 끕니다.");
	}
}
``` 

<br>

#### :round_pushpin: Abstract 추상클래스, 메소드 특징
* ##### abstract 예약어사용  
             
             public 'abstract' class ClassName {	//클래스에도 
                 public 'abstract' void methodName();   //메소드에도
             }
* ##### 추상 메소드는 바디를 구현하는 {중괄호} 부분이 존재하지 않음. 
  ##### 메서드의 바디가 없으니까 불려질 수 있는 게 없어서 추상 클래스는 new(인스턴스화)할 수 없음.
* ##### 클래스 안에 추상 메서드가 하나라도 있으면 추상 클래스.   

 
**굳이, 구현코드가 없는 abstract 사용이유**
* ###### 추상 클래스는 주로 상속의 상위 클래스로 사용됨
* ###### 하위 클래스에서 구현하도록 강제하기위해, "구현의 책임을 하위 클래스에게 위임한다"
* ###### 그니까 그 강제를 why? **"템플릿 메서드"**

<br>

#### 참고
* [Template Pattern, final](https://github.com/6161990/TIL/blob/main/DesignPattern/Template%20Pattern.md)

<br>

 #### :round_pushpin: final을 이용한 템플릿 메서드
```java    
public abstract class Car {
	
	public abstract void drive();        
	public abstract void stop();
	
	public void startCar() {
		System.out.println("시동을 켭니다.");      
	}
	public void turnOff() {
		System.out.println("시동은 끕니다.");
	}
	final public void run() {         //템플릿 메서드:위에 적어놓은 시동, 운전, 정지, 시동끄기의 로직을 정의해놓기 
		startCar();
		drive();	
		stop();
		turnOff();
	}
}
``` 

<br>

#### :round_pushpin: 추상클래스안에 추상 메소드가 아닌 메소드 ?
* ##### 추상 메서드는 하위 클래스가 구현해야하는 메서드로써 쓰이고, 
* ##### 추상 클래스에서 '이미 구현된 메서드'는 하위 클래스가 공통으로 사용하는 기능의 메서드로 쓰이며 
  ##### 하위 클래스에 따라 재정의할 수 있다. 
```java    
public abstract class Car {

            //생략....
      public void turnOff() {
		System.out.println("시동은 끕니다."); 
      }
      
      public void washCar() {}			
      
      final public void run(){
         startCar();		//이미 구현된 메서드
         drive();
         stop();
         turnOff();		//이미 구현된 메서드
         washCar(); 		//이미 구현된 메서드
       }
}
``` 
##### ->하위 클래스가 재정의하면 그제서야 기능을 구현하는 메소드
##### 기능을 확장할 수 있는 메소드. 

<br>

### :computer: 프로그래밍
#### 추상클래스로 만든 Car 프로그래밍
```java    
public abstract class Car {

      public abstract void drive();
      public abstract void stop();
	
      public void startCar() {
	  System.out.println("시동을 켭니다.");
	}
      public void turnOff() {
	  System.out.println("시동은 끕니다."); 
      }
      
      public void washCar() {}			
      
      final public void run(){
         startCar();		
         drive();
         stop();
         turnOff();		
         washCar(); 		
       }
       
       public static void main(String[] args) {
		Car aiCar = new AICar();
		aiCar.run();
		System.out.println("=============");
		Car manualCar = new ManualCar();
		manualCar.run();
	}
}
```
```java
public class ManualCar extends Car{

	@Override
	public void drive() {
	    System.out.println("사람이 운전합니다.");
	}

	@Override
	public void stop() {
	    System.out.println("브레이크를 밟아 정지합니다.");		
	}
}
```
```java
public class AICar extends Car{

	@Override
	public void drive() {
	    System.out.println("자율주행합니다.");
	}

	@Override
	public void stop() {
	    System.out.println("차가 스스로 멈춥니다.");
	}

	@Override
	public void washCar() {
	    System.out.println("자동 세차를 시작합니다");
	}
}
```

<br>

#### :round_pushpin: 추상클래스에서 일반클래스로
* ##### 추상 메서드 2개를 포함하고있는 추상 클래스를 상속받을 때 둘 다 구현해야 일반 클래스가 된다. 
  ##### => 모든 메서드가 구현되었다고해도 클래스에 abstract 키워드를 사용하면 추상클래스,
  #####    상속용으로만, 기반이 되기 위한 클래스를 만들기 위해 사용하기도함.
