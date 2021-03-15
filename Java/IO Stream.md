## :pushpin: 입출력 스트림 I/O Stream
###### 참고 : [표준 입출력 스트림](https://github.com/6161990/TIL/blob/main/Java/Standard%20InputOutput%20Stream.md)
* #### 네트워크에서 자료의 흐름이 물과 같다는 의미에서 유래
* #### 다양한 입출력 장치에 독립적으로 일관성있는 입출력 방식 제공
* #### 입출력이 구현되는 곳에서는 모두 I/O 스트림을 사용
  ##### 키보드, 파일디스크, 메모리 등

<br>

### :round_pushpin: 입출력 스트림 구분
#### 입출력을 같이 하는 스트림은 없다. 입력이든지 출력이든지 하나만 담당
* ##### I/O 대상 기준 : 입력 스트림, 출력 스트림
* ##### 자료의 종류 : 바이트 스트림, 문자 스트림
* ##### 스트림의 기능 : 기반 스트림, (기반 스트림을 Support 하는)보조 스트림

<br>

### :round_pushpin: 입출력 스트림과 출력 스트림(I/O 대상 기준에 따른 스트림)
* #### 입력 스트림: 대상으로부터 자료를 읽어들이는 스트림
* #### 출력 스트림: 대상으로부터 자료를 출력하는 스트림
* #### 스트림의 예 
* ##### 입력 스트림 : FileInPutStream, FileReader, BufferedInputStream, BufferedReader 등
* ##### 출력 스트림 : FileOutputStream, FileWriter, BufferedOutputStream, BufferedWriter 등
   ###### 접미사 InPutStream, FileOutputStream 은 Byte 단위.
   ###### 접미사 Reader, Writer 는 문자 단위. 
   ###### 접두사 File은 어떤 목적지가 있는 기반스트림.
   ###### 접두사 Buffered는 버퍼링 제공하는 보조스트림.

<br>

### :round_pushpin: 자료의 종류에 따른 스트림

<img src="https://user-images.githubusercontent.com/74708028/110724468-2e92b980-8259-11eb-914b-72fa2671cd5b.jpg" width="450" height="290"/>

* #### 바이트 단위 스트림 : 바이트 단위로 자료를 읽고 씀 (동영상, 음악파일 등)
* #### 문자 단위 스트림 : 문자는 2 바이트씩 처리해야함
* #### 스트림의 예 
* ##### 바이트 스트림 : FileInPutStream, FileOutputStream, BufferedInputStream, BufferedOutputStream 등
* ##### 문자 단위 스트림 : FileReader, FileWriter, BufferedReader, BufferedWriter 등

<br>

### :round_pushpin: 기능에 따른 스트림

<img src="https://user-images.githubusercontent.com/74708028/110588681-b5dc2080-81b8-11eb-84cc-0ef99ca58181.jpg" width="470" height="290"/>


* #### 기반스트림 : 대상에 직접 자료를 읽고 쓰는 기능의 스트림
* #### 보조스트림 : 직접 읽고 쓰는 기능은 없고 추가적인 기능을 제공해주는 스트림
  ####             기반 스트림이나 또 다른 보조 스트림을 생성자의 매개변수로 포함함
* #### 스트림의 예 
* ##### 기반스트림 : FileInPutStream, FileOutputStream, FileReader, FileWriter 등
* ##### 보조스트림 : InPutStreamReader, OutputStreamWriter, BufferedInputStream, BufferedOutputStream 등

<br>

### :round_pushpin: 그 외 입출력 클래스
* #### File 클래스 : 파일 개념을 추상화한 클래스 , 입출력 기능은 없고 파일의 속성, 경로, 이름 등을 알 수 있음
* #### RandomAccessFile 클래스 : 입출력 클래스 중 유일하게 파일 입출력을 동시에 할 수 있는 클래스
                            #### 파일 포인터가 있어서 읽고 쓰는 위치의 이동이 가능함. 다양한 자료형에 대한 메서드가 제공됨. 
  
  ![Chapter 14 자바 입출력 - 07 그 외 입출력 클래스와 데코레이터 패턴 (1)_페이지_4](https://user-images.githubusercontent.com/74708028/110743331-3bc0a000-827b-11eb-960d-453997cb8a25.png)
