### 📌 Proxy Pattern
##### Proxy는 대리인이라는 뜻으로써, 뭔가를 대신해서 처리하는 의미이다. 
##### Proxy Pattern 에서는 Proxy class를 통해서 대신 전달하는 형태 로 설계되며, 
##### 실제 Client는 Proxy로부터 결과를 받는다.

<br>
<br>

#### Proxy Pattern을 Cache 기능으로 활용한 예를 살펴보자.
 
#### IBrowser 인터페이스

```java
public interface IBrowser {
    Html show();
}
```

<br>

##### Html 클래스

```java
public class Html {
    private String url;

    public Html(String url){
        this.url=url;
    }

}

}
```

<br>

#####  IBrowser 인터페이스를 구현한 Browser 클래스

```java

public class Browser implements IBrowser{

    private String url;

    public Browser(String url){
        this.url = url;
    }

    @Override
    public Html show() {
        System.out.println("browser loading html from : "+url);
        return new Html(url);
    }
}

```



<br>

#####  Proxy 역할을 하는 BrowserProxy 클래스


```java
public class BrowserProxy implements IBrowser{

    private String url;
    private Html html;

    public BrowserProxy(String url){
        this.url=url;
    }

    @Override
    public Html show(){
        if(html == null){
            this.html = new Html(url);
            System.out.println("BrowserProxy loading html from : "+url);
        }
        System.out.println("BrowserProxy use cache : "+url);
        return html;
    }
}
```

<br>

#####  IBrowser인터페이스를 구현한 AopBrowser

```java

import com.company.design.proxy.Html;
import com.company.design.proxy.IBrowser;

public class AopBrowser implements IBrowser {

    AOP는 특정한 메소드가 있으면 이 메소드에 실행시간이라던지, 
    특정한 패키지의 특정한 메소드의 실행시간 전후로 기능을 넣을 수 있어서 메소드를 측정할 때 쓰인다.
    
    private String url;
    private Html html;
    private Runnable before;
    private Runnable after;

    public AopBrowser(String url, Runnable before, Runnable after){
        this.url=url;
        this.before=before;
        this.after=after;
    }

    @Override
    public Html show() {
        before.run();

        if(html == null){
            this.html = new Html(url);
            System.out.println("AopBrowser html loading from : "+ url);
            try {
                Thread.sleep(1500);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

        after.run();
        System.out.println("AopBrowser html cache : "+url);
        return html;
    }
}
}
```

```java
public class Main {

   public static void main(String[] args) {
   
//        Browser browser = new Browser("www.naver.com");  결과 1 
//        browser.show();
//        browser.show();
//        browser.show();
//        browser.show();

          Proxy Pattern 을 거치치 않으면

          브라우저에서 요청을 할 때마다 새롭게 로딩을 해야한다. 

          이때 로딩해온 값을 저장 해 놓으면 좋은데, 그 역할을 Proxy 로 해줄 수 있다. 


//        IBrowser browser = new BrowserProxy("www.naver.com"); 결과 2
//        browser.show();
//        browser.show();
//        browser.show();
//        browser.show();
//        browser.show();

          한번 로딩해온 html을 저장해두고 사용한다.

          BrowserProxy loading html from : www.naver.com
          BrowserProxy use cache : www.naver.com
          
          

        //동시성 문제때문에 아토믹을 사용
        AtomicLong start = new AtomicLong();  결과 3
        AtomicLong end = new AtomicLong();

        IBrowser aopBrowser = new AopBrowser("www.naver.com",
                () -> {
                        System.out.println("before");
                        start.set(System.currentTimeMillis());
                },
                ()->  {
                        long now = System.currentTimeMillis();
                        end.set(now-start.get());
                        System.out.println("after");
                }

                );

                aopBrowser.show();
                System.out.println("loding time : "+ end.get());

                aopBrowser.show();
                System.out.println("loding time : "+ end.get());
                
                

    }

}
```

<br>
<br>

##### 📍  Browser browser = new Browser("www.naver.com") 결과 1

<img width="328" alt="다운로드 (1)" src="https://user-images.githubusercontent.com/74708028/120800791-51dcb480-c57b-11eb-98b1-79d14424a053.png">
<br>

##### 📍  IBrowser browser = new BrowserProxy("www.naver.com") 결과 2

<img width="405" alt="다운로드 (2)" src="https://user-images.githubusercontent.com/74708028/120800864-6751de80-c57b-11eb-9993-cac1b17d11f1.png">
<br>

##### 📍  IBrowser aopBrowser = new AopBrowser("www.naver.com" ...생략) 결과 3
<img width="332" alt="다운로드 (3)" src="https://user-images.githubusercontent.com/74708028/120800894-7042b000-c57b-11eb-9d8d-8667c06df6ea.png">


<br>

##### 📢 AOP는 특정한 메소드가 있으면 이 메소드에 실행시간이라던지, 
##### 특정한 패키지의 특정한 메소드의 실행시간 전후로 기능을 넣을 수 있어서 메소드를 측정할 때 쓰인다.
##### show라는 메소드가 걸린 시간이 처음엔 1.5(1513)초
##### 다음에는 cache가 걸려있기 때문에  0 초가 걸리는 것을 알 수가 있다.
##### 이를 통해 cache가 잘 돌아가는 것을 확인할 수 있다.

<br>

##### 📢 AOP패턴은 프록시 패턴을 이용하고있고 특정한 메소드, 특정한 기능의 앞 뒤로 내가 원하는 기능, 
##### 앞뒤로 넘어가는 아규먼트에 대해 조작도 할 수 있으며, 흩어져있는 공통된 기능을 한꺼번에 묶어 줄 수도 있다. 

<br>

##### 📢 HTTP클라이언트와 통신을 한다고하면, HTTP클라이언트의 코드가 흩어져있거나, 
##### REST클라이언트 서비스라던지가 뭉쳐있다고하면 거기에 있는 메소드의 시간 측정한다던지 , 
##### 데이터베이스에 INSERT한다던지, 꺼내와서 작업하는 TRANSACTION 쪽에다가도 시간관련 AOP를 넣어서
##### 현재 시스템이 오래걸리는 위치가 어디인지,
##### 어떤 메소드가 오래걸려서 해당 서비스에 로딩이 걸리는지 파악할 수 있다.
