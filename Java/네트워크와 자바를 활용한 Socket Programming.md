### :pushpin: 네트워크와 자바를 활용한 Socket Programming

#### :round_pushpin: 네트워크 Network, 서버와 클라이언트
* ##### 네트워크 : 여러 대의 컴퓨터를 통신 회선으로 연결한 것을 말한다. 홈 네트워크, 지역 네트워트, 인터넷 등이 해당된다.
* ##### 서버와 클라이언트 : 네트워크로 연결된 컴퓨터간의 관계를 역할로 구분한 개념으로, 서버와 클라이언트로 구분한다.  
    * ##### 서버는 서비스를 제공하는 프로그램을 말한다. 클라이언트의 연결을 수락하고 요청 내용을 처리 후 응답을 보내는 역할을 담당한다.  
    * ##### 클라이언트는 서비스를 받는 프로그램으로, 네트워크 데이터를 필요로 하는 모든 어플리케이션이 해당한다. 

<br>

#### :round_pushpin: IP주소와 포트 (port)
* ##### IP주소 : 네트워크 상에서 컴퓨터를 식별하는 번호로 네트워크 어댑터(랜카드)마다 고유의 번호를 할당하여 통신에 사용한다.
* ##### 포트 (port) : 같은 컴퓨터 내에서 프로그램을 식별하는 번호이다. 클라이언트 서버 연결 요청시 IP 주소와 port 번호를 알아야 한다.

<br>

#### :round_pushpin: URL 클래스 
##### 특정 URL 주소를 다루기 위해 자바에서 제공되는 클래스
```java
public class UrlTest {

	public static void main(String[] args) {
		InputStream is = null;
		InputStreamReader isr = null;
		BufferedReader br = null;
		
		try {
			URL url = new URL("https://github.com/6161990/TIL"); //https는 s: 시큐리티, 보안이 들어감
			is = url.openStream();
			isr = new InputStreamReader(is, "UTF-8");
			br = new BufferedReader(isr);
			String str = "";	
			while((str = br.readLine())!=null) {
				System.out.println(str);
			}
		} catch (MalformedURLException e) {
			e.printStackTrace();
		} catch (UnsupportedEncodingException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		} finally {
			try {
				is.close();
				isr.close();
				br.close();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
	}

}
```

<br>

#### :round_pushpin: URLConnetion 클래스 
##### 추상클래스이므로 생성자를 사용해서 객체를 생성할 수는 없으며, URL 객체의 openConnection()메소드를 이용해서 생성할 수 있다. 
##### 또한, URLConnetion 객체가 생성되면 connect 메소드를 호출하여 URL객체에 설정되어 있는 URL에 연결할 수 있다. 
```java
public class UrlConnectionTest {

	public static void main(String[] args) {
		InputStream is = null;
		InputStreamReader isr = null;
		BufferedReader br = null;
		
		try {
			URL url = new URL("https://github.com/6161990/TIL");
			URLConnection conn = url.openConnection();
			is = conn.getInputStream();
			isr = new InputStreamReader(is, "UTF-8");
			br = new BufferedReader(isr);
			String str = "";
			String contentType = conn.getContentType();
			System.out.println("contentType= "+contentType);
			while((str=br.readLine())!=null) {
				System.out.println(str);
			}
		} catch (MalformedURLException e) {
			e.printStackTrace();
		} catch (UnsupportedEncodingException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		} finally {
			try {
				is.close();
				isr.close();
				br.close();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
	}

}

```
<br>

#### :round_pushpin: InetAddress 클래스 
##### 특정 IP주소를 다루기 위한 클래스로, InetAddress 클래스 객체는 생성자로 생성할 수 없으며 자바에서 제공되는 여러 개의 static 메소드에서의 의해서 생성된다.

