### :pushpin: GUI, Graphic User Interface
#### 자바에서는 GUI 프로그래밍(윈도우 프로그래밍)을 위한 도구로 다양한 컴포넌트 API를 제공한다. 
#
##### :round_pushpin: AWT (Abstract Window Toolkit)
* ##### AWT는 java 전용 컴포넌트가 아닌 OS용 컴포넌트로 표현되는 것이 특징이다. 즉, 실행환경 OS에 따라 GUI 화면의 모양이 다르다라는 단점이 있다.
#
##### :round_pushpin: Swing
* ##### 자바 AWT를 확장한 GUI 프로그래밍 도구이다. AWT보다 더 많은 종료의 컴포넌트를 제공하며,  
  ##### OS용 컴포넌트를 사용하지 않고 Java 전용 컴포넌트를 사용한다는 것이 특징이다.
* ##### OS가 달라져도 자바 컴포넌트의 GUI 모양이 달라지지 않는다. Swing J 컴포넌트는 AWT 컴포넌트의 후손이다. 
* ##### 클래스명 앞에 J를 붙여서 AWT와 구분한다. 

<br>

####  :round_pushpin: Container와 Conponent
<img width="501" alt="11" src="https://user-images.githubusercontent.com/74708028/113366441-24fdfc80-9394-11eb-80b4-b8f09094b376.png">

* ##### Container : 다른 컴포넌트를 포함할 수 있는 GUI 컴포넌트이다.다른 컨테이너에 포함될 수도 있다. 다른 컨테이너에 속하지 않고 
  ##### 독립적으로 존재 가능하며, 스스로 화면에 자기 자신을 출력하는 컨테이너로는 JFrame, JDialog, JApplet이 있다.
* ##### Conponent : 컨테이너에 포함되어 화면에 출력되는 GUI 객체이다. GUI 컴포넌트의 최상위 클래스는 java.awt.Component클래스이다.
  ##### Swing 컴포넌트의 최상위 클래스는 javax.swing.JComponent이다.

<br>
 
#### :round_pushpin: 작업순서
##### 1. JFrame 을 상속받은 컨테이너 객체 생성함
##### 2. 배치 방식(레이아웃)을 컨테이너에 세팅함 (Layout 설정)
##### 3. 컴포넌트 객체 생성함
##### 4. 지정된 배치 방식에 따라 컨테이너 컴포넌트 배치함 (add)
##### 5. 컴포넌트에 마우스나 키보드 반응에 대한 이벤트 연결 처리함
##### 6. 이벤트 동작에 대한 코드 구현함

<br>

#### :checkered_flag: 1단계 ) 컨테이너 객체 생성
#####  1. JFrame 상속을 이용한 방법
```java
import javax.swing.*;

public class 클래스명 extends JFrame{
  public 클래스명(){
    super("MyMemo");
    //세부 속성 지정
  }
  
  public static void main(String[] args){
    new 클래스명();
  }
}
```
#
#####  2. 상속 받지 않고 객체 생성하기 
```java
import javax.swing.*;

public class 클래스명 {
   public static void main(String[] args){
    JFrame mainFrame = new JFrame("Mymemo");
    //세부 속성 지정
  }
}
```
#
#####  3. JFrame 상속 받은 클래스 작성하고, 실행용 클래스가 실행
```java
import javax.swing.*;

public class extends JFrame {
   public 클래스명(){
    super();
    //세부 속성 지정
  }
}

public class 클래스명{
 public static void main(String[] args){
    클래스명 레퍼런스 new 클래스명();
  }
}
```

#

#### :checkered_flag: 1단계 ) 컨테이너 세부 속성 지정
* ##### setLocation(int x, int y)  : 프레임 위치 설정
* ##### setSize(int width, ing height) : 프레임 사이즈 설정
* ##### setBounds(int x, int y, int width, int height) : 프레임의 위치와 사이즈 동시 설정
* ##### setTitle(String title) : 프레임의 제목 설정
* ##### setIconImage(IconImage) : 프레임 아이콘 이미지 설정
* ##### setDefaultCloseOperation(JFrame, EXIT_ON_CLOSE): 프레임 닫기 버튼 클릭시 종료 기능 연결 동작 설정
* ##### setVisiable(true) : 프레임 보이게 설정(반드시 true)
* ##### setResizable(true) : 프레임 사이즈 조정 활성화 


<br>

#### :checkered_flag: 2단계 ) 컨테이너 배치 방식 지정
##### 1. BorderLayOut
<img width="233" alt="626262" src="https://user-images.githubusercontent.com/74708028/113371971-82994580-93a2-11eb-9782-35942b3b3d82.png">


