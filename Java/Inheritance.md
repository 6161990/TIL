## :pushpin: 상속 inheritance
* ###### 참고 : [객제 지향 언어 OOP](https://github.com/6161990/TIL/blob/main/Java/Object-Oriented%20Programming(OOP).md), [객제 지향 언어의 메모리 구조와 특징](https://github.com/6161990/TIL/blob/main/Java/OOP%20Memory.md)
* #### 클래스에서 상속의 의미
  #### 새로운 클래스를 정의할 때 이미 구현된 클래스를 상속(inheritance)받아서 속성이나 기능이 확장되는 클래스를 구현함. 
  #### 단순한 코드의 재사용을 뜻하는 것이 아니라, 
  #### 유사한 클래스를 만드는데 기존의 클래스를 가져다 조금 더 기능이 확장된 클래스를 만드는 것. 
        class B extend A{}  상위클래스 A를 상속받은 하위클래스B
    
* #### 상위 클래스는 하위 클래스보다 일반적인 개념과 기능을 가짐
* #### 하위 클래스는 상위 클래스보다 구체적인 개념과 기능을 가짐
* #### 자바는 single inheritance만을 지원함 : extents뒤에는 단 하나의 class만 사용할 수 있음
   
  <br>
   
#### :round_pushpin: protected
  * ##### 외부클래스에 대해서는 private하게 하고 싶지만 날 상속 받은 클래스에 대해서는 변수를 접근하게하고싶다.
    ##### => protected : 상속받은 관계에서는 public이고, 외부에는 private으로 사용되는 키워드 
  * #### 한편, 부모의 private 멤버는 상속은 되지만 접근 불가능하다. 
    ##### => 후손 객체 생성시에 부모의 필드값 전달받은 경우, 후손 생성자 안에서 부모의 private 필드에 직접 초기값을 대입하지 못한다. 
    ##### => 전달받은 부모 필드 값을 부모 생성자 쪽으로 넘기는 방법을 이용한다. 
    		ex) super(전달 받을 값, ...) ; // 부모의 매개변수 있는 생성자를 통한 초기화 
  
  <br>		
  
#### :triangular_flag_on_post: 제어자 조합 유의사항  
* ##### 클래스 : public, default, final, abstract 사용가능
* ##### 메소드 : 모든 접근 제어자, final, abstract , static
* ##### 변수 : 모든 접근 제어자, final, static
* ##### 지역변수 : final
##### - private 메소드의 오버라이딩은 불가하다.
##### - 메소드에 static과 abstract 함께 사용할 수 없다.  정적 메모리 할당(static)과 미완성 (abstract)다.
##### static은 프로그램 시작시 함께 할당되기때문에 아직 완성되지 않은 미완성 추상클래스는 사용할 수 없다.

##### - 클래스에 abstract과 final을 동시에 사용할 수 없다. 반드시 상속과, 상속 불가의 반대개념이기때문. 
##### - abstract 메소드의 접근제어자가 private일 수 없다. 후손이 접근해서 사용해야 하기 때문, private은 같은 클래스 내에서만 가능함

##### - 메소드에 private와 final을 같이 사용할 수 없다. final은 한번 정한 값을 외부에서 고칠 수 없다뿐이지 외부 사용이 언제나 가능하다.
##### - 부모 메소드의 접근제어자 수정 가능하다. 단, 부모의 것보다 같거나 넓은 범위로만 변경가능하다. 
  
 <br>
  
  
 #### :triangular_flag_on_post: 동적 바인딩과 정적 바인딩
* ##### 바인딩 : 실제 실행할 메소드 코드와 호출하는 코드를 연결시키는 것. 클래스를 컴파일 할 때, 모든 소스 코드는 정적바인딩된다. 
* ##### 그런데 후손 클래스가 부모의 것을 오버라이딩 했을 때는? 부모 쪽으로 정적 바인딩 연결되었다가 실행이 될 때 레퍼런스가 후손 객체를 참고하고 있으면 후손에 오버라이딩된 메소드로 연결된 연결을 바꾸면서 실행된다. => 동적 바인딩 (@override 애노테이션으로 파악한다.)
 * ##### 성립 요건 : 상속 관계로 이루어져 다형성이 적용된 경우에, 메소드 오버라이딩이 되어있으면 정적으로 바인딩 된 메소드 코드보다 오버라이딩 된 메소드 코드를 우선적으로 수행하게 된다. 
  
 <br>
    
