## :pushpin: 예외 Exception
<img src="https://user-images.githubusercontent.com/74708028/110581279-9390d580-81ad-11eb-837c-5d74a03f35b1.jpg" width="500" height="300">

<br>

### :round_pushpin: 오류란 무엇인가?
* #### 컴파일 오류 :  프로그램 코드 작성 중 발생하는 문법적 오류
* #### 실행 오류 : 실행 중인 프로그램이 의도하지 않은 동작을 하거나 (bug), 프로그램이 중지되는 오류 (runtime error)
  ##### 자바는 예외 처리를 통하여 프로그램의 비정상 종료를 막고 log를 남길 수 있음
  ##### log를 잘 남겨야 예외 처리가 수월함
  
  <br>
  
### :round_pushpin: 오류와 예외 클래스
* #### 시스템 오류 (error) : 가상 머신에서 발생, 프로그래머가 처리할 수 없음
  ####                      동적 메모리를 다 사용한 경우, stack over flow 등
* #### 예외 ( Exception ) : 프로그램에서 제어할 수 있는 오류
     ####                  읽으려는 파일이 없는 경우, 네트윅이나 소켓 연결 오류 등
     ####                  자바 프로그램에서는 예외에 대한 처리를 수행함

<br>

### :round_pushpin: 예외 클래스
#### 모든 예외 클래스의 최상위 클래스는 Exception 클래스

<br>

#### :round_pushpin: try - catch 문으로 예외 처리 하기

      try{
        예외가 발생할 수 있는 코드 부분    
	// 예외가 발생하면 바로 중단되고 catch의 예외 타입과 매치가되면 거기로 넘어감
      } catch(처리할 예외 타입 e){
         try 블록 안에서 예외가 발생했을 때 수행되는 부분
      }
```java
public class ArrayExceptionTest {

	public static void main(String[] args) {
		int[] arr = new int[5];
		
		try {
			for(int i=0; i<=5; i++) {
				System.out.println(arr[i]);
			}
		}catch(ArrayIndexOutOfBoundsException e) {
			System.out.println(e);
			System.out.println("예외처리");
		}
		System.out.println("프로그램 종료되지않고 계속 넘어옴. 서버가 죽은게 아님");
	}
}
```

<br>

#### :round_pushpin: try - catch - finally 문으로 예외 처리 하기

              try{
                예외가 발생할 수 있는 코드 부분    
              } catch(처리할 예외 타입 e){
                try 블록 안에서 예외가 발생했을 때 수행되는 부분
              } finally{
                예외 발생 여부와 상관없이 항상 수행되는 부분
                리소스를 정리하는 코드를 주로 씀
              }
```java
public class ExceptionTest {

    public static void main(String[] args) {
		
    FileInputStream fis = null;
    
    try {
    	fis = new FileInputStream("a.txt");	
    } catch (FileNotFoundException e) {
	System.out.println(e);
        return;  //---finally수행 후 , 바로 return
    }finally{
      	try{
          fis.close();//-------null인 상태에서 open안되고 close수행하면 nullPointException뜸
          System.out.println("finally");
        } catch (Exception e) { //--IOException에서 Exception으로 변경한 이유.
	  System.out.println(e);
	}
    }
  // 여기는 출력이 안됨. finally수행하고 바로 return이 됐기때문. return없으면 end가 출력된다.
  System.out.println("end");  
}
```

<br>

### :round_pushpin: try - with - resources 문
 * ##### 리소스를 자동으로 해제하도록 제공해주는 구문, finally가 필요없게됨
 * ##### 해당 리소스가 AutoCloseable을 구현한 경우 close()를 명시적으로 호출하지 않아도
   ##### try{}블록에서 오픈된 리소스는 정산적인 경우나 예외가 발생한 경우 모두 자동으로 close()가 호출됨
 * ##### 자바 7부터 제공됨
 * ##### FileInputStream의 경우 AutoCloseable을 구현하고있음
 
 <br>
 
:triangular_flag_on_post: #### AutoCloseable 인터페이스 사용하기
 ##### AutoCloseable 인터페이스를 구현한 클래스를 만들고 close()가 잘 호출되는지 확인해본다
      public class AutoCloseObj implements AutoCloseable{
        @Override
        publid void close( ) throws Exception{
          System.out.println("리소스가 close() 되었습니다.");
        }
      }
 ```java
 public class AutoCloseObj implements AutoCloseable{

	@Override
	public void close() throws Exception {
		System.out.println("close()가 호출되었습니다.");
	}
}
```
```java
public class AutoCloseTest {

  public static void main(String[] args) {
				 
	try(AutoCloseObj obj = new AutoCloseObj()){
		throw new Exception();  //예외 일부러발생시켜도 
			
	}catch(Exception e) {
		System.out.println(e);  //예외가 있어도 없어도 close호출. 출력, "close()가 호출되었습니다."
	}
   }
}
```
      
      <br>
      
### :round_pushpin: 향상된 try - with - resources 문
 #### 자바 9에서 제공되는 구문
 * ##### 자바 9이전
          AutoCloseObj obj = new AutoCloseObj();
          try (AutoCloseObj obj2 = obj){
            throw new Exception( );
          }catch(Exception e){
            System.out.println("예외 부분입니다");
          }
  * ##### 자바 9 이후
          AutoCloseObj obj = new AutoCloseObj();
          try (obj){--------------외부에서 선언한 변수를 그대로 쓸 수 있음 
            throw new Exception( );
          }catch(Exception e){
            System.out.println("예외 부분입니다");
          }
            

<br>

