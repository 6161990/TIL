
### :pushpin: 인터페이스Interface
* #### 인터페이스 :  상수형 필드와 추상 메소드만을 작성할 수 있는 추상 클래스의 변형체이다. 
  #### abstract,final 처럼 규제역할을 한다.(클라이언트 프로그램에 어떤 메서드를 제공하는지 알려주는 명세서역할)
  ###### => 메소드의 통일성을 부여하기 위해서 추상 메소드만 따로 모아 놓은 추상 클래스로, 상속시 인터페이스 내에 정의된 모든 추상 메소드를 구현해야한다. 
* #####              클라이언트 프로그램은 실제 구현내용은 몰라도 인터페이스 정의만 알면 그 객체를 사용할 수 있음.
  ##### 어떤 객체가 있고 그 객체가 특정한 인터페이스를 사용한다면, 그 객체는 반드시 인터페이스의 메소드를 구현해야한다.
          interface I {
           public void z();    -> abstract 메소드
          }
  
         class A implements I {     // 'implements' 뜻 :"시행한다"
           public void z(){}  -> 구현 메소드
          }
          => "class A가 interface I를 구현(implements)한다." 

<br>

#### :round_pushpin: 인터페이스를 사용하는 이유
* ##### 탄생이유 : 클래스의 본래 목적은 객체 생성이기 때문에 클래스 안에 abstract로 미완성을 넣기 보다는 차라리 규칙을 강제하고 싶은 메소드만 모아서 클래스를 만들자   
  ##### => 완벽한 미완성 클래스 interface 탄생. 
* ##### 프로그램의 로직을 인터페이스로 구성하고 그 로직에 따라 implements 로 구현하면, 
  ##### 그 안에서 인터페이스가 "어떠한 클래스가 어떠한 메소드를 가지고 있는가" 에 대한 명세서와 같은 역할을 하기 때문에, 
  ##### 같은 프로그램을 만드는 개발자 사이에서 커뮤니이션이 정확하게 이루어질 수 있음. 그래서 설계 단계에서 ***전략패턴*** 으로 많이 쓰임.

<br>