##### 모두 5개 영역으로 나누고, 각 영역에 하나의 컴포넌트를 넣을 수 있다. 한 영역에 하나 이상의 컴포넌트를 넣고 싶으면 Panel을 사용한다.
##### 2. FlowLayout
<img width="171" alt="dfagd" src="https://user-images.githubusercontent.com/74708028/113367362-c423f380-9396-11eb-9402-e36cf0974523.png">


##### 컴포넌트를 워드프로세서와 같은 방식, 즉 왼쪽에서 오른쪽으로 배치한다. 3가지 정렬방식(왼쪽, 가운데, 오른쪽)이 가능하다.
##### 3. GridLayout
<img width="210" alt="65616" src="https://user-images.githubusercontent.com/74708028/113371976-85943600-93a2-11eb-87d9-de9673e8345b.png">


##### 컴포넌트를 가로, 세로의 일정 수만큼 배치하고자 할 때 주로 사용한다. 행과 열을 지정하고, 각 컴포넌트는 동일한 사이즈를 가진다.
##### 4. CardLayout
<img width="490" alt="55" src="https://user-images.githubusercontent.com/74708028/113367091-1adcfd80-9396-11eb-971a-62682a39ae8a.png">

##### 여러 컨테이너를 슬라이드처럼 바꿔가며 보여줄 수 있다. 앨범이나 퀴즈 또는 설치 프로그램에 주로 사용된다.
##### 5. GridbagLayout
<img width="216" alt="777" src="https://user-images.githubusercontent.com/74708028/113367108-229ca200-9396-11eb-9f6c-90439417b040.png">

##### 컴포넌트의 위치와 크기를 자유롭게 만들 수 있다. 사용하기 매우 복잡하다.

<br>

#### :checkered_flag: 3단계 ) 컴포넌트 객체 생성함

<img width="485" alt="888" src="https://user-images.githubusercontent.com/74708028/113367454-03524480-9397-11eb-82ea-4e6cb13e3d4d.png">

<br>

#### :checkered_flag: 4단계 )  지정된 배치 방식에 따라 컨테이너 컴포넌트 배치함 (add)
<img width="550" alt="20210402060653" src="https://user-images.githubusercontent.com/74708028/113367533-2d0b6b80-9397-11eb-8fa3-7fdb236b5299.png">
<img width="444" alt="xxx" src="https://user-images.githubusercontent.com/74708028/113369813-2ed82d80-939d-11eb-9bef-b7d68bd49c6b.png">


<br>

#### :checkered_flag: 5단계 )  컴포넌트에 마우스나 키보드 반응에 대한 이벤트 연결 처리함
* ##### 이벤트 기반 프로그래밍
  ##### Event Driven 방식의 프로그래밍, 이벤트 발생에 의해 프로그램 흐름이 결정된다.
  ##### 이벤트가 발생하면 이벤트를 처리하는 루틴(이벤트 리스너)이 실행된다. 
* ##### 이벤트의 종류
  ##### 1. 사용자의 입력 : 마우스 드래그, 마우스 클릭, 키보드 누름 등
  ##### 2. 센서의 입력, 네트워크로부터 데이터 송수싱
  ##### 3. 다른 응용프로그램이나 다른 스레드로부터의 메세지 

<br>


#### :round_pushpin: 이벤트처리흐름과 계층 구조
<img width="417" alt="33131" src="https://user-images.githubusercontent.com/74708028/113369937-8d9da700-939d-11eb-9380-099c22132464.png">
<img width="484" alt="945" src="https://user-images.githubusercontent.com/74708028/113369948-942c1e80-939d-11eb-984d-1e675623be8c.png">

<br>


#### :round_pushpin: 이벤트(Event)객체에 포함된 정보
* ##### 이벤트 종류, 소스 
* ##### 이벤트가 발생한 화면 좌표, 컴포넌트 내 좌표
* ##### 버튼이나 메뉴 아이템에 이벤트가 발생한 경우, 버튼이나 메뉴 아이템의 문자열
* ##### 클릭된 마우스 버튼 번호
* ##### 마우의 클릭 횟수
* ##### 눌러진 키의 코드 값과 문자 값
* ##### 체크박스, 라디오 버튼 등과 같은 컴포넌트에 이벤트 발생시, 체크 상태 

<br>


