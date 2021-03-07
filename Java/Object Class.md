### Object Class 
 ###### 모든 클래스의 최상위 클래스, 객체지향에서의 object처럼 추상적 의미 아님. 
 * ###### java.lang.Object 클래스. import하지 않아도 됨.
 * ###### 모든 클래스는 사실 Object 클래스에서 암시적으로 상속 받고있음.  

            class A  => 실상은 class A (extends Object) 
 * ###### 모든 클래스는 Object 클래스의 메서드를 사용할 수 있음.
 * ###### 모든 클래스는 Object 클래스의 일부 메서드를 재정의하여 사용할 수 있음(final로 선언된 메서드 제외하고!)
# 
 **toString()메서드**  
 
        원형 : getClass().getName().+'@'+Integer.toHexString(hashCode())
 * ###### 어떠한 객체를 문자화시켜주는 메소드       
 * ###### 객체의 정보를 String으로 바꾸어 사용할 때 유용함.
 * ###### 자바 클래스 중에는 이미 정의된 클래스가 많음. 많은 클래스에서 재정의하여 사용
   ###### ex)String, Integer,Calender 등
  ```java    
class Book {

	String title;
	String author;
	
	public Book(String title, String author) {
		this.title = title;
		this.author = author;
	}
 
 @Override
	public String toString() {
		return author +","+title;
	}
	
}
public class ToStringTest{

	public static void main(String[] args) {
		Book book = new Book("토지","박경리");
		System.out.println(book);
		
		String str = new String("토지");
		System.out.println(str);
	}

}
 ```   
#
 **equals()메서드**
* ###### 두 객체의 동일함을 **논리적**으로 재정의 할 수 있음.
* ###### 원시데이터형 비교와 같이 단순비교는 연산자 '=='를 이용 (물리적동일함)
* ###### 물리적 동일함 : 같은 주소를 가지는 객체
* ###### 논리적 동일함 : 같은 학번의 학생, 같은 주문 번호의 주문
 
 ###### => 물리적으로 다른 메모리에 위치한 객체라도 논리적으로 동일함을 구현하기 위해 사용하는 메서드
        Student studentKim = new Student("김우빈");
        Student studentKim2 = studentKim2;
        Student studentKimWooBin = new Student(100,"김우빈");
        
        => studentKim , studentKim2 는 같은 힙 메모리에 저장되지만
           studentKimWooBin은 다른 힙메모리에 저장됨. 
           But, 물리적으로는 다른 위치에 있지만 논리적으로는 같은 학생임.
                 equals로 구현.
                 
 #
**hashCode()메서드**
 * ###### hashCode()메서드의 반환 값: 인스턴스가 저장된 가상머신의 주소를 10진수로 반환.
 * ###### 두 개의 서로 다른 메모리에 위치한 인스턴스가 동일하다는 것은? 
   ###### => 논리적 동일 : equals의 반환값이 true
   ###### => 동일한 hashCode 값을 가짐 = hashCode()의 반환 값이 동일 
   ###### => overriding 재정의를 통해 equals가 true일 때 hashCode도 같은 값이 반환될 수 있도록.
 * ###### 일반적으로 equals 오버라이딩할 때 hashCode도 같이 오버라이딩된다. 

#
**clone()메서드**
 * ###### 객체의 복사본을 만듧.
 * ###### protected 속성을 가지고 있음.
 * ###### 기본 틀(prototype)으로 부터 같은 속성 값을 가진 객체의 복사본을 생성할 수 있음.
 * ###### 복제 가능한 인터페이스를 생성하고(java virtual machine에게 알려줘야하니까) 구현해주어야함. 
 * ###### 객체지향 프로그래밍의 정보은닉에 위배되는 가능성이 있으므로 복제할 객체는 clonealbe 인터페이스를 명시해야함.
#
**finalize()**
* ###### 객체가 소멸될 때 호출하기로 한 메소드.
* ###### 참고 :garbage collection 인스턴스를 만들고 변수를 사용한 뒤, 더 이상 사용하지 않는다는 것을 인지해서 자동으로 쓰지않는 data를 삭제한다. 
