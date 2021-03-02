### this
* ###### 자신의 메모리를 가리킴.
* ###### 셍성자에서 다른 생성자를 호출함.
 ###### 생성자 오버로딩에서 한 생성자가 다른 생성자 호출하는 경우. 
* ###### 인스턴스 자신의 주소를 반환.
   
   
**this역할1. 자신의 메모리를 가리킴. 같은 생성자를 만들어도 둘의 인스턴스 주소는 다름(date & date2)**   

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


**this역할2. 생성자에 다른 생성자를 호출**   

```java
public class Person {

      String name;
    	int age;
    	
    	public Person() {
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
```   

**this역할3. 자신의 주소를 반환하는 this**   

```java
public class Person {

      String name;
    	int age;
    	
    	public Person() {
        //age = 20 ; 불가. why? 다른 statement 올 수 없음. this로 다른 생성자를 호출할 때, first statement여야 하기때문에.
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