```java

import java.net.InetAddress;
import java.net.UnknownHostException;

public class InetAddressTest {

	public static void main(String[] args) {
		InetAddress ia = null;
		try {
			ia = InetAddress.getLocalHost(); //DESKTOP-4730154/192.168.0.101
			System.out.println(ia);
			
			ia = InetAddress.getByName("www.google.or.kr");  //DNS
			System.out.println(ia); //www.google.or.kr
			
			InetAddress[] aia = InetAddress.getAllByName("www.google.or.kr"); //IP //도메인을 IP로 바꿔줌
			for(int i = 1; i<aia.length; i++) { 
				System.out.println(aia[i]); //221.143.20.101
			}
		} catch (UnknownHostException e) {
			e.printStackTrace();
		}
	}

}

```

<br>

#### :round_pushpin: Socket Programming
* ##### 소켓을 이용한 통신 프로그래밍을 뜻한다. 소켓이란, 프로세스간의 통신에 사용되는 양쪽 끝 단을 말한다.
    * ##### TCP : 데이터의 전송 속도가 느리지만 정확하고 안정적으로 전달할 수 있는 연결 지향적 프로토콜이다.
    * ##### UDP : 데이터의 전송 속도가 빠르지만 신뢰성 없는 데이터를 전송하는 비연결 지향적 프로토콜이다.

<br>

#### :round_pushpin: TCP Socket Programming

<img width="397" alt="agd" src="https://user-images.githubusercontent.com/74708028/113475105-98942c80-94ae-11eb-924b-09e62e944b50.png">


* ##### 클라이언트와 서버간의 1:1 소켓 통신이다. 서버가 먼저 실행이 되어 클라이언트의 연결 요청을 기다려야 한다.  
* ##### 서버가 먼저 실행이 되어 클라이언트의 연결 요청을 기다려야 한다. 
* ##### java.net패키지에서 제공하는 ServerSocket과 Socket 클래스가 해당한다. 서버용 프로그램과 클라이언트용 프로그램을 따로 구현해야한다.
#
* ##### TCP 소켓 프로그래밍 순서(서버용)
   ##### 1. 서버의 포트번호를 정한다.
   ##### 2. 서버용 소켓 객체를 생성한다.
   ##### 3. 클라이언트 쪽에서 접속 요청이 오기를 기다린다.
   ##### 4. 접속 요청이 오면 요청을 수락하고 해당 클라이언트에 대한 소켓 객체를 생성한다.
   ##### 5. 연결된 클라이언트와 입출력 스트림을 생성한다.
   ##### 6. 보조스트림을 통해 성능을 개선시킨다.
   ##### 7. 스트림을 통해 읽고 쓰기를 한다.
   ##### 8. 통신을 종료한다.
   
```java

public class TCPServer extends Thread { //통신을 하려면 멀티 처리가 되어야하므로 
	private InputStream is;
	private OutputStream os;
	private ServerSocket serverSocket;
	private ObjectInputStream ois;
	private ObjectOutputStream oos;
	private Socket socket;
	
	@Override
	public void run() {
		try {
			serverSocket = new ServerSocket(5000); //1~1000까지는 예약포트라서 피하고 10000이하의 아무 포트나 골라쓰면 된다.
			while(true) {
				System.out.println("요청 대기 : "); //서버는 항상 대기 접속이 될 때 그것을 받아주고 서비스 제공(정보 제공), 웹 브라우저로 날라온다.
				socket = serverSocket.accept(); // accept : 접속하겠다. 
				System.out.println("접속한 클라이언트 : "+ socket.getInetAddress());
				is = socket.getInputStream();
				os = socket.getOutputStream();
				ois = new ObjectInputStream(is);
				oos = new ObjectOutputStream(os);
				String msg = (String) ois.readObject();
				System.out.println("클라이언트에서 보낸 메세지 : "+msg);
				String retMsg = "서버로부터 되돌아온 메세지 : " + msg;
				oos.writeObject(retMsg);
				socket.close();
			}
		} catch (ClassNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		} 
	}
	
	public static void main(String[] args) {
		new TCPServer().start();
	}

}

```


