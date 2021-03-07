### Object Class 
 ###### 모든 클래스의 최상위 클래스
 * ###### java.lang.Object 클래스. import하지 않아도 됨.
 * ###### 모든 클래스는 Object 클래스에서 상속 받음. 
 * ###### 모든 클래스는 Object 클래스의 메서드를 사용할 수 있음.
 * ###### 모든 클래스는 Object 클래스의 일부 메서드를 재정의하여 사용할 수 있음(final로 선언된 메서드 제외하고!)
# 
 **toString()메서드**  
 
        원형 : getClass().getName().+'@'+Integer.toHexString(hashCode())
 * ###### 객체의 정보를 String으로 바꾸어 사용할 때 유용함.
 * ###### 자바 클래스 중에는 이미 정의된 클래스가 많음. 많은 클래스에서 재정의하여 사용
   ###### ex)String, Integer,Calender 등
#
 **equals()메서드**
* ###### 두 객체의 동일함을 **논리적**으로 재정의 할 수 있음.
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
   ###### 논리적으로 동일 : equals의 반환값이 true
   ###### 동일한 hashCode 값을 가짐 = hashCode()의 반환 값이 동일 
   ###### =>overriding 재정의를 통해 equals가 true일 때 hashCode도 같은 값이 반환될 수 있도록.
 * ###### 일반적으로 equals 오버라이딩할 때 hashCode도 같이 오버라이딩된다. 

#
**clone()메서드**
 * ###### 객체의 복사본을 만듧.
 * ###### 기본 틀(prototype)으로 부터 같은 속성 값을 가진 객체의 복사본을 생성할 수 있음.
 * ###### 객체지향 프로그래밍의 정보은닉에 위배되는 가능성이 있으므로 복제할 객체는 clonealbe 인터페이스를 명시해야함.
