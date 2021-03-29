### :pushpin: this
* ###### 참고 : [객제 지향 언어 OOP](https://github.com/6161990/TIL/blob/main/Java/Object-Oriented%20Programming(OOP).md), [객제 지향 언어의 메모리 구조와 특징](https://github.com/6161990/TIL/blob/main/Java/OOP%20Memory.md)
# 
* #### 모든  인스턴스의 메소드에 숨겨진 채 존재하는 레퍼런스로, 할당된 객체를 가르킨다. 
* #### 사용 이유 : 자기 자신의 클래스 내부에 있는 변수, 메서드, 생성자함수를 재사용하기 위해 사용한다.
* #### 함수 실행시 전달되는 객체의 주소를 자동으로 받는다.
* #### 성자에서 다른 생성자를 호출함.
	###### 생성자 오버로딩에서 한 생성자가 다른 생성자 호출하는 경우. 
* #### 인스턴스 자신의 주소를 반환.
  
   <br>
   
 #### :round_pushpin: this역할1. 자신의 메모리를 가리킴. 같은 생성자를 만들어도 둘의 인스턴스 주소는 다름(date & date2)

```java
public class MyDateTest {

      public static void main(String[] args) {
      MyDate date = new MyDate(); // 여기 date 
       
      date.setYear(2019);
      date.setMonth(77);
      date.setDay(100);
    
      date.showDate();
    
      MyDate date2 = new MyDate(); // 여기 date2의 주소는 다름. 
      date2.setYear(2002);  
    
      date2.showDate();
    }
}
```

   <br>
   
#### :round_pushpin: this역할2. 같은 클래스의 다른 생성자를 호출할 때, 반드시 첫번째 줄에서.

```java
public class Person {

      String name;
    	int age;
    	
    	public Person() {
	 //age = 20 ; 불가. why? 다른 statement 올 수 없음. this로 다른 생성자를 호출할 때, first statement여야 하기때문에.
    	  this("이름없음" ,1);  // 여기서 다른 Person 생성자를 호출. 
    	}
    	
    	public Person(String name, int age) {
    	  this.name = name;
          this.age = age;
    	}
    	
    	public void showInfo() {
    	  System.out.println(name+","+age);
    	}
      
      
        public static void main(String[] args) {
		
	      Person personNoName=new Person();
	      personNoName.showInfo();
	      	
	      Person personLee = new Person("Lee",20);
	      personLee.showInfo();
	      
    }
}
```    
   <br>
   
#### :round_pushpin: this역할3. 자신의 주소를 반환하는 this

```java
public class Person {

      String name;
    	int age;
    	
    	public Person() {
    		this("이름없음" ,1);  
    	}
    	
    	public Person(String name, int age) {
    		this.name = name;
    		this.age = age;
    	}
    	
    	public void showInfo() {
    		System.out.println(name+","+age);
    	}
      
         public Person getSelf(){ // this를 반환하는 메소드의 반환타입은 자기자신
           return this;
         }
      
      public static void main(String[] args) {
		
	     Person personNoName=new Person();
	     personNoName.showInfo();
	      	
	     Person personLee = new Person("Lee",20);
	     personLee.showInfo();
	     System.out.println(personLee);  //인스턴스 주소값 출력 : chapter5.Person@2ff4acd0   
        
             Person p = personLee.getSelf();
             System.out.println(p); //인스턴스 주소값 출력 : chapter5.Person@2ff4acd0   
        
             // 주소 값  : 참조변수와 this가 가리키는 힙 메모리는 같다. 
	}
    
}
```

<br>

------------------------------------------------------------------

### :computer: 프로그래밍 해보기

<br>

```java

public class House {
	//this? 자기 자신의 클래스 내부에 있는 변수, 메서드, 생성자함수를 재사용하기 위해 사용
	
	public int price;  //가격
	public String dong;  //아파트 (동)
	public int size;  //평수 
	public String kind;  //빌라, 아파트 
	
	public House() {
		//this() : 생성자 함수 
		//생성자 함수 내에서 자신의 클래스 내에 있는 다른 생성자 함수를 재사용하겠다. 
		this(100,32,"동판교","오피스텔");  
//		price = 100;
//		size =32;
//		dong = "동판교";
//		kind = "아파트";
	}
	
	public House(int price) {
		//지역변수가 우선순위가 높기 때문에 자기 자신 클래스의 변수를 가리키는 this를 명시해주어야한다.
		//this.price=price; //but 이것은 효율이 떨어짐
		this(price,32,"동판교","빌라");  //thid()함수를 사용
	}
	
	public House(int price, int size) {
		this(price, size, "동판교", "주상복합");
	}
	public House(int price, int size, String dong) {
		this(price, size, dong, "아파트");
	}
	
	public House (int price, int size, String dong, String kind) {
		//this. : 변수, 메소드
		this.price = price;
		this.size = size;
		this.dong = dong;
		this.kind = kind;
	}

}

```
```java
public class HouseConstructorTest {

	public static void main(String[] args) {
		House house1 = new House();
		System.out.println(house1.price+":"+house1.size+":"+house1.dong+":"+house1.kind);  //100:32:동판교:오피스텔
	
		House house2 = new House(300);
		System.out.println(house2.price+":"+house2.size+":"+house2.dong+":"+house2.kind); //300:32:동판교:빌라
		
		House house3 = new House(600,40);
		System.out.println(house3.price+":"+house3.size+":"+house3.dong+":"+house3.kind); //600:40:동판교:주상복합

		House house4 = new House(800,50,"서초동");
		System.out.println(house4.price+":"+house4.size+":"+house4.dong+":"+house4.kind); //800:50:서초동:아파트
		
		
		House house5 = new House(10000,50,"서초동","펜트하우스");
		System.out.println(house5.price+":"+house5.size+":"+house5.dong+":"+house5.kind); //10000:50:서초동:펜트하우스
	}

}

```