* 참고 : [전략 패턴 (Strategy Pattern)](https://github.com/6161990/TIL/blob/main/DesignPattern/Strategy%20Pattern.md)
#


#### :round_pushpin: 인터페이스의 특징
##### 1. 모든 인터페이스의 메소드는 묵시적으로 public이고 abstract이다. 
##### 2. 변수는 묵시적으로 public static final이다. => 인터페이스 변수의 값 변경 시도는 컴파일시 에러발생
##### 3. 객체 생성은 안되나, 참조 변수로서는 가능하다. 
<br>

#### :round_pushpin: 인터페이스의 요소
* ##### 추상메서드 : 추상클래스는 일부는 일반, 일부는 추상메서드 혹은 모두 구현되어있지만 추상클래스라고 선언되어있는데 
  #####             인터페이스는 only 추상메서드로만 구성, 일반 메서드 올수 없음. 그래서 굳이 abstract 예약어 사용하지 않아도 됨. 어차피 다 추상.
* ##### 상수 : 인터페이스 안에 있는 모든 변수는 컴파일 과정에서 상수로 변환된다. final 필드 가질 수 있다.
* ##### 디폴트 메서드, 정적 메서드, private 메서드 : 인터페이스가 구현을 하지 못하니까 그 아래에서 다른 것들끼리 중복구현이 될 수 있는데,   
  ##### 그것을 막기위한 장치. 

<br>

* 참고 : [인터페이스 요소 Interface Elements](https://github.com/6161990/TIL/blob/main/Java/Interface%20Elements.md)

<br>

#### :round_pushpin: 인터페이스의 규칙
* ##### 하나의 클래스는 여러 개의 인터페이스를 구현할 수 있다. (한편, 자바의 상속에서는 하나의 부모클래스만 상속받을 수 있다.)
  ##### 여러 개의 인터페이스를 받을 때 디폴트 메서드의 이름이 중복되는 경우가 있다면? 
              @Override
              public void y() {
                  해결방법 1. 여기서 재정의한다.
                  해결방법 2. I1.super.y(); or
                             I2.super.y();   I1 or I2 둘 중에 뭐 쓸 건지 결정한다. 
              }
* ##### 인터페이스는 그 안에 규정된 메소드들을 외부에서 조작하기 위한 장치이므로, public 메소드여야한다.
```java
          interface I1 {
            public void x();// 모든 인터페이스 메소드는 퍼블릭.
            public void y(); //
          }
          
          interface I2 {
            public void z();
            public void y();
          }
  
         class A implements I1, I2 {   
            public void x(){}           //class A 는 I1, I2 메소드를 다 구현해야하는 의무가 있다. 
            public void z(){}  
          }
```           
 ###### :triangular_flag_on_post: 인터페이스는 상속이 가능하다. 
 ###### 구현이 없으므로 extends 뒤에 여러 인터페이스를 상속받을 수 있음.
 ###### 구현 내용이 없으므로 타입 상속(type inheritance)라고도 함.
 
 <br>
 
```java
           interface I3 {
            public void x();    
          }
          
          interface I4 extends I3 {     
            public void z();    
          }
  
         class B implements I4 {      //class B, I4를 상속한 I3의 메소드도 구현해야한다. 
            public void x(){}          
            public void z(){}  
          }
``` 

<Br>
  
* 참고 : [인터페이스 구현과 클래스 상속 함께 사용하기](https://github.com/6161990/TIL/blob/main/Java/Interface%20and%20Inheritance.md)

<br>

#### :round_pushpin: 추상 클래스와 인터페이스의 차이
         abstract vs. interface
* ##### abstract 클래스는 클래스이고, interface는 interface라는 class가 아닌 고유한 형태이다.
* ##### abstract는 extends 사용, interface는 implements사용한다.
* ##### abstract는 abstract 메소드가 0개 이상, interface는 모든 메소드가 abstract이다.
* ##### abstract는 명시적으로 abstract를 사용, interface는 묵시적으로, 당연히 abstract다.
* ##### abstract와 interface 둘 다 객체 생성이 불가하며, 용도는 참조 타입으로 쓰이기 위함이다. 
* ##### abstract 클래스는 특정 메소드를 하위클래스가 강제하여 사용할 뿐, 구체적인 로직이나 기타 상태를 가지고 있을 수 있다. 
  ###### 반면에, interface는 안에 구체적인 로직이나 상태를 가지고 있을 수 없다. 반드시 물체가 없는 메소들만을 가지고 있을 수 있다. 

<br>

#### :round_pushpin: 인터페이스 타입상속과 형변환 그리고 다형성
##### 어떤 특정한 클래스에서의 그것'만'을 사용하기위해서 이용, 사용자가 다른 메소드를 신경 쓸 필요가 없고, 만든이 입장에서는 사용자가 사용하지 않도록 방지할 수 있음.
```java 
           interface I {
            public String A();    
          }
          
         interface I2 {     
            public String B();  
          }
  
         class All implements I2,I3 {      
            public String A(){}          
            public String B(){}  
          }
          
          public class InterfaceDemo{
            public static void main(String[] args){
              All obj = new All();            // public String A,B 둘 다 사용할 때,
              I objI = new All();           // public String A 만 사용하고 싶을 때, 구현해둔 All의 인스턴스에 A만 있는 데이터 타입(I)으로 변수를 지정.
              I2 objI2 = new All();         // public String B() 만 사용하고 싶을 때, 구현해둔 All의 인스턴스에 B만 있는 데이터 타입(I2)으로 변수를 지정.
              
              obj.A();
              obj.B();
              
              objI.A();
              //objI.B();
              
              //objI2.A();
              objI2.B();              
              }
          }
``` 
##### :triangular_flag_on_post: I objI = new All(); 인터페이스를 구현한 클래스 All은 인터페이스 타입(I or I2)로 변수를 선언하여 인스턴스를 생성할 수 있음. 
#####    이게 바로 인터페이스를 타입 상속이라고도 하는 이유!!!

##### :triangular_flag_on_post: interface I,interface I, class All을 인스턴스화 시킬 때, 같은 데이터 타입(class All)을 공유하고 있지만, 
#####    그 실제 클래스가 무엇이냐에 따라서 (interface I,interface I2 안에 있는 메소드가 무엇이냐에 따라서),
#####    다르게 구현할 수 있는 ***'다형성'***

<br>

#### :round_pushpin: 인터페이스를 구현해 놓은 다양한 객체(다형성)
###### EX) JDBD를 구현한 오라클, MSSQL라이브러리 등.
<img src = "https://user-images.githubusercontent.com/74708028/110082858-4689b980-7dd1-11eb-8dbe-95b552150097.jpg" width="670px" height="400">

