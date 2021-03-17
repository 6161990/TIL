## :pushpin: 바이트 단위 입출력 스트림 Byte IO Stream
* #### InputStream : 바이트 단위 입력 스트림 최상위 클래스
* #### OutputStream : 바이트 단위 출력 스트림 최상위 클래스 
  #### => 위 기반 클래스는 추상 메서드를 포함한 추상 클래스로, 아래 하위 클래스가 구현하여 사용 
  
 <br>
 
### :round_pushpin: 입력 보조 스트림
* #### FileInputStream : 파일에서 바이트 단위로 자료를 읽습니니다
* #### ByteArrayInputStream : Byte 배열 메모리에서 바이트 단위로 자료를 읽습니다
* #### FilterInputStream : 기반 스트림에서 자료를 읽을 때 추가 기능을 제공하는 보조 스트림의 상위 클래스입니다

<br>

### :round_pushpin: 출력 보조 스트림
* #### FileOutputStream : 바이트 단위로 파일에 자료를 씁니다
* #### ByteArrayOutputStream : Byte 배열에 바이트 단위로 자료를 씁니다
* #### FilterOutputStream : 기반 스트림에서 자료를 쓸 때 추가 기능을 제공하는 보조 스트림의 상위 클래스입니다

<br>

### :round_pushpin: FileInputStream과 FileOutputStream 사용하기
##### 파일에 한 바이트씩 자료를 읽고 쓰는데 사용 
* #### 문자는 읽지못하기 때문에 한글처럼 멀티바이트로 fileReader, fileWriter를 써야한다.
* #### 입력 스트림은 파일이 없는 경우 예외 발생
* #### 출력 스트림은 파일이 없는 경우 '파일 생성하여' 출력

<br>

### :round_pushpin: FileInputStream
```java
public class FileInputTest1 {

    public static void main(String[] args) {

	FileInputStream fis = null;  // finally에서도 읽을 수 있게 전역변수
	    try {
	      fis = new FileInputStream("input.txt");
	    } catch (FileNotFoundException e) {   //input.txt 파일이 없을 때 , FileNotFoundException -> Unknown Source
	      e.printStackTrace();
	    } finally {
	      try {
		fis.close();
	      } catch (IOException e) {  //close의 오류를 잡으려면 Exception 로.
		e.printStackTrace();
	      }
	 }
     }
}
```
```java
public class FileInputTest1 {

        public static void main(String[] args) {

	    FileInputStream fis = null;
	    
		try {
		fis = new FileInputStream("input.txt"); //파일안에는 'ABC'
			 			 
		int i = fis.read(); //한 바이트씩 처리 
		System.out.print((char)i);   //A
		i = fis.read();
       		System.out.print((char)i);   //B
     		i = fis.read();
       		System.out.print((char)i);   //C
      		} catch (IOException e) {   //FileNotFoundException를 내포하는 예외로 처리, read에서도 예외처리를 해야하니까 더 큰 걸로 다중예외처리
		   e.printStackTrace();
		} finally {
		    try {
			fis.close();
			} catch (Exception e) {
			e.printStackTrace();
			}
		   }
		System.out.println("end");
	}
}
```
```java
public class FileInputTest1 {

	public static void main(String[] args) {

		FileInputStream fis = null;
		
		try {
		   fis = new FileInputStream("input.txt");
			 			 
		   int i;
		   while ( (i = fis.read()) != -1) {  //But, 파일을 끝까지 쭉 읽고싶다면 while //-1 : end Of File
			 System.out.print((char)i);     //But,한글은 깨짐 
			 }
			 
		} catch (IOException e) {
			e.printStackTrace();
		} finally {
		    try {
			 fis.close();
			} catch (Exception e) {
			 e.printStackTrace();
			}
		}
		System.out.println("end");
	}
}
```

<br>


### :triangular_flag_on_post: try-with-resources(Auto Close)
```java
public class FileInputTest2 {

	public static void main(String[] args) {

		try (FileInputStream fis = new FileInputStream("input.txt") ){  //Try안에 선언 //Auto Close이므로 finally필요 없음
			 int i;
			 while ( (i = fis.read()) != -1) {
			 		 System.out.print((char)i);
			 }
			 
		} catch (IOException e) {
			e.printStackTrace();
		}
		System.out.println("end");
	}
}
```

<br>

### :triangular_flag_on_post: read 메소드 byte array(한 바이트씩 읽는 것보다 빠름)
```java
public class FileInputTest3 {

	public static void main(String[] args) {

		try (FileInputStream fis = new FileInputStream("input2.txt") ){
			 int i;
			 byte[] bs = new byte[10];  //array만큼 10개씩 읽어서 
			 while ( (i = fis.read(bs)) != -1) {  //밖에서
			 	/*for(byte b : bs) {
			 		System.out.print((char)b);  // 안에 도는 구문을 이렇게 하면 buffer에 남은 garbage가 출력됨 
			 	}*/
				 
				for(int k=0; k<i; k++) {   //안에서 돌면서 읽은 갯수를 뱉어냄. 
					System.out.print((char)bs[k]);
				}
			 	System.out.println();
			 }
			 
		} catch (IOException e) {
			e.printStackTrace();
		}
		//System.out.println("end");
	}
}
```

------------------------------------------------

<br>

### :round_pushpin: FileOutputStream
```java
public class FileOutputTest1 {

	public static void main(String[] args) {

    //출력스트림(output)은 파일이 없는 경우 생성하여 출력
		try(FileOutputStream fos = new FileOutputStream("output.txt", true)){  //true라고 하면 append되어서 출력
			
			fos.write(65);
			fos.write(66);
			fos.write(67);
			
		}catch( IOException e) {
			System.out.println(e);
		}
	}
}
```

-----------------------------------------------------------

<br>

### :round_pushpin: FileInputStream & FileOutputStream 같이 
```java
public class FileOutputTest2 {

	public static void main(String[] args) {

		byte[] bs = new byte[26];
		byte data = 65;
		for(int i =0; i<bs.length; i++) {     
			bs[i] = data;
			data++;
		}
		
		try(FileOutputStream fos = new FileOutputStream("alpha.txt", true);
			FileInputStream fis = new FileInputStream("alpha.txt")){
			
			fos.write(bs);   // 출력
			int ch;
			while ( (ch = fis.read()) != -1 ) {  //입력
				System.out.print((char)ch);
			}
			
		}catch( IOException e) {
			System.out.println(e);
		}
	}

}
```

-----------------------------------------------------------

<br>

### :round_pushpin: flush()와 close()메서드
* ##### 출력용 버퍼를 비울 때 flush()메서드 호출
* ##### 파일 스트림을 닫기위한 close()메서드가 호출되면 내부에서 flush()를 호출하며 출력 버퍼를 비움
