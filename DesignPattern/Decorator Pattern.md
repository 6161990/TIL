
### 데코레이터 패턴 Decorator Pattern 
###### 참고: [보조 입출력 스트림](https://github.com/6161990/TIL/blob/main/Java/Decorator%20Stream.md)
#### 자바의 입출력 스트림은 데코레이터 패턴을 사용
#### 실제 입출력 기능을 가진 객체(컴포넌트)와 그 외 다양한 기능을 제공하는 데코레이터(보조스트림)을 사용하여
#### 다양한 입출력 기능을 구현
#### => 상속보다 유연한 확장성을 가짐, 지속적인 서비스의 증가와 제거가 용이함 
#### 보조스트림에서 실제 읽고 쓰는 기반 스트림이 아닌, 그의 보조적인 기능을 지원하는 패턴
<img src="https://user-images.githubusercontent.com/74708028/110726518-dd84c480-825c-11eb-8973-5e9f9186dad2.jpg" width="700" height="305"/>

<img src="https://user-images.githubusercontent.com/74708028/110743740-e2a53c00-827b-11eb-85a9-fc3a25893147.jpg" width="700" height="430"/>

#
**데코레이터 패턴을 활용하여 프로그래밍**

<img src="https://user-images.githubusercontent.com/74708028/110743992-4def0e00-827c-11eb-95d3-3c82c6262296.jpg" width="700" height="430"/>
![Chapter 14 자바 입출력 - 07 그 외 입출력 클래스와 데코레이터 패턴 (1)_페이지_9](https://user-images.githubusercontent.com/74708028/110744000-50516800-827c-11eb-86e0-ddb67421cf0d.png)
