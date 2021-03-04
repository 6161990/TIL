### 상속inheritance
* ###### 클래스에서 상속의 의미
  ###### 새로운 클래스를 정의할 때 이미 구현된 클래스를 상속(inheritance)받아서 속성이나 기능이 확장되는 클래스를 구현함. 
  ###### 단순한 코드의 재사용을 뜻하는 것이 아니라, 유사한 클래스를 만드는데 기존의 클래스를 가져다 조금 더 기능이 확장된 클래스를 만드는 것. 
        class B extend A{}  상위클래스 A를 상속받은 하위클래스B
    
* ###### 상위 클래스는 하위 클래스보다 일반적인 개념과 기능을 가짐
* ###### 하위 클래스는 상위 클래스보다 구체적인 개념과 기능을 가짐
* ###### 자바는 single inheritance만을 지원함 : extents뒤에는 단 하나의 class만 사용할 수 있음
   
   #
   
**protected** 
  ###### 외부클래스에 대해서는 private하게 하고 싶지만 날 상속 받은 클래스에 대해서는 변수를 접근하게하고싶다.
  ###### => protected (상속받은 관계에서는 public이고, 외부에는 private으로 사용되는 키워드)
   
**하위클래스가 생성되는 과정**
 ###### 하위 클래스가 생성될 때 상위 클래스가 먼저 생성됨
 ###### 상위 클래스의 생성자가 호출되고 하위 클래스의 생성자가 호출됨 
 ###### => 테스트 메소드에서 상위클래스 생성자없어도 오류가 안나는 이유 
 ```java
	// Customer customerLee = new Customer(10010, "이순신"); // 상속한 상위 클래스 생성자호출 없이도 오류가 안남
	// customerLee.setCustomerName("이순신");
	// customerLee.setCustomerID(10010);
	// customerLee.bonusPoint = 1000;
	// System.out.println(customerLee.showCustomerInfo());
		
	Customer customerKim = new VIPCustomer(10020, "김유신");   //이 안의 내부적으로 상위클래스 생성자가 호출되고 하위클래스가 호출된 과정이 숨어있기 때문.
	customerKim.setCustomerName("김유신");			
	customerKim.setCustomerID(10020);
	customerKim.bonusPoint = 10000;
	System.out.println(customerKim.showCustomerInfo());   
``` 

 ###### 상위클래스의 생성자가 호출되지 않을 경우, 컴파일러는 상위 클래스 기본 생성자를 호출하기 위한 super를 호출함. 
 ###### super();로 호출되는 생성자는 상위 클래스의 기본 생성자. 
 ###### 만약 상위 클래스의 기본 생성자가 없는 경우(매개변수가 있는 생성자만 존재하는 경우), 하위 클래스는 명시적으로 상위 클래스의 생성자를 호출해야함.    
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

**this와 super** 
  ###### this는 자기 자신을 가지고있는 메모리를 가리키고, super는 상위클래스의 메모리 위치, 참조값을 가리킨다.        
 
 
    
       
 **상위 클래스로의 묵시적 형 변환(업캐스팅)** 
 * ###### 상위 클래스 형으로 변수를 서언하고 하위 클래스 인스턴스를 생성할 수 있음. 
 * ###### 하위 클래스는 상위클래스의 타입을 내포하고 있으므로 상위 클래스로 묵시적 형 변환이 가능함.
 * ###### 상속관계에서 모든 하위 클래스는 상위클래스로 묵시적 형 변환이 됨. 그 역은 성립하지 않음. 
   ###### => 상위클래스 집합보다 하위 클래스 집합의 원소가 더 많은 원리. 
        Customer vc= new VIPCustomer(); 에서 vc가 가리키는 것은 Customer의 타입의 것만 가능


test메서드 
private 인 경우 get,set사용하고
public인 경우 바로 대입 