#### :round_pushpin: 이벤트리스너 (Event Listener)
##### 클래스로 작성된 이벤트를 처리하는 코드를 말한다. 이벤트 처리를 위해서는 이벤트 발생을 시킬 컴포넌트에 이벤트 리스너를 연결해야한다. JDK에서 이벤트 리스너 작성을 위한 인터페이스를 제공한다. 
      EX) MouseLister 인터페이스
      interface MouseListener { //5개의 추상 메소드를 제공한다.
          public void mousePress(MouseEvent e); //마우스 버튼 누르는 순간
          public void mouseReleased(MouseEvent e); //눌린 버튼 떼는 순간
          public void mouseClicked(MouseEvent e); //클릭되는 순간
          public void mouseEntered(MouseEvent e); //컴포넌트 안에 들어갈 때
          public void mouseExited(MouseEvent e);  //컴포넌트 밖에 나갈 때
      }

#
#### :round_pushpin: 어뎁터 Adapter 클래스
* ##### 리스너 인터페이스의 추상 메소드를 모두 구현해야 하는 부담을 줄이기 위헤 제공된 클래스이다.
* ##### 리스너의 모든 메소드를 오버라이딩하여 단순 리턴하도록 구현한 클래스이다.
* ##### Adapter 를 상속받은 후손은 구현할 메소드를 선택할 수 있다.
  ##### => 대응하는 어뎁터 클래스가 없으면 리스너 인터페이스 안에 있는 모든 메소드를 전부 오버라이딩해 사용해야한다.

#
#### :round_pushpin: 리스너 연결
* ##### 컴포넌트 객체에 저장된 이벤트 리스너를 연결하면, 이벤트 리스너가 해당 이벤트를 감지하고 자동으로 이벤트 처리 객체로 연결되어 이벤트가 발생한 객체의 정보를 넘긴다. 

        컴포넌트레퍼런스.add이벤트명Listener(이벤트핸들러);
 #
* ##### 이벤트 처리용 클래스 방법
  ##### 1. 별도의 클래스로 작성
  #####   해당 이벤트에 대한 이벤트 리스너 인터페이스를 상속받아야 한다. 
```java
class 클래스명 extends 이벤트 Adapter 또는 implements이벤트명Listener{
   // 컴포넌트 필드 선언;
    
    public 생성자(컴포넌트 전달받음){}
    //해당 인터페이스의 추상메소드들 모두 오버라이딩함
    
    @Override
    public 반환자료형 동작 메소드명(이벤트명Event 레퍼런스){
        //해당 이벤트가 발생한 객체를 골라내서 원하는 동작 처리구문 작성함.
    }
}

```
#
##### 2. 내부 (Inner) 클래스로 작성
#####    현재 클래스 안에 이벤트 핸들러 클래스를 작성한다.
```java
public class 클래스명 extends JFrame {
    //컴포넌트 필드 선언;
    
    //Constructor 작성
    
    class 클래스명 extends 이벤트 Adapter 또는 implements이벤트명Listener{
        @Override
        public 반환자료형 동작 메소드명(이벤트명Event 레퍼런스){
            //해당 이벤트가 발생한 객체를 골라내서 원하는 동작 처리구문 작성함.
        }
    }
}

```
#
##### 3. 무명(익명 : Anonymous) 클래스로 작성
#####    해당 이벤트에 대한 인터페이스를 상속받지 않는다.
```java
컴포넌트레퍼런스.add이벤트 Listener(new 이벤트 Listener() 또는 new 이벤트Adapter(){
      @Override
        public 반환자료형 동작 메소드명(이벤트명Event 레퍼런스){
            //해당 이벤트가 발생한 객체를 골라내서 원하는 동작 처리구문 작성함.
        }
        
        /**사용하지 않는 메소드에 대해서도 다 재구현해야함**/
}
```
##### 4. 프레임 구성 클래스에 인터페이스 상속하여 작성
#####    해당 이벤트에 대한 인터페이스를 상속받지 않는다.
```java
 public class 클래스명 extends JFrame implements 이벤트 인터페이스{
        //컴포넌트에 대한 필드 선언
        //생성자 작성
        public 생성자(){
              //프레임 구성, 컴포넌트 생성 및 배치
              //컴포넌트에 이벤트 리스너 연결하기
              컴포넌트레퍼런스.add이벤트명Listener(this);
        }
        // 상속받은 이벤트 인터페이스의 추상메소드 오버라이딩함
        @Override
        public 반환자료형 동작 메소드명(이벤트명Event 레퍼런스){
            //해당 이벤트가 발생한 객체를 골라내서 원하는 동작 처리구문 작성함.
        }
    }
}
```
