### DownCasting 다운캐스팅
 ###### 하위 클래스로의 형 변환.
 ###### 묵시적으로 상위 클래스 형변환된 인스턴스가 원래 자료형(하위 클래스)으로 변환되어야 할 때,
 ###### 하위 클래스로의 형 변환은 명시적으로 되어야 함.
    묵시적인 업 캐스팅: Customer vc = new VIPCustomer();
    명시적인 다운캐스팅:VIPCustomer vCustomer = (VIPCustomer)vc;  
 ###### But, 위 방법은 오류가 날 수도 있음. 인스턴스에 맞지않는 형 변환을 하려고 시도할 때. 
            Rabbit humanWalking = (Rabbit)human;
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
		Animal human = new Human();                   //변수 human은 Human소속.
		Animal rabbit = new Rabbit();
		Animal fish = new Fish();
		
		Human humanWalk = (Human)human;               //Animal에서 Human으로 다운 캐스팅.
		humanWalk.walking();
    
    Rabbit humanWalking = (Rabbit)human;          //But, Rabbit으로 다운 캐스팅 시도하려고 하면, 빨간색 줄은 안뜨지만 컴파일 에러가 남. 
	}
}
 ```   
 #
###### 그래서 쓰이는 방법이 **'instanceof'** true/false를 반환. 
 ```java    
  public class AnimalTest {

	public static void main(String[] args) {
		Animal human = new Human();                   
		Animal rabbit = new Rabbit();
		Animal fish = new Fish();
		
		Human humanWalk = (Human)human;             //instanceof를 사용하지 않은 것과 
		humanWalk.walking();
    
    if(human instanceof Human) {              //instanceof를 사용한 것.
			Human humanWalking = (Human)human;    
			humanWalking.walking();
		}  
	}
}
 ``` 
      instanceof가 하는 일 
     A instanceof B : A가 정말 B의 인스턴스였느냐!!!! 대답으로 true/false를 반환.
     매개변수가 잘못 넘어올 수 있기 때문에 안정적으로 하기 위해서 사용. 
     
 **instanceof를 이용해 각자가 가진 차별 메소드 출력하기**
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
 
