### :pushpin: Polymorphism 다형성
* ###### 참고 : [객제 지향 언어 OOP](https://github.com/6161990/TIL/blob/main/Java/Object-Oriented%20Programming(OOP).md), [객제 지향 언어의 메모리 구조와 특징](https://github.com/6161990/TIL/blob/main/Java/OOP%20Memory.md)
* ##### 상속을 이용해 부모 타입으로부터 파생된 여러가지 타입의 자식 객체를 부모 클래스 타입 하나로 다룰 수 있음. (여러클래스가 하나의 데이터 타입으로 묶인다)
* ##### 객체지향 프로그래밍의 유연성, 재활용성, 유지보수성에 기본이 되는 특징임. 
* ##### 다양한 여러 클래스를 하나의 자료형(상위 클래스)로 선언하거나, 형 변환하여 각 클래스가 동일한 메서드를 오버라이딩 한 경우.
  ##### 하나의 코드가 다양한 구현을 실행할 수 있음. 
* ##### 다형성의 장점 : 유사한 클래스가 추가되는 경우 유지보수에 용이하고, 각 자료형마다 다른 메서드를 호출하지 않으므로 코드에서 많은 if문이 사라짐.
* ##### 다형성의 원리 : 상속, 형 변환, 오버라이딩, 가상함수를 이용해 객체지향 프로그래밍을 한다. 
             1. 상속-> 
                 2. overriding을 통한 재정의 -> 
                      3. 형 변환 (업 캐스팅) -> 
                          4. 가상함수 을 이용한 유기적 연결이 있음. 


<br>

#### :triangular_flag_on_post: 객체의 다형성
```java

public class ChildMethodCall {

	public static void main(String[] args) {
		//부모 Person, 자식 Student
		
		//Person person = new Student(); 와 아래 두 줄은 같다.
		Student student = new Student();
		Person person = student;
		
	//error person.study(); 이건 오버라이드 안했음. 일반 함수임(Student에서)
		person.showSleepStyle(); //이건 오버라이드 해놓았음. (Student에서)  
    	// 	=> 학생의 showSpeepStyle가 출력됨
		
		
	}

}

```
```java
public class OverridingTest {

	public static void main(String[] args) {
		//부모 Person, 자식 Employee
		
		Employee employee = new Employee();
		Person person = employee;
		System.out.println("employee="+ employee.x); 	//employee=500
		System.out.println("person="+ person.x); 	//person=0
		employee.sleep();
		person.sleep(); 
	 // => 직장인 클래스의 sleep 메소드가 출력
     	// => 다른 코딩인데 결과가 같다. 
	
	}

}
```

<br>

#### :triangular_flag_on_post: 매개변수(파라미터)의 다형성
```java

public class PersonInfo {
	public void showSleepingType(Person person) { 
	//Person person = (Person) employee, student, president
	
	person.showSleepStyle();
	}

}
```
```java

public class ParameterPolyTest {
 
	public static void main(String[] args) {
		PersonInfo pf = new PersonInfo();
		Person person = new Person();
		Employee employee = new Employee();
		Student student = new Student();
		President president = new President();
		pf.showSleepingType(person);
		pf.showSleepingType(employee);
		pf.showSleepingType(student);
		pf.showSleepingType(president);
	}

}
```

#### :triangular_flag_on_post: 배열의 다형성
```java

public class ArrayPolyTest {
 
	public static void main(String[] args) {
		//부모 Person, 자식 Employee,Student,President
		
		Person[] pArray = new Person[3];
		
		pArray[0] = new Employee(); //Employee가 재정의한 메소드가 출력
		pArray[1] = new Student();  //Employee가 재정의한 메소드가 출력
		pArray[2] = new President(); //Employee가 재정의한 메소드가 출력
		for(int i =0; i<pArray.length;i++) {
			pArray[i].showSleepStyle();
		}		
	}
}
```
-----------------------------------
### :computer: 프로그래밍하기
#### 다형성을 이용해 동물들의 습성 프로그래밍
```java    
public class Animal {

	public void eat() {
		System.out.println("동물이 먹습니다.");
	}
}

class Human extends Animal{
	public void eat() {
		System.out.println("사람은 젓가락을 사용합니다");         // 1. 상속-> Animal을 Human,Rabbit,Fish가 각각 상속.
	}                                                               // 2. overriding을 통한 재정의 
}
class Rabbit extends Animal{
	public void eat() {
		System.out.println("토끼는 발을 이용합니다.");
	}
}
class Fish extends Animal{
	public void eat() {
		System.out.println("물고기는 물어뜯습니다.");
	}
}
``` 
```java    
public class AnimalTest {
	public static void main(String[] args) {
		Animal human = new Human();       // 3. 형 변환 (업 캐스팅) -> Animal human = new Human(); 상위 클래스로 묶어서 UPCASTING
		Animal rabbit = new Rabbit();     // 4. 가상함수 : 오버라이딩 되었을 때 메소드의 호출리 인스턴스에서 불려진다.
		Animal fish = new Fish();
		
		AnimalTest test = new AnimalTest();
		test.eatAnimal(human);
		test.eatAnimal(rabbit);
		test.eatAnimal(fish);
	}

	public void eatAnimal(Animal animal) {
		animal.eat();
	}
}
``` 

#

#### 다형성으로 구현하면 ArrayList,enhanced for문을 이용해 출력 가능해짐
```java    
public class AnimalTest {
	public static void main(String[] args) {
		Animal human = new Human();                                   
		Animal rabbit = new Rabbit();                                 
		Animal fish = new Fish();
		
	ArrayList<Animal> animalList = new ArrayList<Animal>();         //ArrayList에 담아 for문으로 돌려서 출력 
		animalList.add(human);
		animalList.add(rabbit);
		animalList.add(fish);
		
		for(Animal animal : animalList) {
			animal.eat();
		}
	}

	public void eatAnimal(Animal animal) {
		animal.eat();
	}
}
``` 

<br>

### :round_pushpin: IS-A(상속)와 HAS-A(composition)
* #### IS-A관계( is a relationship : inheritance)
  * ##### 일반적인(general)개념과 구체적인(specific) 개념과의 관계가 성립될 때 써야함.
  * ##### 단순한 코드의 재사용이 아님 

* #### HAS-A (composition) :
  * ##### 한 클래스가 다른 클래스를 소유한 관계.
  * ##### 내가 필요한 클래스가 있다고 하면 그 클래스를 포함해서 쓰는 방식
  * ##### ArrayList가 필요하다고해서 그 ArrayList 클래스를 따로 생성해 사용하지 않고 클래스 내부에서 사용하는 것처럼.
```java
//부분(점)
public class Point {
	
	int x, y;

}

```
```java
//Has-a 관계 (소유, 포함의 관계)
//전체(원)
public class Circle {
	
	Point p;
	int r;
	
	public Circle() {
		p = new Point();
	}

	public static void main(String[] args) {
		Circle c = new Circle();
		c.p.x=10;
		c.p.y=10;
		c.r=5;
		System.out.println(c.p.x);
		System.out.println(c.p.y);
		System.out.println(c.r);
	}
}
```

#### :triangular_flag_on_post: 설계 단계에서 상속을 사용할 것인지 일반 HAS로 갈 것인지 잘 생각해야함.
####    상속으로 갈거면 어떤 메소드를 오버라이딩(재정의)할 것인지도...!
