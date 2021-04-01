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

#### :checkered_flag: 1단계 ) 컨테이너 객체 생성하기
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

