### :pushpin: 보조 스트림 Decorator Stream

###### 참고: [데코레이터 패턴](https://github.com/6161990/TIL/blob/main/DesignPattern/Decorator%20Pattern.md)

####  실제 읽고 쓰는 스트림이 아닌 보조적인 기능을 추가하는 스트림 
* ##### FilterInputStream 과 FilterOutputStream이 보조스트림의 상위 클래스
* ##### 생성자의 매개 변수로 또 다른 스트림을 가짐
  * ###### protected FilterInputStream(InputStream in) : 생성자의 매개변수로 InputStream을 받습니다.
  * ###### public FilterOutputStream(OutputStream out) : 생성자의 매개변수로 OutputStream을 받습니다.
* ##### :triangular_flag_on_post: 데코레이터 패턴 (Decorator Pattern) 
<img src="https://user-images.githubusercontent.com/74708028/110726518-dd84c480-825c-11eb-8973-5e9f9186dad2.jpg" width="700" height="305"/>  

<br>

#### :round_pushpin: 여러가지 보조스트림 사용하기
* ##### InputStreamReader / OutputStreamWriter : 소스 스트림이 바이트 기반 스트림이지만 데이터가 문자일경우 사용한다. Reader와 Writer는 문자 단위로 입출력을 하기 때문에 데이터가 문자인 경우에 바이트 기반 스트림보다 편리하게 사용할 수 있다. 
* ##### Buffered 스트림 : 느린 속도로 인해 입출력 성능에 영향을 미치는 입출력 소스를 이용하는 경우(하드디스크, 느린 네트워크)사용한다. 입출력 소스와 직접 작업하지 않고 버퍼에 데이터를 모아 한꺼번에 작업을 하여 실행 성능이 향상된다. ( 내부에 8192 바이트 배열을 가지고 있어, 입출력 속도를 줄인다.)
* ##### DataInputStream/ DataOutputStream : 자료가 저장된 상태 그대로 자료형을 유지하며 읽거나 쓰는 기능을 제공하는 스트림, 입력된 자료형의 순서와 출력될 자료형의 순서가 일치해야한다.
* ##### ObjectInputStream/ ObjectOutputStream  : 객체를 파일 또는 네트워크로 입출력할 수 있는 기능을 제공한다. 단, 객체는 문자가 아니므로 바이트 기반으로 데이터를 변경해주는 작업인 직렬화를 반드시 해야한다. 
    * ###### 참고 : [직렬화](https://github.com/6161990/TIL/blob/main/Java/Serialization.md)
#

<br>

![Chapter 14 자바 입출력 - 05 보조 스트림_페이지_5](https://user-images.githubusercontent.com/74708028/110728099-c693a180-825f-11eb-90fb-462e242bbe79.png)


#### :round_pushpin: Buffered 사용하기 
```java
public class BufferedReaderTest {

	public static void main(String[] args) {
		
		FileInputStream fi = null; //1바이트에서 
		InputStreamReader isr = null; //2 바이트로 : 한글도 읽어올 수 있음
		BufferedReader  bfr = null; //빠르게 성능 업 
		/*BufferedReader input = new BufferedReader(new InputStreamReader(System.in));
		System.out.println("입력하숑");
		input.readLine();*/  //Scanner 말고 성능 좋게 이용하는 키보드 입력기능 
			
	 	try {
			fi = new FileInputStream("c:\\kh\\bufferedReader.txt");
			isr = new InputStreamReader(fi);
			bfr = new BufferedReader(isr);
			String str = null;
			while((str = bfr.readLine())!=null) { //라인 별로 끝까지 읽어오는 기능 
				System.out.println(str);
		    }
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		} finally {
			try {
				fi.close();
				isr.close();
				bfr.close();
			} catch (Exception e) {
				e.printStackTrace();
			}
		}
	}

}

```

![Chapter 14 자바 입출력 - 05 보조 스트림_페이지_6](https://user-images.githubusercontent.com/74708028/113797861-09786480-978d-11eb-9856-6b1f285a211e.png)


#### :round_pushpin: DataInputStream & DataOutputStream 사용하기 
```java

import java.io.DataInputStream;
import java.io.DataOutputStream;
import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;

public class DataStreamTest {

	public static void main(String[] args) {
		    FileOutputStream fo = null;
		    FileInputStream fi = null;
		    DataOutputStream dos = null;
		    DataInputStream dis = null;

		    try {
			      fo = new FileOutputStream("c:\\kh\\dataFile.txt"); //아웃풋은 생성기능 있음 파일 만듦.
			      fi = new FileInputStream("c:\\kh\\dataFile.txt");
			      dos = new DataOutputStream(fo);
			      dis = new DataInputStream(fi);

			      dos.writeShort(-1);
			      dos.writeByte(2);
			      dos.writeDouble(3.14);
			      dos.writeLong(30);
		       	      dos.writeUTF("dataStreamTest");
			      System.out.println(dis.readUnsignedShort()); //2바이트의 입력데이터를 읽기, 0~65535범위의 int값을 return 합니다. 
			      dis.skip(1); //현재 읽고 있는 위치에서 지정된 숫자만큼 건너뛴다.
			      System.out.println(dis.readDouble());
			      System.out.println(dis.readLong());
			      System.out.println(dis.readUTF());
			      
		    } catch (FileNotFoundException e) {
		      	      e.printStackTrace();
		    } catch (IOException e) {
		              e.printStackTrace();
		    } finally {
		       try {
			      fi.close();
			      fo.close();
			      dos.close();
		     } catch (IOException e) {
			  e.printStackTrace();
		     }
		    }

		   }

}

```

