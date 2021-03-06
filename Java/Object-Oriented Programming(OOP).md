## :pushpin: 객체 지향 프로그래밍 Object-Oriented Programming(OOP)
* ###### 참고 : [객제 지향 언어의 메모리 구조와 특징](https://github.com/6161990/TIL/blob/main/Java/OOP%20Memory.md)

#### :round_pushpin: 객체란

<img width="500" height="250" src="https://user-images.githubusercontent.com/74708028/112074532-dc875780-8bb9-11eb-8127-cdbc71a02607.jpg">

* ##### 현실에 존재하는 독립적이면서 하나로 취급되는 사물이나 개념을 말한다. 
* ##### 객체 지향 언어에서 객체의 개념은 클래스의 의해 메모리에 할당된 결과물(Object)이다.

<br>
<br>

#### :round_pushpin: 객체의 할당

<img width="600" height="220" src="https://user-images.githubusercontent.com/74708028/112074753-53245500-8bba-11eb-88f8-5d4141f8ee9b.jpg"/>

* ##### new연산자와 생성자를 사용하여 객체를 생성하면, 
##### heap 메모리 공간에 서로 다른 자료형의 데이터가 연속으로 나열 할당된 객체 공간이 만들어진다.
##### 이것을 인스턴스Instance 라고 한다.

<br>

##### :triangular_flag_on_post:  **new** 의 역할 
##### 1. 자유 메모리 공간 heap에 객체(인스턴스)를 만든다.
##### 2. 생성자를 통해서 초기화 처리한다. (기본 생성자면 준비된 기본 값으로 초기값 기록함)
###### => 생성된 인스턴스의 heap 주소가 레퍼런스 변수 s에 기록이 되면서 
######    stack 메모리에 있는 s가 heap에 있는 인스턴스의 주소를 참조하게된다. 

<br>

### :round_pushpin: 클래스
* #### 자료형이 다른 변수들의 연속 나열 (클래스의 멤버 변수) 
* #### 객체의 특성에 대한 정의를 한 것으로 캡슐화를 통해 기능 포함한 개념. 
* #### 외부에서 클래스내부의 필드에는 접근하지 못하지만, 멤버함수에는 접근가능. 
* #### 사물이나 개념의 공통 요소를 추상화하여 정의함. ex) 제품의 설계도

<br>

#### :triangular_flag_on_post: 클래스 멤버 
```java
[접근제한자] [예약어] class 클래스명{
  //멤버변수 Field, new 할 때 메모리에 연속으로 할당되는 변수. 
  자료형 변수명; 
  자료형 변수명;
  
  //생성자 Constructor
  [접근제한자] 생성자명(){}
  
  
  //멤버 함수 Method 기능정의설정
  [접근제한자] 리턴명 메소드명(매개변수){
      기능정의
  }
}
```

<br>

#### :triangular_flag_on_post: 자바에서 만들 수 있는 네 가지 클래스 형태
```java
[접근제한자] [예약어] class 클래스명{}
  
 public class 클래스명{...} //1
 class 클래스명{...} //2
 public abstract class 클래스명 {...}  //3
 public final class 클래스명 {...}  //4
```
  #####   1. 가장 일반적인 형태
  #####   2. default class = package private class
  #####   3. abstract = "미완성의" 상속에서 부모의 역할을 수행한다. 태어난 목적이 '부모'의 역할을 하기 위해서다. 
  #####       클래스 내 추상 메서드가 선언되어 있는 추상 클래스, 반드시 후손이 완성해야한다.
  #####   4. final 종단클래스 : 더 이상 후손을 만들지 못하는 클래스 , 클래스의 기능 확장을 하지 못하게 하려고 만든 클래스,
  #####      변경될 수 없는 클래스이다.
  ######    => final과 abstract 두 예약어를 동시에 사용할 수 없다. 상속 불가인 final, 반드시 상속해야하는 abstract, 반대의 개념을 가지고 있기 때문이다. 

<br>

