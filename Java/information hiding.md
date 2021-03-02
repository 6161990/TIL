### 접근제어자 access modifier
* ###### 변수, 메서드, 생성자에 대한 접근 권한 지정.
* ###### private, public protected, 아무것도 안쓰는 경우(기본 접근 제어자: 같은 패키지 내에서만 사용).
* ###### private을 사용하면 클래스 외부에서는 접근할 수 없음.



### 정보은닉 information hiding
* ###### private키워드를 지정해 외부에서 클래스 내부의 정보에 접근하지 못하도록함.
* ###### private변수를 외부에서 접근하게 하려면 public 메서드 제공함. 주로 get,set.
* ###### public 메소드의 기능을 잘 활용해서 정보를 잘 핸들링하면 된다. 
* ###### 클래스 내부 데이터를 잘못 사용하는 오류를 방지할 수 있음. 
* ###### 사용자가 사용하도록 외도된 인터페이스만 사용자가 사용할 수 있게함.
* ###### why 정보은닉을 통해 public 메소드를 가져오는가?
   1. 유효한 data를 가져올 수 있고 
   2. data를 보호할 수 있다

   
   
**접근 제어자를 이용한 정보은닉**
```java
public class MyDate {

  private int day;
  private int month;
  private int year;
  
  private boolean isVaild = true;
  
  public void setDay(int day){
    this.day = day;
  }
  
  public int getDay(){
    return day; 
  }
  
  public int getMonth(){
    return month;
  }
  
  public void setMonth(int month){
    if (month <1 || month > 12 ){
        isVaild = false;
    }
    else 
        this.month = month;
  }
  
  public int getYear(){
    return year;
  }
  
  public void setYear(int year){
    this.year = year;
  }
  
  public void showDate(){
    if(isVaild){
      Systme.out.println(year+ "년" + month + "월" + day + "일 입니다.");
    }  
    else {
      Systme.out.println("유요하지 않은 날짜입니다.");
    }
  } 
}
```

```java
public class MyDateTest {

 	public static void main(String[] args) {
   	   MyDate date = new MyDate();
       
      date.setYear(2019);
      date.setMonth(77);
      date.setDay(100);
    
      date.showDate();
    
      MyDate date2 = new MyDate();
      date2.setYear(2002);  
    
      date2.showDate();
    }
}
```
