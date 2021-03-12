## :pushpin: Class 클래스
### class 이름 자체가 Class임.
* #### 자바의 모든 클래스와 인터페이스는 컴파일 후 class 파일로 생성됨
* #### class 파일에는 객체의 정보(멤버변수, 메서드, 생성자 등)가 포함되어 있음.
* #### Class 클래스는 컴파일된 class 파일에서 객체의 정보를 가져올 수 있음.

<br>

#### :round_pushpin: Class 클래스 가져오기
##### 1.String s = new String();
#####   Class c = s.getClass();  // getClass()는 Object의 메소드 
##### 2. Class c = String.Class;  => 컴파일 된 상태로 있는 경우
##### 3. Class c = Class.forName("java.lang.String");  // 동적로딩
* ###### 장점 : runtime 시 로딩이 된다. 
  ######       쓰이는 경우) JDBC의 라이브러리 모두 링크할 수 없으니까, 내가 필요할 때 원하는 라이브러리를 불러올 수 있다. 
* ###### 단점 : runtime시, 오타가 나있다면 로딩이 죽을 수도 있다. 

<br>

#### :round_pushpin: 동적로딩
##### 자바 안에 모든 constructor를 가져오기
```java    
public class Class {

	public static void main(String[] args) throws ClassNotFoundException {
		Class c3 = Class.forName("java.lang.String");
		
		Constructor[] cons = c3.getConstructors();
		for(Constructor con: cons) {
			System.out.println(con);
		}
		
		System.out.println();
    
    Method[] methods = c3.getMethods();       //Method는 java.lang.reflect.Method;의 Method. 
		for(Method  method : methods) {     
			System.out.println(method);
		}
	}
}
 ```   
 ##### => 클래스 가져오기의 다른 쉬운 방법이 있기 때문에 특별한 상황이 아닌 이상, 잘 쓰지 않음. 
 
<br>

#### :round_pushpin: reflection 프로그래밍
* ##### Class 클래스로부터 객체의 정보를 가져와 프로그래밍하는 방식
* ##### 로컬에 객체가 없고 자료형을 알 수 없는 경우 유용한 프로그래밍, 그렇지 않고서는 많이 쓰이지 않음.
* ##### java.lang.reflect 패키지에 있는 클래스 활용

<br>

#### :round_pushpin: new Instance()메서드
##### Class 클래스 메서드, new 키워드를 사용하지 않고 인스턴스를 생성.

**클래스를 가져오는 두 가지 방법**
```java    
public class ClassTest {

	public static void main(String[] args) throws ClassNotFoundException, InstantiationException, 
							IllegalAccessException, NoSuchMethodException, SecurityException, IllegalArgumentException, InvocationTargetException{


    //static으로 해놓고 가져와서 쓰는 쉬운 방법.
		Person person = new Person("James");          
		System.out.println(person);
		
    
    // 내가 필요할 때 불러서 쓰는 동적 로딩 방법. 
    //디폴트 construct
		Class c1 = Class.forName("classex.Person");   
		Person person1 = (Person)c1.newInstance();          //**new Instance()메서드, 디폴트 컨스트럭트를 생성함**
		System.out.println(person1);                        //null이 나옴
		
    
    //매개변수있는 construct
		Class[] parameterTypes = {String.class};	       // 2. 가져오려는 Constructor의 매개변수의 타입을 써줘야함. 
		Constructor cons = c1.getConstructor(parameterTypes);  // 1. 매개변수 있는 걸 가져오려면, Constructor를 우선 한번가져와야함.
		
		Object[] initargs = {"이동동"};			       //3. personLee에 넣을 매개변수를 initargs에 담아라
		Person personLee = (Person)cons.newInstance(initargs);   //3. Object에서 (Person)으로 형변환을 해 personLee에 매개변수를 담아라
		System.out.println(personLee);
	
	}
}
 ``` 

<br>

#### :round_pushpin: forName()메서드와 동적로딩
##### Class 클래스 static 메서드
##### 동적로딩?
##### => 컴파일 시에 데이터 타입이 모두 binding 되어 자료형이 로딩되는 것(static loding)이 아니라 (Person person = new Person("James");),
#####    실행 중에 데이터 타입을 알고 binding 되는 방식.
##### => 실행 시에 로딩되므로 경우에 따라 다른 클래스가 사용될 수 있어 유용함
##### => 컴파일 타임에 체크할 수 없으므로 해당 문자열에 대한 클래스가 없는 경우,
#####    예외(Class Not Found Exception)이 발생할 수 있음.
