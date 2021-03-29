## :pushpin: 표준 입출력 스트림 Standard InputOutput Stream
###### 참고 : [I/O 입출력 스트림](https://github.com/6161990/TIL/blob/main/Java/IO%20Stream.md)
#### System 클래스의 표준 입출력 멤버 : static이기 때문에 생성자없이 쓸 수 있었음

    public class System{
       public static PrintStream out; //표준 출력 스트림
       public static InputStream in;  //표준 입력 스트림
       public static PrintStream err; // 표준 에러 스트림
     }
 
<br>

### :round_pushpin: System.in 사용하여 입력 받기
* #### 한 바이트씩 읽어들임
* #### read() 의 데이터 타입은 int : 파일의 끝에 도달해 더이상 읽을 것이 없을 때 -1을 반환해야하기때문
* #### 한글과 같은 여러 바이트로 된 문자를 읽기 위해서는 InputStreamReader와 같은 보조 스트림을 사용해야함
* #### System.in은 InputStream임.

<br>

##### :triangular_flag_on_post: 문자가 아닐 때
```java
public class SystemInTest {

	public static void main(String[] args) {

		System.out.println("입력");
		
		try {
			int i;
	    while(( i= System.in.read()) !='\n'){ //\n ; Enter
			System.out.println((char)i);
		} catch (IOException e) {
			e.printStackTrace();
		}	
	}
}
```
##### => 엔터 누르기 전까지만 입력을 받고, 엔터누르면 더이상 입력할 수 없음

<br>

##### :triangular_flag_on_post: 문자일 때
```java
public class SystemInTest2 {

	public static void main(String[] args) {

		System.out.println("입력 후 '끝' 이라고 쓰세요:");
		
		try {
			int i;
			while ( (i = isr.read()) != '끝') {  
				System.out.print((char)i);
			}
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
}
```
##### :interrobang: '끝'이라고 입력할 때까지만 입력한다고 했는데, 콘솔창에 계속 입력가능. why?
#####    '끝'은 한글. 한글은 2byte씩 읽는데, System.in.read()는 1byte씩 밖에 못읽음.
#####     muti byte로 읽을 수 있게 (문자로 바로 읽을 수 있게 바꿔줘야함)
#####     보조스트림필요 InputStreamReader

<br>

#### :round_pushpin: 문자일 때 보조스트림이용해 출력하기
```java
public class SystemInTest2 {

	public static void main(String[] args) {

		System.out.println("입력 후 '끝' 이라고 쓰세요:");
		
		try {
			int i;
			InputStreamReader isr = new InputStreamReader(System.in); //보조스트림은 다른 스트림을 안에 받는다.
			while ( (i = isr.read()) != '끝') {
				System.out.print((char)i);
			}
		} catch (IOException e) {
			e.printStackTrace();
    }	
	}
}
```

<br>

### :round_pushpin: Scanner 클래스
* ###### 참고:  [내장 클래스](https://github.com/6161990/TIL/blob/main/Java/%EB%82%B4%EC%9E%A5%ED%81%B4%EB%9E%98%EC%8A%A4.md)
#
* #### java.util 패키지에 있는 입력 클래스
* #### 문자뿐 아니라 정수, 실수등 다양한 자료형을 읽을 수 있음
* #### 생성자가 다양하여 여러 소스로부터 자료를 읽을 수 있음
 * ##### Scanner(File source) : 파일을 매개변수로 받아 Scanner를 생성합니다
 * ##### Scanner(InputStream source) : 바이트 스트림을 매개변수로 받아 Scanner를 생성합니다
 * ##### Scanner(String source) : String을 매개변수로 받아 Scanner를 생성합니다

<br>

### :round_pushpin: Console 클래스
* #### System.in 을 사용하지 않고 콘솔에서 표준 입출력이 가능
* #### 이클립스와는 연동되지 않음
* #### Console 클래스의 메서드
 * ##### String readLine() : 문자열을 읽습니다
 * ##### char[] readPassword() : 사용자에게 문자열을 보여주지않고 읽습니다.
 * ##### Reader reader() : Reader 클래스를 반환합니다.
 * ##### PrintWriter writer() : PrintWriter 클래스를 반환합니다.

```java
public class ConsoleTest {

   public static void main(String[] args) {

	Console console = System.console();
		
	System.out.println("ŔĚ¸§:");
	String name = console.readLine();
	System.out.println("şńšĐšřČŁ:");
	char[] password = console.readPassword();
		
	System.out.println(name);
	System.out.println(password);
   }

}
```