#### :triangular_flag_on_post: 클래스 필드
```java
public class 클래스명 {
      접근제한자 [예약어] 자료형 변수명 [=초기값];
}
```
* ##### 클래스 필드 네 가지 접근 제한자 
    #####   1. public + : 전체공개
    #####   2. protected # : 상속이 안되었을 때는 default 와 같다. 패키지 안에 있는 클래스만 접근할 수 있다. 
    #####              상속이 되었을 때는 상속된 후손 내부에서만 부모의 것을 쓸 수 있다. 
    #####   3. default ~ : package private으로도 불린다.생략할 수 있다.
    #####   4. private - : 해당 클래스 내부에서만 사용가능하다. (캡슐화의 원칙)
#
* ##### 클래스 필드 예약어
   * ##### static : 같은 타입의 여러 객체가 공유할 목적의 필드에 사용하며, 프로그램 시작시 정적 메모리 영역에 자동 할당된다.
   * ##### final : 하나의 값만 계속 저장해야하는 변수에 사용한다. 메소드 안에 지역변수에도 final 사용가능하다.
#####      => static + final = 값을 변경할 수 없는 상수 의 의미다. 변수와의 구분을 위해 대문자로 선언한다.

<br>


#### :triangular_flag_on_post: 클래스 초기화 블럭
* ##### 초기화 순서 
   * ###### 클래스 변수
 
            JVM 기본값 -> 명시적 초기값 -> 클래스 초기화 블록 초기값

   * ###### 인스턴스 블록

           JVM 기본값 -> 명시적 초기값 -> 인스턴스 초기화 블록 초기값 -> 생성자를 통한 초기값
   
   <br>
   
##### :triangular_flag_on_post: 객체 지향 class의 핵심?
##### 자료형이 다른 변수들의 묶음을 private(-)하게 보관한다. 
##### => 외부에서 접근하지 못하게 캡슐화 하는 과정
##### 이 변수들에 대해 연산처리(메소드)등을 해야하는 기능들이 외부에 존재하게 되면 
##### 클래스 안에 멤버에 접근할 수 없기 때문에 해당 기능들을 클래스 안으로 집어넣어서 처리한다. 

<br>

#### 클래스 생성과정 (참조 자료형)
<img width="476" alt="20210323092513" src="https://user-images.githubusercontent.com/74708028/112074506-caa5b480-8bb9-11eb-9326-a00735520fb4.png">


<br>
<br>

### :round_pushpin: 추상화
* #### 유연성을 확보하기 위해 구체적인 것은 제거한다는 의미
* #### 프로그램에서 필요한 공통점을 추출하고, 불필요한 공통점을 제거하는 과정
#####      => 프로그램을 만들려면 필요한 data들이 있는데 그게 어떤 것인지 추출하는 과정
#####      ex) 국가에서 국민 정보 관리용 프로그램을 만들려고 할 때, 프로그램에서 요구되는 "국민 한 사람"의 정보를 추상화 한다면?
#####           국민 한 사람'당' 필요한 정보 : 이름, 주소, 성별, 전화번호, 나이, 주민번호 => 추상화해야할 data들.
* #### 추상화한 결과물을 객체 지향 프로그래밍 언어를 사용해서 변수명(데이터 이름)과 자료형(데이터 타입)을 정리함. 
  #### -> 그 다음 정리한 내용을 다이어그램으로 표현한다
#####      => 추출된 data들을 같은 종류씩 정리하는 ***DB 모델링*** 과정.

<br>

### :round_pushpin: 객체 지향의 3대 원칙
##### 1. 캡슐화 : 클래스의 멤버변수는 반드시 private처리한다.
* ###### 추상화를 통해 정리된 데이터들과 기능을 하나로 묶어 관리하는 기법을 말한다.
  ###### 클래스의 가장 중요한 목적인 데이터의 접근제한을 원칙으로 하여 클래스 외부에서 데이터의 직접 접근을 막고, 
  ###### 대신 데이터를 처리하는 함수들을 클래스 내부에 작성하는 방법을 캡슐화라고 한다. 
