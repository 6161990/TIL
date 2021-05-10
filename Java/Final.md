### :pushpin: FINAL
* ###### 파이널 변수는 값이 변경될 수 없는 상수
          public static final double PI=3.14	
  ###### 오직 한번만 값을 할당할 수 있음
* ###### 파이널 메서드는 하위 클래스에서 재정의(오버라이딩)할 수 없음
* ###### 파이널 클래스는 더이상 상속되지 않음
* ###### 프로젝트 구현 시 여러 파일에서 공유해야하는 상수 값은 하나의 파일에 선언하여 사용하면 편리함.    
 

#### final을 이용한 템플릿 메서드 패턴
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
