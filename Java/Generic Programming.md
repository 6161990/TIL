### :pushpin: 제네릭 프로그래밍 Generic Programming
###### Generic : 일반적인, 포괄적인

	클래스명<클래스타입> 레퍼런스 = new 생성자<클래스타입>();
	
* #### 클래스 내부에서 사용할 데이터 타입을 외부에서 확정하는 기법
* #### jdk1.5 부터 제공되는 기능으로 컬렉션 클래스를 이용해서 객체를 저장할 때, 저장할 객체(클래스타입)을 제한하는 기능으로, 한가지 종류의 클래스만 저장할 수 있게 해놓은 기능이다. 

<img src="https://user-images.githubusercontent.com/74708028/110271099-ad45e780-800a-11eb-90a4-a71e5971dbb6.jpg" width="850" height="300">

* ##### 변수의 선언이나 메서드의 매개변수를 하나의 참조 자료형이 아닌 여러 자료형으로 변환될 수 있도록 프로그래밍 하는 방식
* ##### 실제 사용되는 참조 자료형으로의 변환은 컴파일러가 검증하므로 안정적인 프로그래밍 방식

<br>

 #### :triangular_flag_on_post: 제네릭 프로그래밍의 효용:
 * ##### 모든 데이터 타입을 수용하기위해 or 중복을 제거하기위해 Object를 데이터 타입으로두면, 엉뚱한 data type이 오는 것을 수용해버릴수도..
    #####   그건, 변수의 베이터 타입을 제한해서 얻을 수 있는 type 안정성을 잃어버릴수도 있다는 것을 의미.
    #####   타입이 안전해질 수 있고,  코드의 중복을 제거할 수도 있는 '제네릭'이용.
 * ##### 컬렉션에 저장된 여러 종류의 객체를 꺼내서 사용할 때, 객체의 종류에 따라 매번 형변환을 해야하기 때문에 코드가 복잡해지는데 제네릭을 이용하면 타입 변환을 따로 하지 않아도 된다.
 ```java 
 //제네릭 사용 x
 List list = new ArrayList();
 liat.add("Hello");
 String str = (String)list.get(0);
 ```
 ```java
 //제네릭 사용
 List<String> list = new ArrayList<String>();
 liat.add("Hello");
 String str = list.get(0);  //(형변환 필요 없음)
 ```
  #
 ##### :triangular_flag_on_post: ( 주의 )제네릭은 참조 자료형만 가능, 기본 자료형 (int, char ...) 은 자바 안에서 객체가 아니기 때문에 불가능. 
  #####     => 기본 데이터 타입의 제네릭 사용법?
  #####        객체인 것 처럼 꾸미는 객체를 이용 [Wrapper](https://github.com/6161990/TIL/blob/main/Java/String%2C%20Wrapper%20Class.md)

#

<br>

#### :round_pushpin: 자료형 매개변수 <T>
##### 여러 참조 자료형으로 대체될 수 있는 부분을 하나의 문자로 표현
##### (type의 의미로 대개 T 사용)
            클래스형 : public class GenericPrinter<T>{
                       private T mateial;
            }
            
            매개변수 형 : public void setMaterial(T material){
                          this.material = material;
            }
            반환형: public T getMaterial(){
                    return material;
            }

<br>


#### :round_pushpin: 제네릭과 상속 <T extends 클래스> (interface)
##### T 대신에 사용될 자료형을 제한하기 위해 사용. 
##### 중괄호 {}안에서 타입 파라미터 변수로 사용 가능한 것은 상위탕비의 멤버(필드, 메소드)로 제한되어, 하위 타입에만 있는 필드와 메소드는 사용할 수 없다. 
#### class extends
```java
abstract class Info{                   //abstract 
  public abstract int getLevel();
}
class EmployeeInfo extends Info{      //추상 클래스를 상속하기
  public int rank;
  
  EmployeeInfo(int rank){ 
    this.rank = rank;
  }
  public int getLevel(){
    return this.rank; 
  }
}
class Person<T extends Info> {      //제네릭 T로 올 수 있는 데이터타입은 1. Info 2. EmployeeInfo
  public T info;
  Person (T info){
    this.info = info;
  }
  
  public class GenericDemo{
    public static void main(String[] args){
      Person<EmployeeInfo> p1 = new Person<EmployeeInfo>(new EmployeeInfo(1));        
      Person<String> p2 = new Person<String>("부정");       //but, <String> 은 아님. Person은 Info의 상속이니까. Error
     } 
  }
```
**interface extends**
```java
interface Info{         //interface
  int getLevel();
}
class EmployeeInfo implements Info{      //interface를 실현하는 implements
  public int rank;
  EmployeeInfo(int rank){ 
    this.rank = rank;
  }
}
class Person<T extends Info> {          //그럼 얘도 implements여야 하는거 아닌가?
  public T info;                        //Nope! 서 'extends'는 상속이 아니라 부모가 누군지 알려주는 역할
  Person (T info){
    this.info = info;
  }
  
  public class GenericDemo{
    public static void main(String[] args){
      Person<EmployeeInfo> p1 = new Person<EmployeeInfo>(new EmployeeInfo(1));
      Person<String> p2 = new Person<String>("부정");
     } 
  }
```