### :round_pushpin: 예외 처리 미루기
#### throws를 사용하여 예외처리 미루기
* ##### try{} 블록으로 예외를 처리하지않고, 메서드 선언부에 throws 를 추가
* ##### 예외가 발생한 메서드에서 예외 처리를 하지 않고 이 메서드를 호출한 곳에서 예외처리를 한다는 의미
* ##### main()에서 throws를 사용하면 가상머신에서 처리됨
```java
public class ThrowsException {

	public Class loadClass(String fileName, String className) throws FileNotFoundException, ClassNotFoundException {
		FileInputStream fis = new FileInputStream(fileName);
		Class c = Class.forName(className);
		return c;
	}
	
	public static void main(String[] args)  {

		ThrowsException test = new ThrowsException();
		
		try {
			test.loadClass("a.txt", "java.lang.string"); //'s'소문자로 잘못입력해 예외발생시킴
	
		
		} catch (FileNotFoundException e) {
			System.out.println(e);   //"java.io.FileNotFoundException: b.txt 지정된 파일을 찾을 수 없습니다"
		} catch (ClassNotFoundException e) {
			System.out.println(e);
		} 
		
	}

}
```

<br>

### :round_pushpin: 다중 예외처리하기
* #### 하나의 try{}블록에서 여러 예외가 발생하는 경우 catch{} 블록 한곳에서 처리하거나 
  #### 여러 catch{} 블록으로 나누어 처리할 수 있음
* #### 가장 최상위 클래스인 Exception 클래스는 가장 마지막 블록에 위치해야함.
  #### => 모든 것을 포함하는 예외클래스이지만, 상황에 맞는 log를 남기기위해 하위 예외를 사용하는 것임
  
   	public static void main(String[] args){
	  ThrowsException test = new ThrowsException();
	  try {
	   test.loadClass("a.txt","java.lang.String");
	  } catch (FileNotFoundException e){
	   e.printStackTrace( );
	  } catch (ClassNotFoundException e){
	   e.printStackTrace( );
	  } catch(Exception e){ ---------Exception 클래스로 그 외 예외상황처리
	   e.printStackTrace( );
	  }
	 } 
	 
	 
#### 한꺼번에 다중처리하기	 
```java
public static void main(String[] args){
	  ThrowsException test = new ThrowsException();
	  try {
	   test.loadClass("a.txt","java.lang.String");
	  } catch (FileNotFoundException | ClassNotFoundException e){
	   e.printStackTrace( );
	  }
```

<br>

### :round_pushpin: 사용자 정의 예외	 
* #### JDK에서 제공되는 예외 클래스 외에 사용자가 필요에 의해 클래스를 정의하여 사용
* #### 기존 JDK 클래스에서 상속받아 예외 클래스 만듦.
* #### throw 키워드로 예외를 발생시킴, throws는 던지는 것.

	   public class IDFormatException extends Exception{
	     public IDFormatException(String message){--------생성자의 매개변수로, 예외 상황 메세지를 받음
	     super(message);
	     }
	   }
```java
public class IDFormatException extends Exception{
	
	public IDFormatException(String message) {
		super(message);
	}
}
```
```java
public class IDFormatTest {
	
	private String userID;

	public String getUserID() {
		return userID;
	}

	public void setUserID(String userID) throws IDFormatException {
	
		if (userID == null) {
			throw new IDFormatException("아이디는 null 일수 없습니다");
		}
		else if( userID.length() < 8 || userID.length() > 20) {
			throw new IDFormatException("아이디는 8자 이상 20자 이하로 쓰세요");
		}
				
		this.userID = userID;
	}

	public static void main(String[] args) {
		
		IDFormatTest idTest = new IDFormatTest();
		
		String myId = null;
		
		try {
			idTest.setUserID(myId);
		} catch (IDFormatException e) {
			System.out.println(e);
		}
		
		myId = "123456";
		try {
			idTest.setUserID(myId);
		} catch (IDFormatException e) {
			System.out.println(e);
		}
	}

}
```

<br>

-------------------------------------------
## 예외 총정리

<br>

![Chapter 13 예외 처리 - 01 예외와 예외 처리_페이지_13](https://user-images.githubusercontent.com/74708028/110584864-3e57c280-81b3-11eb-999b-93e68e6f7be7.png)
![Chapter 13 예외 처리 - 01 예외와 예외 처리_페이지_14](https://user-images.githubusercontent.com/74708028/110584872-4283e000-81b3-11eb-8c76-e26327713ae9.png)
![Chapter 13 예외 처리 - 01 예외와 예외 처리_페이지_15](https://user-images.githubusercontent.com/74708028/110584875-444da380-81b3-11eb-8f62-4bae0cb80ab8.png)
![Chapter 13 예외 처리 - 01 예외와 예외 처리_페이지_16](https://user-images.githubusercontent.com/74708028/110584882-46affd80-81b3-11eb-9480-0ee48284bd98.png)
![Chapter 13 예외 처리 - 01 예외와 예외 처리_페이지_17](https://user-images.githubusercontent.com/74708028/110584892-49aaee00-81b3-11eb-9121-8a2e165b35ed.png)
![Chapter 13 예외 처리 - 01 예외와 예외 처리_페이지_18](https://user-images.githubusercontent.com/74708028/110584897-4c0d4800-81b3-11eb-8550-8cd51b7dd39e.png)
![Chapter 13 예외 처리 - 01 예외와 예외 처리_페이지_19](https://user-images.githubusercontent.com/74708028/110584901-4e6fa200-81b3-11eb-96f8-6cd64ac89dcc.png)
![Chapter 13 예외 처리 - 01 예외와 예외 처리_페이지_20](https://user-images.githubusercontent.com/74708028/110584909-50d1fc00-81b3-11eb-9669-a0c92cb8e73c.png)