#
* ##### TCP 소켓 프로그래밍 순서(클라이언트용)
  ##### 1. 서버의 IP 주소와 서버가 정한 port 번호를 매개변수로 하여 클라이언트용 소켓 객체를 생성한다.
  ##### 2. 서버와의 입출력 스트림을 오픈한다.
  ##### 3. 보조스트림을 붙여 성능을 개선한다.
  ##### 4. 스트림을 통해 읽고 쓰기를 한다.
  ##### 5. 통신을 종료한다.
```java

public class TCPClient {
	private InputStream is;
	private OutputStream os;
	private Socket socket;
	private ObjectInputStream ois;
	private ObjectOutputStream oos;
	public BufferedReader input;
	private String rMsg;
	
	public void start() {
		try {
			socket = new Socket("125.178.1.44", 5000); //5000포트로 들우가
			sendMessage(socket);
			receiveMessage(socket);
		} catch (UnknownHostException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		} finally {
			try {
				socket.close();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
	}
	
	private void receiveMessage(Socket socket) {
		try {
			is = socket.getInputStream();
			ois = new ObjectInputStream(is);
			rMsg =(String) ois.readObject();
			System.out.println(rMsg);
		} catch (ClassNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
	
	private void sendMessage(Socket socket) {
		try {
			os = socket.getOutputStream();
			oos = new ObjectOutputStream(os);
			input = new BufferedReader(new InputStreamReader(System.in));
			System.out.println("보낼 메세지");
			String sMsg = input.readLine(); //버퍼드 리더가 지원하는 메소드 리드 라인
			oos.writeObject(sMsg);
		} catch (IOException e) {
			e.printStackTrace();
		}
	}
	public static void main(String[] args) {
		TCPClient tcp = new TCPClient();
		tcp.start();
	}
}

```


<br>

#### :round_pushpin: UDP Socket Programming

<img width="418" alt="20210403181227ffff" src="https://user-images.githubusercontent.com/74708028/113475121-a3e75800-94ae-11eb-8ea9-a2b1a10d59dd.png">


* ##### UDP 는 연결지향적이지 않기 때문에 연결요청을 받아줄 서버소켓이 필요없다. 
* ##### java.net 패키지에서 제공하는 두 개의 DatagramSocket 간에 DatagramPacket으로 변환된 데이터를 주고 받는다.
#
* ##### UDP 소켓 프로그래밍 순서(서버용)
  ##### 1. 포트 번호를 정한다.
  ##### 2. DatagramSocket 객체를 생성한다.
  ##### 3. 연결한 클라이언트 IP주소를 가진 InetAddress 객체를 생성한다.
  ##### 4. 전송할 메시지를 byte[]로 바꾼다.
  ##### 5. 전송할 메시지를 DatagramPacket 객체에 담는다.
  ##### 6. 소켓레퍼런스를 사용하여 메시지를 보낸다.
  ##### 7. 소켓을 닫는다.
#
* ##### UDP 소켓 프로그래밍 순서(클라이언트용 )
  ##### 1. 서버가 보낸 메시지를 받을 byte[]을 준비한다.
  ##### 2. DatagramSocket 객체를 생성한다.
  ##### 3. 메시지를 받을 DatagramPacket 객체를 준비한다.
  ##### 4. 소켓레퍼런스를 사용하여 메시지를 보낸다.
  ##### 5. byte[] 로 받은 메시지를 String으로 바꾸어 출력한다.
  ##### 6. 소켓을 닫는다.


<br>

#### :round_pushpin: TCP Socket Programming와 UDP Socket Programming
비교항목 | TCP | UDP 
 -- | -- | --
 신뢰성 | 연결지향적인 통신이므로 신뢰성이 우수 | 신뢰성이 보장되지 못한다. 상대방의 수신결과와 상관없이 송신하다. 
 재전송 | 요청가능 | 불가능
 데이터손실 | 데이터 손실없음. (수신확인 메시지를 주고받으므로) | 데이터 손실있을 수 있음
 비유 | 상대방과 연결하고 통화가 이루어지는 전화통신 | 상대방과 비연결로 이루어지는 이메일 송신
 속도 | 비교적 느림 | 빠름 

    
