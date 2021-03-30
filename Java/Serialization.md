### :pushpin: 직렬화 Serialization
* #### 인스턴스의 상태 그대로 저장하거나 네트웍으로 전송하고 이를 다시 복원(Deserialization)하는 방
* #### ObjectInputStream 과 ObjectOutputStream 사용
* #### 이해하기
##### => 어떤 데이터를 전송하기위해 순서대로 하나씩 보내주어야 하는 상황,
#####    예를 들어 에스컬레이터를 데이터 전송을 위한 통로라고 생각한다면,
#####    에스컬레이터에 순서대로 입장을 해야함.
#####    그런데 클래스에 있는 변수들은 순서가 없음
#####    필드 선언되어있고, 값들이 저장되어 있는데 이 값들을 전송하기 위해서는 
#####    어떤 데이터를 어느 순서로 보낼지 결정을 해야함. 
#####    그래야 받는 쪽에서도 어느데이터가 어떤 순서인지 알아야 처음 상태로 복원을 함.
#####    이렇게 일렬로 순서대로 쭉 나열하는 작업이 직렬화.
#####    직렬화가 되면 순서대로 전송을 하면 끄-읏

<br>

#### :round_pushpin: Serializable 인터페이스
##### 직렬화는 인스턴스의 내용이 외부(파일, 네트웤)로 유출되는 것이므로 프로그래머가 객체의 직렬화 가능 여부를 명시함
##### 구현 코드가 없는 mark interface

      class Person implements Serializable{ // 직렬화 하겠다는 의도를 표시
      ...
      String name;
      String job;
      ...
      }


<br>

#### :round_pushpin: Externalizable 인터페이스
##### 구현할 메서드가 있는 인터페이스
##### 프로그래머가 자료를 읽고 쓰는 방식을 직접 구현함

<br>

#### :round_pushpin: 역직렬화
##### 직렬화된 객체를 역직렬화 할 때는 직렬화 했을 때와 같은 클래스를 사용한다. 하지만 클래스의 이름이 같더라도 클래스의 내용이 변경된 경우 역 직렬화에 실패하게 된다. 
##### :triangular_flag_on_post: serialVersionUID 필드
###### 직렬화한 클래스와 같은 클래스임을 알려주는 식별자 역할을 한다. 컴파일시 JVM이 자동으로 serialVersionUID  정적 필드를 추가(컴파일 할때마다 변경됨)해주어 별도로 작성을 하지 않아도 오류는 나지 않는다. 하지만 자동 생성시 역직렬화과정에서 예상하지 못한 InvaildClassException을 유발할 수 있기 때문에 명시를 권장한다. 
      
          private static final long serialVersionUID = -7316658989322446161L;
---------------------------------------------------------------

<br>

#### :triangular_flag_on_post: 직렬화 정리 

![Chapter 14 자바 입출력 - 06 직렬화_페이지_6](https://user-images.githubusercontent.com/74708028/110730243-79193380-8263-11eb-99d9-1b7dda0667d9.png)
