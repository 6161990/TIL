## :pushpin: Overroading 오버로딩
* #### 클래스에 메소드를 정의할 때, 같은 이름이지만 다른 매개변수의 형식을 가진 여러 메소드를 정의할 수 있는 방법. 
  #### => 다양한 값의 처리방식을 하나의 이름으로 다루고자 할 때 쓰인다.
* ###### 참고 : 생성자 오버로딩은 클래스에 대한 객체를 new 생성할 때, 초기값을 주는 방법을 다양화시키고 싶을 때.
	######  메소드 오버로딩은 처리내용은 동일하되, 여러 종류의 값 다루게 하고자 할 때.
 
 
 <br>
 
#### Overroading 오버로딩  
```java    
    public void setOperands(int left, int right){     //매개변수 2개 메소드 
      System.out.println("setOperands(int left, int right)");
      this.left = left;
      this.right = right;
    }
    
    public void setOperands(int left, int right, int third){    //매개변수 3개 메소드 
      System.out.println("setOperands(int left, int right, int third)");
      this.left = left;
      this.right = right;
      this.third = third;
    }
    
    public static void main(String[] args) {
     Calculator c1 = new Calculator();   // 매개변수 2개 
      c1.setOprands(10,20);
      c1.sum();
    
      Calculator c2 = new Calculator();   // 매개변수 3개 
     c1.setOprands(10,20,30);
     c1.sum();
    }
 ```   
 #
#### But, 중복이 존재. 제거하기 
	this.left = left;
    this.right = right;
```java    
    public void setOperands(int left, int right){     
      System.out.println("setOperands(int left, int right)");
      this.left = left;
      this.right = right;
    }
    
    public void setOperands(int left, int right, int third){    
      System.out.println("setOperands(int left, int right, int third)");
      **this.setOperands(left, right);**    //중복 제거. 
      this.third = third;
    }      
``` 

<br>

### :round_pushpin: Overroading 오버로딩의 조건(오버라이딩과의 차이)
 * ##### 오버로딩은 공통점은 메소드이름,리턴값 / 차이점은 매개변수의 형식 
 * ##### 오버라이딩은 메소드이름, 리턴값, 매개변수의 형식 모든 것이 일치해야함. 
   ##### :triangular_flag_on_post: 완벽히 일치하면 그건 중복이 되기 때문에 super()를 이용해 코드를 줄이고, 수정할건하고 추가할 건 밑에 로직을 작성하면됨. 
       Overroading 은 "끌고 온다" , Overriding 은 "올라탄다". 


-------------------------------------------

### :pushpin: (method) Overriding 오버라이딩
* #### 재정의, 새롭게 정의한다. => super의 기능을 변경한다.
* #### @overriding 애노테이션
* #### 부모클래스도 가지고있고, 자식 클래스도 가지고 있는 메소드를 자식 클래스에서 재정의하게되면, 
  #### 부모클래스에서 정의한 메소드는 무시가 되고, 자식 클래스에서 정의한 메소드가 호출된다. 
* #### 상속과 오버라이딩
  #### 상속은, 메소드의 동작 방식을 기본적으로 공유한다. 공통분모를 정의한다.
  #### 오버라이딩은, 부모클래스에 있는 메소드를 그대로 상속받지 않고 하위 클래스에서 그 메소드를 재정의해 구현한다. 
  ####   =>기본값은 넓게 적용시키고 예외적으로 사용하는 변칙이 필요한 부분은 더 높은 우선순위를 배정하는 접근방법.
  
  <br>
  
#### Overriding 오버라이딩
```java    
public class Customer {
          //생략
    public int CalPrice(int price) {
	  	bonusPoint += price * bonusRatio;
		return price;
}
```         
```java    
public class VIPCustomer extends Customer {
          //생략
   @Override
	  public int CalPrice(int price) {
		  bonusPoint += price * bonusRatio;
		return price = (int)(price *salesRatio);
	}
}
```   

<br>

### :round_pushpin: Overriding 오버라이딩의 조건
* ##### 메소드의 서명(return 데이터 타입, 메소드 이름, 매개변수의 데이터 타입)이 부모의 것과 자식의 것이 일치해야함.
* ##### 자식 메소드에서 오버라이딩할 때는 

       	return super.method();
        하위메소드가 추가하고 싶은 기능이 있다면 밑에, 이 부분에 로직을 넣으면 된다. 
   
 <br>
            
### :round_pushpin: 형 변환과 Overriding 메서드 호출(가상함수)   

	Customer vc = new VIPCustomer();
	vc.calcPrice(10000);
* #### 여기서 Customer 는 Type , VIPCustomer는 인스턴스. 
  #### vc의 타입이 Customer이기 때문에 Customer의 것만 보임.
  #### 그러나 calcPrice(10000)메서드는 VIPCustomer 메서드가 호출된다. 
  #### why? 자바에서는 항상 인스턴스(VIPCustomer)의 메서드가 호출되기 때문에 => 가.상.함.수
 
 <br>
 
#### :triangular_flag_on_post: 가상함수(virtual method)?
* #####  메서드의 이름이 같다는 것은 메서드 주소가 같다는 것. 단, **재정의하지 않았을 시**
* #####  메서드는 수행되는 수행 코드의 위치가 따로 있는데, 함수가 호출되면 그 위치로 제어가 넘어간다. 
* #####  메서드와 제어가 넘어간 위치 사이에 그 주소를 매핑하고 있는 가상테이블이 있다. 
          메서드 -------------------**매서드 주소(mapping)**--------------------제어가 넘어온 메서드 영역
* ##### 상위클래스 메서드를 하위 클래스에서 **재정의**한다면 그 주소는 달라짐. 같은 메서드 이름이지만 각각 매핑되는 주소가 따로 생기는 것. 
  ##### So, 가상함수 작용으로 인해 호출 시 실제적으로 호출되는 애는 타입이 기반이 아니라 생성된 인스턴스의 기반으로 호출되는 것    


##### 한편, 오버로딩할 때는 컴파일 할 때 같은 메서드 이름이라도 컴파일 할 때 내부적으로 이름이 조금씩 바뀜(매개변수의 타입에 따라서)

<br>

 #### :triangular_flag_on_post:  오버로딩과 오버라이딩 비교
 * ##### overridding (재정의) 는 메소드를 하위 클래스에서 정의하고 overloading(다중정의)는 메소드를 같은 클래스에서 정의한다.
* ##### overridding은 메소드 이름, 매개변수(갯수와 데이터 타입), 리턴 타입이 모두 동일해야하고, overloading는 메소드 이름은 동일해야하지만 매개변수(개수나 데이터타입)과 리턴 타입은 다를 수 있다. 
* ##### overridding의 접근제어자는 하위 메소드의 접근 범위가 상위 메소드의 접근 범위보다 넓거나 같아야 하고, overloading에서 접근 제어자는 관계없다. 
* ##### overridding는 예외 발생시 같은 예외 형식이거나, 더 구체적인 예외 형식이어야하고, overloading에서는 관계 없다.  
