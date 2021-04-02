### :pushpin: 쓰레드 Thread

<img src="https://user-images.githubusercontent.com/74708028/110875195-85ab9380-8318-11eb-9b00-1c3f786c6478.jpg" width="500" height="300"/>


* #### Process : 실행중인 프로그램, OS로부터 메모리를 할당 받음
  #### => 하나의 프로그램은 process가 돼서 메모리에 올라가게됨. process가 실행되는 단계가 thread 
* #### Thread : 프로세스 내에서 실제 작업을 수행하는 작업단위 , 모든 프로세스는 하나 이상의 Thread와 할당받은 자원(메모리 등)을 가지고 독립적인 작업 단위를 가진다.
  #### => cpu를 점유하는 scheduler가 thread에 cpu할당을 통해 thread가 수행되도록함.
* #### 프로세스 종료 : 싱글 스레드의 경우 메인 스레드가 종료하면 프로세스도 종료되지만, 멀티 스레드의 경우 실행 중인 스레드가 하나라도 있다면 프로세스가 종료되지 않는다.

<br>

### :round_pushpin: main thread와 daemon thread
* ##### main thread : 모든 자바 프로그램은 메인 스레드가 main() 메소드를 실행하며 시작한다. main()메소드의 첫 코드부터 아래로 순차적으로 실행되고, return을 만나면 실행을 종료시킨다.
* ##### daemon thread : 주 스레드의 작업을 돕는 보조적인 역할을 수행하는 스레드이다. 주 스레드가 종료되면 데몬 스레드는 강제적으로 자동 종료된다. 
    * ##### 데몬스레드 만들기
      ##### 데몬 스레드가 될 스레드의 레퍼런스 변수에 setDaemon(true)를 호출하여 생성한다. 
      ##### 단, start() 메소드 호출 전에 setDaemon(true)메소드를 호출해야한다. (lllegalThreadStareException이 발생한다.)


<br>

### :round_pushpin: 자바 Thread클래스로 부터 상속받아 구현
```java
class MyThread extends Thread {
  
	public void run() {
		int i;
		
		for( i=0; i<=200; i++) {
			System.out.print(i + "\t");
			
			try {
				Thread.sleep(10);  // thread class의 static 메서드 : 1000분의 일초 재우는 것, 자다깨다 자다깨다
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
	}
}

public class ThreadTest {
    
  pulbic static void main(String[] args){
    System.out.println("start");  
		MyTread th1 = new MyThread();  // 만들어놓은 thread 두 개가 각자 자다깨는 사이사이 번갈아가며 200까지 출력
		MyThread th2 = new MyThread();
		
		th1.start();
		th2.start();
		
    System.out.println("end"); // end는 앞부분쯤에 출력됨. why?
    
    //여기에는 총 세 개의 thread가 있는데 1. main 2. th1 3.th2 
    //-> 메인은 시작과 동시에 거의 thread가 끝난다. th2, th3는 수행해야 할 쓰레드가 남아있어서 그 뒤로 계속 돔
    }

}
```
##### => 자바는 다중 상속이 허용되지 않으므로 이미 다른 클래스를 상속한 경우, 
#####     thread를 만들려면 Runnable interface를 implements 하도록한다.


<br>

### :round_pushpin: Runnable 인터페이스로 구현
```java
class MyThread implements Runnable{  // 상속은 하나밖에 못하기 때문에 이미 어떤 class를 상속받았다면 Runnable로 구현

	
	public void run() {
		int i;
		
		for( i=0; i<=200; i++) {
			System.out.print(i + "\t");
			
			try {
				Thread.sleep(10);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
	}
}


public class ThreadTest {

	public static void main(String[] args) {

		System.out.println("start");
		
		
		MyThread runner1 = new MyThread(); 
		Thread th1 = new Thread(runner1); //thread class를 만들고 그 컨스트럭트에서 runnable한 객체를 받는 것 
		th1.start();
		
		
		MyThread runner2 = new MyThread();
		Thread th2 = new Thread(runner2);
		th2.start();
	
		System.out.println("end");
		
	}

}
```

<br>

-------------------------

<br>

### :round_pushpin: Multi-thread 프로그래밍
#### 동시에 여러 개의 Thread가 수행되는 프로그래밍
* ##### 자원을 보다 효율적으로 사용할 수 있고 작업이 분리되어 코드가 간결해진다.
* ##### Thread는 각각의 작업공간(context)를 가짐 -> thread가 swith되면 작업공간도 swith 된다.
* ##### 공유 자원이 있는 경우 race condition이 발생
* ##### critical section에 대한 동기화(synchronization)의 구현이 필요, 아니면 충돌한다.

