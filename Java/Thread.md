### 쓰레드 Thread

<img src="https://user-images.githubusercontent.com/74708028/110875195-85ab9380-8318-11eb-9b00-1c3f786c6478.jpg" width="500" height="300"/>


* #### Process : 실행중인 프로그램, OS로부터 메모리를 할당 받음
  #### => 하나의 프로그램은 process가 돼서 메모리에 올라가게됨. process가 실행되는 단계가 thread 
* #### Thread : 실제 프로그램이 수행되는 작업의 최소 단위, 하나의 프로세스는 하나 이상의 Thread를 가지게됨.
  #### => cpu를 점유하는 scheduler가 thread에 cpu할당을 통해 thread가 수행되도록함.
#
**자바 Thread클래스로 부터 상속받아 구현**
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
###### => 자바는 다중 상속이 허용되지 않으므로 이미 다른 클래스를 상속한 경우, 
######     thread를 만들려면 Runnable interface를 implements 하도록한다.
#
**Runnable 인터페이스로 구현**
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
#
**Multi-thread 프로그래밍**
###### 동시에 여러 개의 Thread가 수행되는 프로그래밍
* ###### Thread는 각각의 작업공간(context)를 가짐 -> thread가 swith되면 작업공간도 swith 된다.
* ###### 공유 자원이 있는 경우 race condition이 발생
* ###### critical section에 대한 동기화(synchronization)의 구현이 필요, 아니면 충돌한다.
<img src="https://user-images.githubusercontent.com/74708028/110875364-d3c09700-8318-11eb-95f3-571fc78c57fe.jpg" width="350" height="200"/>


##### critical section? 
###### shared resource는 여러가지 thread가 있을 떄, 공유하는 자원.
###### 같이 쓰다보니까 오류가 날 수도 있다.
###### 이런 영역에 대해 순서를 지켜주자는 것이 동기화 synchronization.
###### "네가 먼저 ~하고, 내가 나중에 ~할게" 하면서 race condition
###### 그래서 critical section에는 한번에 하나만 들어갈 수 있음

----------------------
#### Thread의 여러가지 메서드 활용
**Thread status**

<img src="https://user-images.githubusercontent.com/74708028/110876513-f6ec4600-831a-11eb-9236-72b117739c4e.jpg" width="700" height="480"/>

**Thread 우선순위**
##### Thread.MIN PRIORITY(=1) ~ Thread.MAX PRIORITY(=10)
##### 디폴트 우선 순위 : Thread.NORM_PRIORITY (=5)
###### setPriority(int newPriority)
###### int getPriority()
###### 우선 순위가 높은 thread는 CPU를 배분 받을 확률이 높음(주려면 높게 확 주어야함)
```java

     //생략...

public class ThreadTest {

	public static void main(String[] args) {

		Thread t = Thread.currentThread();  // Thread[main,5,main] => [쓰레드 이름, 디폴트 우선순위 5, thread가 속해있는 곳]
		System.out.println(t);
		
	}
}
```
**join() 메서드**
<img src="https://user-images.githubusercontent.com/74708028/110876621-34e96a00-831b-11eb-88ef-11e7942185b5.jpg" width="430" height="300"/>

##### 다른 thread의 결과를 보고 진행해야하는 일이 있는 경우 join() 메서드를 활용
##### join() 메서드를 호출한 thread가 non-runnable 상태가 됨


