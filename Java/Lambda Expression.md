## :pushpin: 람다식 
### 자바에서 함수형 프로그래밍(functional programming)을 구현하는 방식
* #### 클래스를 생성하지 않고 함수의 호출만으로 기능을 수행
* #### 함수형 인터페이스를 선언함
  #### => 함수 기반의 프로그래밍을 하는데 매개변수를 받아서 그걸로 프로그래밍을 하게되면 외부변수들을 사용하지않음
  #### => "순수 함수형 프로그래밍", 내부적으로는 익명함수가 만들어며 병렬처리가 가능해짐
* #### 자바 8부터 지원되는 기능

<br>

  #### :triangular_flag_on_post: 병렬처리?
  #### ex)이 함수가 돌아감으로써 다른 매개변수가 변한다든가하는 발생이 없음.

<br>

#### :round_pushpin: 함수형 프로그래밍이란?
* ##### 순수 함수(pure function)를 구현하고 호출
* ##### 매개 변수만을 사용하도록 만든 함수로 외부 자료에 부수적인 영향(side effect)가 발생하지 않도록 함
* ##### 입력 받은 자료를 기반으로 수행되고 외부에 영향을 미치지 않으므로 병렬처리 등에 가능.
  ##### => 입력받은 자료를 기반으로 수행되니까 똑같은 자료들을 입력하면 항상 수행결과가 같음.
  ##### => 다양한 자료가 있을 때 동시에 돌릴 수 있는 병렬처리가 가능한 이유.
* ##### 안정적이며 확장성있는 프로그래밍 방식

<br>

#### :round_pushpin: 람다식 문법
  ##### ' -> ' 화살표 오퍼레이터 : "이 매개변수를 이렇게 구현해라"
* ###### 매개 변수하나인 경우 괄호 생략가능 ( 두 개인경우는 괄호를 생략할 수 없음)

        str -> {System.out.println(str);}
* ###### 중괄호 안의 구현부가 한 문장인 경우 중괄호 생략

        str -> System.out.println(str);
* ###### 중괄호 안의 구현부가 한 문장이라도 return 문은 중괄호를 생략할 수 없음 

        str-> return str.length(); //오류
* ###### 중괄호 안의 구현부가 반환문 하나라면 return과 중괄호를 모두 생략할 수 있음

         (x, y) -> x+y       // 두 값을 더하여 반환 
         str-> str.length() // 문자열 길이를 반환12내부 클래스, 람다식, 스트림

<br>

#### :round_pushpin: 함수형 인터페이스
* ##### 람다식을 선언하기 위한 인터페이스
* ##### @FuctionalInterface 애노테이션 사용
* ##### 익명 함수와 매개변수만으로 구현되므로 단 하나의 메서드만을 선언해야함
  ##### (두 개 이상의 메서드가 선언되면 어느 메서드의 호출인지 모호해짐)
```java
@FuctionalInterface
public interface MyMaxNumber{
  int getMaxNumber(int x , int y);
  void add(int x, int y);
}
```
```java
public class TestMyNumber{
  public static void main(String[] args){
    MyMaxNumber max = (x,y) -> (x >= y) x: y;
    System.out.println(max.getMaxNumber(10,20));
  }
}
```

<br>

#### :round_pushpin: 함수를 변수처럼 사용하는 람다식
##### 프로그램에서 변수는

          자료형에 기반하여 선언하고 int a;
          매개변수로 전달하고 int add(int x, int y);
          메서드의 반환 값으로 사용 return num;
##### 람다식은 프로그램내에서 변수처럼 사용할 수 있음
```java
    StringConcat concat = (s,v)-> System.out.println(s+","v);  //함수 구현부인데 변수에 대입
    concat.makeString("hello","world");
```

<br>

#### :triangular_flag_on_post: 람다식 정리


![Chapter 12 내부 클래스, 람다식, 스트림 - 02 람다식 (1)_페이지_8](https://user-images.githubusercontent.com/74708028/110442444-325df900-80fe-11eb-8555-5c4297e5ddf7.png)
![Chapter 12 내부 클래스, 람다식, 스트림 - 02 람다식 (1)_페이지_9](https://user-images.githubusercontent.com/74708028/110442460-35f18000-80fe-11eb-9c81-0c433b65e659.png)
