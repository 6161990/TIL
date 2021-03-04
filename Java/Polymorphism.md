### Polymorphism 다형성
* ###### 하나의 코드가 여러 자료형으로 구현되어 실행되는 것.같은 코드인데도 실행 결과는 여러개. 
* ###### 객체지향 프로그래밍의 유연성, 재활용성, 유지보수성에 기본이 되는 특징임. 
* ###### 여러클래스가 하나의 데이터 타입으로 묶여 한 코드로 여러 클래스의 실행 결과를 출력할 수 있음. 
* ###### 다양한 여러 클래스를 하나의 자료형(상위 클래스)로 선언하거나, 형 변환하여 각 클래스가 동일한 메서드를 오버라이딩 한 경우.
  ###### 하나의 코드가 다양한 구현을 실행할 수 있음. 
* ###### 다형성의 장점 : 유사한 클래스가 추가되는 경우 유지보수에 용이하고, 각 자료형마다 다른 메서드를 호출하지 않으므로 코드에서 많은 if문이 사라짐.
* ###### 다형성의 원리 : 상속, 형 변환, 오버라이딩, 가상함수를 이용해 객체지향 프로그래밍을 한다. 
             1. 상속-> 
                 2. overriding을 통한 재정의 -> 
                      3. 형 변환 (업 캐스팅) -> 
                          4. 가상함수 을 이용한 유기적 연결이 있음. 


**다형성을 이용해 동물들의 습성 프로그래밍**
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
		Animal human = new Human();                        // 3. 형 변환 (업 캐스팅) -> Animal human = new Human(); 상위 클래스로 묶어서 UPCASTING
		Animal rabbit = new Rabbit();                      // 4. 가상함수 : 오버라이딩 되었을 때 메소드의 호출리 인스턴스에서 불려진다.
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
**다형성으로 구현하면 ArrayList,enhanced for문을 이용해 출력 가능해짐**
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

#

**S-A(상속)와 HAS-A(composition)**
* ###### S-A관계( is a relationship : inheritance)
###### 일반적인(general)개념과 구체적인(specific) 개념과의 관계가 성립될 때 써야함.
###### 단순한 코드의 재사용이 아님 

* ###### HAS-A (composition) :
###### 한 클래스가 다른 클래스를 소유한 관계.
###### 내가 필요한 클래스가 있다고 하면 그 클래스를 포함해서 쓰는 방식
###### ArrayList가 필요하다고해서 그 ArrayList 클래스를 따로 생성해 사용하지 않고 클래스 내부에서 사용하는 것처럼.    

###### =>설계 단계에서 상속을 사용할 것인지 일반 HAS로 갈 것인지 잘 생각해야함.
######   상속으로 갈거면 어떤 메소드를 오버라이딩(재정의)할 것인지도...!
