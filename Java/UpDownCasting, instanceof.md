## :pushpin: DownCasting 다운캐스팅
 * #### 하위 클래스로의 형 변환.
 * #### 묵시적으로 상위 클래스 형변환된 인스턴스가 원래 자료형(하위 클래스)으로 변환되어야 할 때,
 * #### (가상함수 작용으로 원래 인스턴스의 메서드를 사용할 수 없을 때) 
 * #### 하위 클래스로의 형 변환은 명시적으로 되어야 함.
     * #### 묵시적인 업 캐스팅: Customer vc = new VIPCustomer();
     * #### 명시적인 다운캐스팅:VIPCustomer vCustomer = (VIPCustomer)vc;  
   #### But, 위 방법은 오류가 날 수도 있음. 인스턴스에 맞지않는 형 변환을 하려고 시도할 때. 
            Rabbit humanWalking = (Rabbit)human;

---------------------------------
* ###### 참고 [객체지향프로그래밍](https://github.com/6161990/TIL/blob/main/Java/Object-Oriented%20Programming(OOP).md#1-%ED%81%B4%EB%9E%98%EC%8A%A4-%ED%98%95%EB%B3%80%ED%99%98-up-casting-%EC%9E%91%EC%9D%80-%EA%B2%83%EC%97%90%EC%84%9C-%EB%A7%8E%EC%9D%80-%EA%B2%83%EC%9C%BC%EB%A1%9C-%ED%95%99%EC%9E%A5)
```java

public class CastingTest {

	public static void main(String[] args) {
		//Person = 부모 , President/Student = 자식

		
		President president1 = new President();
		//president1 객체를 상위클래스인 Person 클래스 레퍼런스 변수에 참조시킴.
		
		//부모가 아직 생성되지 않은 상태면 다른 타입을 참조가능하다. 
		Person person1 = president1; //자식이 가지고 있는 변수 , 메소드는 사라짐 (축소)
		//persident1 객체가 자동으로 Person 타입으로 UpCasting 되면서 참조됨.
		
		
		President president2 = (President)person1; 
		//(확장) down. person1이 객체가 생성되지 않았기 때문에 가능(heap에 메모리공간이 아직 만들어지지 않았기 때문에)
		//person1 레퍼런스 변수의 참조값을 President 타입의 레퍼런스 변수에 할당함
		//부모 클래스 타입의 참조값을 자식 클래스 타입의 참조변수에 할당하므로 명시적 캐스팅
		
		
		
		Person person2 = new Person();
		//객체생성
		System.out.println(person2.getAge());
		
		President president3 = new President();
		//president3 = (President)person2; // 이미 person 의 메모리 공간이 19라인에서 만들어졌기때문에 불가능. 13라인과 대조적.
		//Person의 객체를 President 타입의 레퍼런스 변수에 참조시킴
		
		//Student student = (Student) president2;
		//같은 부모클래스를 상속받는 클래스 타입끼리 캐스팅. 불가. 같은 층위에서 업다운 캐스팅불가.
		//상속관계에서만 업다운 캐스팅이 가능하다. 
		
		//President president4 = new Student();
	}

}

```
 ```java
 public class InstanceOfTest {

	public static void main(String[] args) {
		//Person = 부모 , President/Student = 자식
		
		President president1 = new President();
		
		Person person1 = president1;
		
		if(person1 instanceof President) {
			President president2 = (President) person1;
			System.out.println("person1을 President타입으로 캐스팅성공");
		}else {
			System.out.println("person1을 캐스팅 할 수 없다.");
		}
		
		Person person2 = new Person();
		if(person2 instanceof President) {
			President president3 = (President) person2;
			System.out.println("person2를 President타입으로 캐스팅 성공");
		}else {
			System.out.println("person2를 캐스팅할 수 없다.");
		}
	
	}

		
}

 ```
-----------------------------------------------------------------

### :computer: 프로그래밍하기 
#### 다형성을 이용해 다운캐스팅 적용하기
	    
 ```java    
   public class Animal {

	public void eat() {
		System.out.println("동물이 먹습니다.");
	}
}
class Human extends Animal{
	public void eat() {
		System.out.println("사람은 젓가락을 사용합니다");
	}
	public void walking() {
		System.out.println("사람은 걷습니다.");
	}
}
class Rabbit extends Animal{
	public void eat() {
		System.out.println("토끼는 발을 이용합니다.");
	}
	public void jumping() {
		System.out.println("토끼는 껑충껑충뜁니다.");
	}
}
class Fish extends Animal{
	public void eat() {
		System.out.println("물고기는 물어뜯습니다.");
	}
	public void swimming() {
		System.out.println("물고기는 유유히 헤엄칩니다.");
	}

} 
 ```   
  ```java    
public class AnimalTest {

     public static void main(String[] args) {
	Animal human = new Human();           //변수 human은 Human소속.
	Animal rabbit = new Rabbit();
	Animal fish = new Fish();
		
	Human humanWalk = (Human)human;        //Animal에서 Human으로 다운 캐스팅.
	humanWalk.walking();
    
   	Rabbit humanWalking = (Rabbit)human;   //But, Rabbit으로 다운 캐스팅 시도하려고 하면, 빨간색 줄은 안뜨지만 컴파일 에러가 남. 
    }
}
 ```   
 #
#### :triangular_flag_on_post: 컴파일 에러를 피하는 방법:  **'instanceof'** true/false를 반환. 
 ```java    
 public class AnimalTest {

    public static void main(String[] args) {
	Animal human = new Human();                   
	Animal rabbit = new Rabbit();
	Animal fish = new Fish();
		
	Human humanWalk = (Human)human; 	//instanceof를 사용하지 않은 것과 
	humanWalk.walking();
    
    if(human instanceof Human) {              	//instanceof를 사용한 것.
	Human humanWalking = (Human)human;    
	humanWalking.walking();
    }  
  }
}
 ``` 
 
 <br>
 
 #### :triangular_flag_on_post: instanceof가 하는 일
 #### A instanceof B : A가 정말 B의 인스턴스였느냐!!!! 대답으로 true/false를 반환.
 #### 매개변수가 잘못 넘어올 수 있기 때문에 안정적으로 하기 위해서 사용. 
 
 <br> 
### :computer: 프로그래밍하기      
#### instanceof를 이용해 각자가 가진 차별 메소드 출력하기 (Animal)
  ```java    
public class AnimalTest {

   public static void main(String[] args) {
	Animal human = new Human();                   
	Animal rabbit = new Rabbit();
	Animal fish = new Fish();
		
	ArrayList<Animal> animalList = new ArrayList<Animal>();
	animalList.add(human);
	animalList.add(rabbit);
	animalList.add(fish);
		
	AnimalTest test = new AnimalTest();
	test.testDownCasting(animalList);
	}
    
  public void testDownCasting(ArrayList<Animal> list) {
	for(int i=0; i<list.size(); i++) {
	Animal animal = list.get(i);
			
	if(animal instanceof Human) {
	  Human humanWalking = (Human)animal;
	  humanWalking.walking();
	}else if(animal instanceof Rabbit) {
	  Rabbit rabbitJumping = (Rabbit)animal;
	  rabbitJumping.jumping();
	}else if(animal instanceof Fish) {
	  Fish fishSwimming =(Fish)animal;
	  fishSwimming.swimming();
	}else {
	  System.out.println("error");
	}
    }
 }
  
}
 ``` 
 