<br>

#### :round_pushpin: 자료형 매개 변수가 두 개 이상일 때
```java
public class Point<T, V>{
  private T x;
  private V y;
  
  Point(T x, V y){
    this.x = x;
    this.y = y;
  }
  
  public T getX(){    //제너릭 메서드
    return x;
  }
  public V getY(){    //제너릭 메서드
   rerturn y;
  }
}
```

<br>

#### :round_pushpin: 제너릭 메서드
* ##### 일반 클래스에서 쓰일 수 있음. 
* ##### 메서드의 매개 변수를 자료형 매개 변수로 사용하는 메서드
```java
ArrayList<Book> list = new ArrayList<Book>();  //제네릭이 설정된 레퍼런스 
BookManager bm = new BookManager();
bm.printInfomation(list);

//BookManager의 클래스
public void printInformation(ArrayList<Book> list){  // 가 인자로 넘어올 때 
	...
}
```
##### => 제네릭이 설정된 레퍼런스를 인자로 넘기는 경우 메소드 쪽에서 받아주는 매개변수도 제네릭이 적용되어야 한다. 
```java
public class GenericMethod{
  public static <T, V> double makeRectangle(Point<T, V> p1, Point<T, V> p2){
    double left = ((Number)p1.getX()).doubleValue( );
    double right = ((Number)p2.getX()).doubleValue( );
    double top = ((Number)p1.getY()).doubleValue( );
    double bottom = ((Number)p2.getY()).doubleValue( );
    
    double width = right - left;
    double height = bottom - top;
    
    return width * height;
  }
}
```
* ##### 메세드 내에서의 매개 변수는 메서드 내에서만 유효함. (지역 변수와 같은 개념)  

           class Shape<T>{
                public static <T, V> double makeRectangle(Point<T, V>p1, Point<T, v> P2){
                    ...
                }
            }
  #####  => Shape의 makeRectangle의 T는 전혀 다른 의미 

<br>

#### :round_pushpin: 제네릭의 생략
```java
class EmployeeInfo{
  public int rank;
  EmployeeInfo(int rank){ this.rank = rank;}
  }
class Person<T, S> {
  public T info;
  public S id;
  Person (T info, S id){
    this.info = info;
    this.id = id;
  }
  
  public <U> void printInfo(U info){
    System.out.println(info);
  }
  public class GenericDemo{
    public static void main(String[] args){
      EmployeeInfo e = new EmployeeInfo(1);
      Integer i = new Integer(10);
      
      // = Person p1<EmployeeInfo,Integer> = new Person<EmployeeInfo,Integer>((1),id);
      Person p1 = new Person(e,i);    // 명시 없어도 자바가 제네릭임을 유추
     } 
  }
}
```

<br>

------------------------------------------------------

### :computer: 프로그래밍해보기
#### 제네릭을 이용한 3D 프린팅 프로그래밍
**전체 재료 관리 : 여기서 상속 받은 재료만 3D프린팅 가능하도록 제한하기 위해**
```java
public abstract class Meterial {
	public abstract void doPrinting(); 
}
```
**플라스틱 재료**
```java
public class Plastic extends Meterial{

	public String toString() {
		return "재료는 Plastic 입니다";
	}

	@Override
	public void doPrinting() {
		System.out.println("Plastic으로 프린팅 합니다");		
	}
}
```
**파우더 재료**
```java
public class Powder extends Meterial{

	public String toString() {
		return "재료는 Powder 입니다";
	}

	@Override
	public void doPrinting() {

		System.out.println("Powder로 프린팅 합니다");
	}
}
```

**물 재료(3D로 프린팅 불가능한 재료. 즉, 제한되어야 하는 제네릭)**
```java
  public class Water {}   //Meterial 상속 받지 못함.
```
**3D 프린터기**
```java
public class GenericPrinter<T extends Meterial> {

	private T material;

	public T getMaterial() {
		return material;
	}

	public void setMaterial(T material) {
		this.material = material;
	}
	
	public String toString() {
		return material.toString();
	}
	
	public void printing() {
		material.doPrinting();
	}
}
```
**테스트**
```java
public class GenericPrinterTest {

	public static void main(String[] args) {

		GenericPrinter<Powder> powderPrinter = new GenericPrinter<Powder>();
		Powder powder = new Powder();
		powderPrinter.setMaterial(powder);
		System.out.println(powderPrinter);
		
		GenericPrinter<Plastic> plasticPrinter = new GenericPrinter<Plastic>();
		Plastic plastic = new Plastic();
		plasticPrinter.setMaterial(plastic);
		System.out.println(plasticPrinter);
		
		powderPrinter.printing();
		plasticPrinter.printing();
		
		GenericPrinter printer = new GenericPrinter();  //제네릭 생략, 많이 쓰이진 않음.
	}
}
```