<img src="https://user-images.githubusercontent.com/74708028/110875364-d3c09700-8318-11eb-95f3-571fc78c57fe.jpg" width="350" height="200"/>


<br>

#### :triangular_flag_on_post:  멀티 프로세스 vs. 멀티 스레드
##### 독립적으로 프로그램을 실행하는 것을 멀티 프로세스라고 하고, 한 개의 프로그램을 실행하고 내부적으로 여러가지 작업을 처리하는 것을 멀티스레드라고한다. 

#### :triangular_flag_on_post: critical section(임계 영역)? 
##### 두 개 이상의 thread가 동시에 접근하게 되는 리소스(자바로 예를 들면 static 키워드를 가진 객체들)
##### shared resource는 여러가지 thread가 있을 떄, 공유하는 자원. 같이 쓰다보니까 오류가 날 수도 있다.  
##### 이런 영역에 대해 순서를 지켜주자는 것이 동기화 synchronization.
##### "네가 먼저 ~하고, 내가 나중에 ~할게" 하면서 race condition. 그래서 critical section에는 한번에 하나만 들어갈 수 있음

<br>

#### :triangular_flag_on_post: 순자척인 임계영역 접근

<img src="https://user-images.githubusercontent.com/74708028/110880049-5a797200-8321-11eb-9211-d6073a6fabac.jpg" width="700" height="350"/>


<br>

### :round_pushpin: 동기화 (synchronization)? 
#### 임계 영역에 여러 thread가 접근하는 경우, 한 thread가 수행하는 동안 공유 자원을 lock하려 다른 thread의 접근을 막음
#### 잘못 구현하면 deadlock에 빠질 수 있음

#### :triangular_flag_on_post: 자바에서 동기화구현
##### synchronized 수행문과 synchronized 메서드를 이용
 * ##### synchronized 메서드 : 현재 이 메서드가 속해있는 객체에 lock을 건다. 
   #####                       synchronized메서드 내에서 다른 synchronized 메서드를 호출하지 않는다.(deadlock 방지위해)
	    synchronized 수행문
		synchronized(*참조형 수식*){}
	    => 참조형 수식에 해당되는 객체에 lock을 건다
	
	
#### :triangular_flag_on_post:deadlock

<img src="https://user-images.githubusercontent.com/74708028/110880759-792c3880-8322-11eb-9551-32e4a6841fa5.jpg" width="800" height="480"/>

### :computer: 동기화구현 해보기

