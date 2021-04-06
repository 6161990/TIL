### :pushpin: 문자 단위 스트림 String IO Stream
* ##### Reader : 문자 단위로 읽는 최상위 스트림, Input
* ##### Writer : 문자 단위로 쓰는 최상위 스트림, Output
##### => 위 기반 클래스는 추상 메서드를 포함한 추상 클래스로, 아래 하위 클래스가 구현하여 사용 

<br>

#### :round_pushpin: 입력 보조 스트림
* ##### FileReader : 파일에서 문자 단위로 자료를 읽는 스트림 클래스입니다
* ##### InputStreamReader : 바이트 단위로 읽은 자료를 문자로 변환해주는 보조 스트림 클래스 입니다.
* ##### BufferedReader : 문자로 읽을 때 배열을 제공하여 한꺼번에 읽을 수 있는 기능을 제공해주는 보조 스트림입니다.

<br>

##### :round_pushpin: 출력 보조 스트림
* ##### FileWriter : 파일에 문자 단위로 출력하는 스트림 클래스입니다
* ##### OutputStreamWriter : 파일에 바이트 단위로 출력한 자료를 문자로 변환해주는 보조 스트림입니다
* ##### BufferedWriter : 문자로 쓸 때 배열을 제공하여 한꺼번에 쓸 수 있는 기능을 제공해주는 보조 스트림입니다


<br>

#### :round_pushpin: FileReader와 FileWriter 사용하기
##### 파일에 문자를읽고 쓸 때 가장 많이 사용하는 클래스
##### 문자의 인코딩 방식을 지정할 수 있음

![Chapter 14 자바 입출력 - 04 문자 단위 입출력 스트림_페이지_5](https://user-images.githubusercontent.com/74708028/110724091-7a912e80-8258-11eb-9700-346556461fe3.png)


