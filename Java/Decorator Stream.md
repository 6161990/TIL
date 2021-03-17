## :pushpin: 보조 스트림 Decorator Stream

###### 참고: [데코레이터 패턴](https://github.com/6161990/TIL/blob/main/DesignPattern/Decorator%20Pattern.md)

###  실제 읽고 쓰는 스트림이 아닌 보조적인 기능을 추가하는 스트림 
* #### FilterInputStream 과 FilterOutputStream이 보조스트림의 상위 클래스
* #### 생성자의 매개 변수로 또 다른 스트림을 가짐
  * ###### protected FilterInputStream(InputStream in) : 생성자의 매개변수로 InputStream을 받습니다.
  * ###### public FilterOutputStream(OutputStream out) : 생성자의 매개변수로 OutputStream을 받습니다.
* #### :triangular_flag_on_post: 데코레이터 패턴 (Decorator Pattern) 
<img src="https://user-images.githubusercontent.com/74708028/110726518-dd84c480-825c-11eb-8973-5e9f9186dad2.jpg" width="700" height="305"/>  

<br>

### :round_pushpin:여러가지 보조스트림 사용하기
* ##### Buffered 스트림 : 내부에 8192 바이트 배열을 가지고 있음. 읽어나 쓸 때 속도가 빠름
* ##### DataInputStream/ DataOutputStream : 자료가 저장된 상태 그대로 자료형을 유지하며 읽거나 쓰는 기능을 제공하는 스트림  


<br>

![Chapter 14 자바 입출력 - 05 보조 스트림_페이지_5](https://user-images.githubusercontent.com/74708028/110728099-c693a180-825f-11eb-90fb-462e242bbe79.png)
![Chapter 14 자바 입출력 - 05 보조 스트림_페이지_6](https://user-images.githubusercontent.com/74708028/110728114-ceebdc80-825f-11eb-928b-d6fe8869d18a.png)


