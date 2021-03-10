### 예외 Exception
#### 오류란 무엇인가?
* ###### 컴파일 오류 :  프로그램 코드 작성 중 발생하는 문법적 오류
* ###### 실행 오류 : 실행 중인 프로그램이 의도하지 않은 동작을 하거나 (bug), 프로그램이 중지되는 오류 (runtime error)
  ###### 자바는 예외 처리를 통하여 프로그램의 비정상 종료를 막고 log를 남길 수 있음
  ###### log를 잘 남겨야 예외 처리가 수월함
#### 오류와 예외 클래스
* ###### 시스템 오류 (error) : 가상 머신에서 발생, 프로그래머가 처리할 수 없음
  ######                      동적 메모리를 다 사용한 경우, stack over flow 등
* ###### 예외 ( Exception ) : 프로그램에서 제어할 수 있는 오류
                              읽으려는 파일이 없는 경우, 네트윅이나 소켓 연결 오류 등
                              자바 프로그램에서는 예외에 대한 처리를 수행함
#### 예외 클래스
###### 모든 예외 클래스의 최상위 클래스는 Exception 클래스

#
**try - catch 문으로 예외 처리 하기**

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
**try - catch - finally 문으로 예외 처리 하기**

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
        return;  //-----------finally수행 후 , 바로 return
    }finally{
      	try{
          fis.close();//-------null인 상태에서 open안되고 close수행하면 nullPointException뜸
          System.out.println("finally");
        } catch (Exception e) { //-----IOException에서 Exception으로 변경한 이유.
	  System.out.println(e);
	}
    }
  // 여기는 출력이 안됨. finally수행하고 바로 return이 됐기때문. return없으면 end가 출력된다.
  System.out.println("end");  
}
```
 #            
 **try - with - resources 문**
 ###### 리소스를 자동으로 해제하도록 제공해주는 구문,finally가 필요없게됨
 ###### 해당 리소스가 AutoCloseable을 구현한 경우 close()를 명시적으로 호출하지 않아도
 ###### try{}블록에서 오픈된 리소스는 정산적인 경우나 예외가 발생한 경우 모두 자동으로 close()가 호출됨
 ###### 자바 7부터 제공됨
 ###### FileInputStream의 경우 AutoCloseable을 구현하고있음
 
*  ##### AutoCloseable 인터페이스 사용하기
 ###### AutoCloseable 인터페이스를 구현한 클래스를 만들고 close()가 잘 호출되는지 확인해본다
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
		throw new Exception();  //---------예외 일부러발생시켜도 
			
	}catch(Exception e) {
		System.out.println(e);  //예외가 있어도 없어도 close호출. 출력, "close()가 호출되었습니다."
	}
   }
}
```
      
 **향상된 try - with - resources 문**
 ##### 자바 9에서 제공되는 구문
 * ###### 자바 9이전
          AutoCloseObj obj = new AutoCloseObj();
          try (AutoCloseObj obj2 = obj){
            throw new Exception( );
          }catch(Exception e){
            System.out.println("예외 부분입니다");
          }
  * ###### 자바 9 이후
          AutoCloseObj obj = new AutoCloseObj();
          try (obj){---------------------------------------------외부에서 선언한 변수를 그대로 쓸 수 있음 
            throw new Exception( );
          }catch(Exception e){
            System.out.println("예외 부분입니다");
          }
            