* ###### 캡슐화의 원칙 
  ###### 클래스의 멤버 변수에 대한 접근권한은 private을 원칙으로 한다. 
  ###### 클래스의 멤버 변수에 대한 연산처리를 목적으로하는 함수들을 클래스 내부에 작성한다.
  ###### 멤버 함수는 클래스 밖에서 접근할 수 있도록 public으로 설정한다. 
  
  <br>
  
##### 2. 상속 : 소스코드 중복을 줄이기 위한 방법론.
* ##### 다른 클래스가 가지고 있는 멤버(필드와 메소드)들을 새로 작성할 클래스에서 직접 만들지 않고, 상속을 받음으로써
  ##### 새 클래스가 자신의 멤버처럼 사용할 수 있는 기능, 클래스를 재사용하기 위해 사용하며 여러 프로젝트에 같은 기능의 클래스가 필요한 경우에도 상속을 사용한다.
* ##### 보다 적은 양의 코드로 새로운 클래스를 작성할 수 있고, 코드를 공통적으로 관리하기 때문에 코드의 추가 및 변경이 용이하다.
  #####   => 코드의 중복을 제거하여 프로그램의 생산성과 유지보수가 좋아진다.

##### 3. 다형성 : 상속을 이용해 다양한 타입 ( = 다양한 클래스)
###### '서로 다른 형태'를 지칭하는 말로 객체지향 프로그래밍의 3대 특징 중 하나이며, 하나의 행동으로 여러가지 일을 수행하는 개념이다.
###### 상속을 이용한 기술로, 부모 타입으로부터 파생된 여러 가지 타입을 하나의 타입인 것 처럼 처리할 수 있다. 
* #####         여러 종류의 클래스를 한 가지 타입으로 해결하는 기술.
* #####         부모 클래스가 후손 클래스의 레퍼런스 정보를 받을 수 있음.
* #####         부모의 데이터 타입으로 매개변수를 선언하면 메소드의 오버로딩을 줄일 수 있음
* #####         클래스 안에서 같은 메소드 이름을 중복작성해야할 경우, 다형성 이용.
#
###### :+1: 클래스 형변환 up casting (작은 것에서 많은 것으로 학장)
###### 상속 관계에 있는 부모, 자식 클래스 간에 부모타입의 레퍼런스가 모든 후손 타입의 객체의 주소를 받을 수 있다. 
        //Sonata 클래스가 Car 클래스의 후손임
        Car c = new Sonata();
        Sonata 클래스형 -> Car 클래스 형으로 바뀜
###### :-1: 클래스 형변환 down casting  (많은 것에서 작은 것으로 축소)
###### 후손 객체의 주소를 받은 부모 레퍼런스를 가지고 후손의 멤버를 참조해야할 경우에는, 후손 클래스 타입으로 레퍼런스를 형변환해야한다. 
###### 이 때 부모 클래스 타입을 후손 클래스 타입으로 바꾸는 것을 down casting 이라고 하며, 자동으로 처리되지 않기 때문에 반드시 후손 타입을 명시해서 형변환해야한다. 객체는 상속이 되지 않는다. (클래스와 객체의 차이)
            //Sonata 클래스가 Car 클래스의 후손임
            Car c = new Sonata();
            (Car)c.moveSonata();
   ###### (( 주의 )) 같은 층위의 객체끼리는 업, 다운 캐스팅을 할 수 없다. 
* ###### 참고 [업다운캐스팅](https://github.com/6161990/TIL/blob/main/Java/UpDownCasting%2C%20instanceof.md)
  #
###### :triangular_flag_on_post: instanceof 연산자
###### 주로 down casting 할 때, 현재 레퍼런스가 어떤 클래스형의 객체 주소를 참조하고 있는지 확인이 필요할 때 사용함.
```java
if(레퍼런스 instanceof  클래스 타입){
  참일 때 처리할 내용
  //해당 클래스 타입으로 down casting
}
```