### :round_pushpin: 하위클래스가 생성되는 과정
 #### 1. 하위 클래스가 생성될 때 상위 클래스가 먼저 생성됨
 #### 2. 상위 클래스의 생성자가 호출되고 하위 클래스의 생성자가 호출됨 
 #### => 테스트 메소드에서 상위클래스 생성자없어도 오류가 안나는 이유 
 ```java
	// Customer customerLee = new Customer(10010, "박민아"); // 상속한 상위 클래스 생성자호출 없이도 오류가 안남
	// customerLee.setCustomerName("박민아");
	// customerLee.setCustomerID(10010);
	// customerLee.bonusPoint = 1000;
	// System.out.println(customerLee.showCustomerInfo());
		
	Customer customerKim = new VIPCustomer(10020, "송혜교");   //이 안의 내부적으로 상위클래스 생성자가 호출되고 하위클래스가 호출된 과정이 숨어있기 때문.
	//customerKim.setCustomerName("송혜교");			
	//customerKim.setCustomerID(10020);
	customerKim.bonusPoint = 10000;
	System.out.println(customerKim.showCustomerInfo());   
```   

 #### 3. 상위클래스의 생성자가 호출되지 않을 경우, 컴파일러는 상위 클래스 기본 생성자를 호출하기 위한 super를 호출함. 
  ##### => 부모 클래스의 생성자, 초기화 블럭은 상속되지 않으며 후손 클래스 객체 생성시, 부모 클래스 생성자가 먼저 실행되도록 되어있다.
  ##### => super();로 호출되는 생성자는 상위 클래스의 기본 생성자. 
  ##### => 후손 객체 생성시에는 부모부터 생성된다. 그렇기 때문에 후손 클래스 생성자 안에는 부모의 생성자를 호출하는 super();가 첫줄에 존재한다. 부모 생성자가 가장 먼저 실행이 되어야 하기때문에 명시적으로 작성시에도 반드시 첫줄에만 작성할 수 있다. 후손의 매개변수 있는 생성자 작동시 초기값의 일부를 부모쪽으로 넘겨야 할 경우에는 부모의 매개 변수 있는 생성자 쪽으로 초기값을 넘길때 사용한다.

 
 <br>
 
 #### 4. 만약 상위 클래스의 기본 생성자가 없는 경우(매개변수가 있는 생성자만 존재하는 경우), 
 ####    하위 클래스는 명시적으로 상위 클래스의 생성자를 호출해야함. 
   ##### (후손 클래스 생성자 안에서 부모 클래스 생성자 호출을 명시하고 싶으면 super();를 입력한다.)
   ##### => super();는 디폴트 생성자, 상위클래스에는 super(customerID, customerName); 생성자만 존재. 
   #####    하위클래스에서 super(customerID, customerName); 라고 명시필요.
 
     	 => error message "Implicit super constructor ***상위.class()*** is undefined.
         	                 Must explicitly invoke another constructor(생성자)"
				 
<br>

 ```java
   public class VIPCustomer extends Customer{
	
	double salesRatio;
	private int agentID;
	
	public VIPCustomer(int customerID, String customerName) {
	     super(customerID, customerName);         //상위 클래스기본 생성자를 호출하기 위한 super
		
	     customerGrade = "VIP";
	     bonusRatio = 0.05;
	     salesRatio = 0.1;
	}
}	
```     
   
   <br>

### :round_pushpin: this.와 super.
 * ##### this는 자기 자신을 가지고있는 메모리를 가리키고, super는 상위클래스의 메모리 위치, 참조값을 가리킨다.        
   
   <br>
       
 ### :round_pushpin: 상위 클래스로의 묵시적 형 변환(업캐스팅)
 * ##### 상위 클래스 형으로 변수를 서언하고 하위 클래스 인스턴스를 생성할 수 있음. 
 * ##### 하위 클래스는 상위클래스의 타입을 내포하고 있으므로 상위 클래스로 묵시적 형 변환이 가능함.
 * ##### 상속관계에서 모든 하위 클래스는 상위클래스로 묵시적 형 변환이 됨. 그 역은 성립하지 않음. 
   ##### => 상위클래스 집합보다 하위 클래스 집합의 원소가 더 많은 원리. 
        Customer vc= new VIPCustomer(); 에서 vc가 가리키는 것은 Customer의 타입의 것만 가능
   
 --------------------------------------------------------------------------
 
### :computer: 프로그래밍해보기
   
#### 상속을 이용한 백화점 고객 보너스포인트 프로그래밍  

**일반 Customer** 
 ```java
   public class Customer {

	protected String customerName;
	protected String customerGrade;
	protected int customerID;
	int bonusPoint;
	double bonusRatio;
	
	public Customer(int customerID, String customerName) {
		this.customerID= customerID;
		this.customerName= customerName;
		
		customerGrade = "SILVER";
		bonusRatio=0.01;
	}
	
	public int CalPrice(int price) {
		bonusPoint += price * bonusRatio;
		return price;
	}
	public String showCustomerInfo() {
		return customerName+ "님의 등급은" +customerGrade +"이며, 적립된 보너스 포인트는"+bonusPoint+" 점 입니다.";
	}
}		
```   
**VIP Customer** 
 ```java
   public class VIPCustomer extends Customer{
	
		double salesRatio;
		private int agentID;
		
	public VIPCustomer(int customerID, String customerName) {
		super(customerID, customerName);
		
		customerGrade = "VIP";
		bonusRatio = 0.05;
		salesRatio  =0.1;
	}
}	
```   
**Test** 
 ```java
   public class CustomerTest {

	public static void main(String[] args) {

		Customer customerLee = new Customer(10010,"박민아");
		customerLee.bonusPoint=1000;
		System.out.println(customerLee.showCustomerInfo());
		
		Customer customerKim = new VIPCustomer(100011,"송혜교");
		customerKim.bonusPoint=15000;
		System.out.println(customerKim.showCustomerInfo());
	}
}	
```   