![Chapter 15 자바 Thread 프로그래밍 - 03 multi-thread 프로그래밍_페이지_07](https://user-images.githubusercontent.com/74708028/110888289-39b81900-832f-11eb-9052-7aa526a7487c.png)

<br>

-------------------------------------------

<br>


### :round_pushpin: Thread의 여러가지 메서드 활용
#### Thread status

<img src="https://user-images.githubusercontent.com/74708028/110876513-f6ec4600-831a-11eb-9236-72b117739c4e.jpg" width="800" height="480"/>

<br>

### :round_pushpin: Thread 우선순위
#### Thread.MIN PRIORITY(=1) ~ Thread.MAX PRIORITY(=10)
#### 디폴트 우선 순위 : Thread.NORM_PRIORITY (=5)
#### 우선 순위가 높은 thread는 CPU를 배분 받을 확률이 높음(주려면 높게 확 주어야함)
	 setPriority(int newPriority)
	 int getPriority()
	
```java

     //생략...

public class ThreadTest {

	public static void main(String[] args) {

		Thread t = Thread.currentThread();  // Thread[main,5,main] => [쓰레드 이름, 디폴트 우선순위 5, thread가 속해있는 곳]
		System.out.println(t);
		
	}
}
```

<br>

#### :triangular_flag_on_post: wait()/notify() 메서드(Object의 메서드)
* ##### wait(): 리소스가 더 이상 유효하지 않은 경우 리소스가 사용 가능할 때까지 기다리기위해
  ##### thread를 non-runnable 상태로 전환.
  ##### wait()상태가 된 thread은 notify()가 호출될 때까지 기다린다.
* ##### notity() : wait()하고 있는 thread 중 아무 thread를 runnable한 상태로 깨움
* ##### notifyAll() : wait()하고 있는 모든 thread가 runnable 한 상태가 되도록 함.
  ##### notify() 보다 notifyAll()사용권장. 
  ##### 특정 thread가 통지를 받도록 제어할 수 없으므로 모두 깨운 후 scheduler에 CPU를 점유하는 것이 좀 더 공평하다고함.
  
  #### :computer: wait()/notify() 메서드 사용해보기
  ![Chapter 15 자바 Thread 프로그래밍 - 03 multi-thread 프로그래밍_페이지_11](https://user-images.githubusercontent.com/74708028/110888090-d1693780-832e-11eb-9e63-aca5f0ec4361.png)

<br>

#### :triangular_flag_on_post: join() 메서드

<img src="https://user-images.githubusercontent.com/74708028/110876621-34e96a00-831b-11eb-88ef-11e7942185b5.jpg" width="430" height="300"/>

* ##### 다른 thread의 결과를 보고 진행해야하는 일이 있는 경우 join() 메서드를 활용
* ##### join() 메서드를 호출한 thread가 non-runnable 상태가 됨
```java
public class JoinTest extends Thread {

	int start;
	int end;
	int total;
	
	public JoinTest(int start, int end) {
		this.start = start;
		this.end = end;
	}
	
	public void run() {
		int i;
		for(i=start; i<=end; i++) {
			total += i;
		}
	}
	
	public static void main(String[] args) {

		JoinTest jt1 = new JoinTest(1, 50);
		JoinTest jt2 = new JoinTest(51, 100);
		
		jt1.start();
		jt2.start();
		
		try {
			jt1.join();	//join 넣지 않으면 total이 제대로 나오지않음. jt1의 계산 수행을 기다렸다가 jt2의 수행이 시작.
			jt2.join();
		} catch (InterruptedException e) {
			e.printStackTrace();
		}
		
		
		int total = jt1.total  + jt2.total;
		System.out.println( "jt1.total = "  + jt1.total );
		System.out.println( "jt2.total = "  + jt2.total );
		
		System.out.println(total);
	}
}
```

<br>

#### :triangular_flag_on_post: interrupt() 메서드
* ##### 다른 thread에 예외를 발생시키는 interrupt를 보냄
* ##### thread가 join(), sleep(), wait() 메서드에 의해 블럭킹 되었다면 interrupt에 의해 다시 runnable상태가 될 수 있음

```java
public class InterruptTest extends Thread{
	
	public void run() {
		
		int i;
		for(i=0; i<100; i++) {
			System.out.println(i);
		}
		
		try {
			sleep(5000);
		} catch (InterruptedException e) {
			System.out.println(e);
			System.out.println("Wake!!!");
		}
	}

	public static void main(String[] args) {

		InterruptTest test = new InterruptTest();
		test.start();
		test.interrupt();  
		// 선언하지 않은 경우 : 99까지 출력되고 sleep(5초)하다가 ending
		// interrupt 선언한 경우 : 예외 발생해 catch 처리되고 wake!!! 출력.
		
		System.out.println("end");
	}

}
```

<br>

### :round_pushpin: thread 종료하기
* #### 데몬 등 무한반복하는 thread가 종료될 수 있도록 run() 메서드 내의 while 문을 활용.
* #### Thread.stop()은 사용하지않음
```java
public class TerminateThread extends Thread{

	private boolean flag = false; //true가 되면 Not이 되면서 멈춤
	int i;
	
	public TerminateThread(String name) {
		super(name);  //flag thread 컨스트럭트 중, 이름을 받을 수 있음
	}
	
	public void run() {
		while( !flag ) { //true일 때까지! 
			
			try {
				sleep(100);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
		
		System.out.println(getName() +  " end");
	}
	
	public void setFlag(boolean flag) {
		this.flag = flag;
	}
	
	public static void main(String[] args) throws IOException {
		
		TerminateThread threadA = new TerminateThread("A");
		TerminateThread threadB = new TerminateThread("B");
		
		threadA.start();
		threadB.start();
		
		int in;
		while(true) {
			in = System.in.read();
			if ( in == 'A') {
				threadA.setFlag(true);
			}
			else if(in == 'B') {
				threadB.setFlag(true);
			}else if (in == 'M') {
				threadA.setFlag(true);
				threadB.setFlag(true);
				break;
			}
			/*else {
				System.out.println("try again");  \n \r
			}*/
		}
		System.out.println("main end");
	}
}

```


