### 바이트 단위 입출력 스트림 Byte IO Stream
#### InputStream : 바이트 단위 입력 스트림 최상위 클래스
#### OutputStream : 바이트 단위 출력 스트림 최상위 클래스 
##### => 위 기반 클래스는 추상 메서드를 포함한 추상 클래스로, 아래 하위 클래스가 구현하여 사용 
###### 입력 보조 스트림
* ###### FileInputStream : 파일에서 바이트 단위로 자료를 읽습니니다
* ###### ByteArrayInputStream : Byte 배열 메모리에서 바이트 단위로 자료를 읽습니다
* ###### FilterInputStream : 기반 스트림에서 자료를 읽을 때 추가 기능을 제공하는 보조 스트림의 상위 클래스입니다
###### 출력 보조 스트림
* ###### FileOutputStream : 바이트 단위로 파일에 자료를 씁니다
* ###### ByteArrayOutputStream : Byte 배열에 바이트 단위로 자료를 씁니다
* ###### FilterOutputStream : 기반 스트림에서 자료를 쓸 때 추가 기능을 제공하는 보조 스트림의 상위 클래스입니다


#
**FileInputStream과 FileOutputStream 사용하기**
###### 파일에 한 바이트씩 자료를 읽고 쓰는데 사용 
* ###### 문자는 읽지못하기 때문에 한글처럼 멀티바이트로 fileReader, fileWriter를 써야한다.
* ###### 입력 스트림은 파일이 없는 경우 예외 발생
* ###### 출력 스트림은 파일이 없는 경우 '파일 생성하여' 출력

#
**flush()와 close()메서드**
* ###### 출력용 버퍼를 비울 때 flush()메서드 호출
* ###### 파일 스트림을 닫기위한 close()메서드가 호출되면 내부에서 flush()를 호출하며 출력 버퍼를 비움
