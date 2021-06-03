### 📌 어뎁터 패턴 Adapter Pattern 
##### Adapter Pattern 에서는 실생활에서 많이 쓰이는 어뎁터를 떠올리면 된다. 
##### 흔히 돼지코라고 불리는데 100v를 200v로 변경해주거나, 그 반대로 해주는 변환기를 뜻한다.

#### 📍  어뎁터 패턴의 원칙
##### 호환성이 없는 기존 클래스의 인터페이스를 변환하여 재사용 할 수 있도록 한다. 
##### SOLID 중에서 개방 폐쇄 원칙OCP를 따른다. 

<br>
<br>

##### Electronic110v 인터페이스

```java
public interface Electronic110v {

    void powerOn();
}

```


##### Electronic220v 인터페이스

```java
public interface Electronic220v {

    void connect();
}
```

##### Electronic110v 인터페이스를 구현한 HairDryer 클래스

```java
public class HairDryer implements Electronic110v{
    @Override
    public void powerOn(){
        System.out.println("헤어 드라이기 100v on");
    }
}
```


##### Electronic220v 인터페이스를 구현한 AirConditioner 클래스

```java
public class AirConditioner implements Electronic220v{
    @Override
    public void connect() {
        System.out.println("에어컨 220v on");
    }
}
```

##### Electronic220v 인터페이스를 구현한 Cleaner 클래스

```java
public class Cleaner implements Electronic220v{

    @Override
    public void connect() {
        System.out.println("청소기 220v on");
    }
}
```

##### 220v를 110v로 바꿔주는 어뎁터 클래스

```java
package com.company.design.adepter;

public class SocketAdepter implements Electronic110v{

    private Electronic220v electronic220v;

    public SocketAdepter(Electronic220v electronic220v){
        this.electronic220v = electronic220v;
    }
    
    @Override
    public void powerOn() {
        electronic220v.connect();
    }
}

```

##### Main 클래스

```java
public class Main {

    public static void main(String[] args) {
    
        HairDryer hairDryer = new HairDryer(); // 110v 구현 클래스 생성
        connect(hairDryer); 

        Cleaner cleaner = new Cleaner();
        //connect(cleaner);
        //오류가 뜸. connect()은 매개변수로 Electronic110v만 받을 수 있는데 Cleaner 객체는 220v를 상속받았기 때문이다
        //220v를 110v로 바꿔주는 돼지코가 필요한 상황이다.
        
        //SocketAdepter를 이용한다.
        Electronic110v adapter = new SocketAdepter(cleaner);
        connect(adapter);
        // => 자기 자신(Cleaner) 은 변하지 않고 중간에 인터페이스로 맞추는 형식 = adepter pattern

        AirConditioner airConditioner = new AirConditioner();
        Electronic110v airAdepter = new SocketAdepter(airConditioner);
        connect(airAdepter);
    }

    public static void connect(Electronic110v electronic110v){ Electronic110v만 받을 수 있음
        electronic110v.powerOn();
    }

}
```

##### => 자기 자신(Cleaner) 은 변하지 않고 중간에 인터페이스로 맞추는 형식 = adepter pattern
