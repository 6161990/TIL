### 컬렉션 프레임워크 Collection Framework
* #### 프로그램 구현에 필요한 자료구조와 알고리즘을 구현해 놓은 라이브러리
###### 자료구조 : 메모리 위에 data들이 있는데 그것들을 어떻게 관리할 것이냐
###### 알고리즘 : 수행 속도나 얼마나 최적의 솔루션을 찾느냐 
* #### java.util 패키지에 구현되어 있음
* #### 개발에 소요되는 시간을 절약하고 최적화된 라이브러리를 사용할 수 있음
* #### Collection 인터페이스와 Map 인터페이스로 구성됨


<img src="https://user-images.githubusercontent.com/74708028/110276692-09af0400-8017-11eb-932c-4173ac2e4efb.jpg" width="650" height="300">
 
#
**Collection 인터페이스**
###### **하나의 객체** 관리를 위해 선언된 인터페이스로 필요한 기본 메서드가 선언되어있음
###### 하위에 List, Set 인터페이스가 있음
* ###### List 인터페이스 : 순서가 있는 자료관리, 중복 허용. 이 인터페이스를 구현한 클래스는 ArrayList, Vector, LinkedList, Stack, Queue 등이 있음.
* ###### Set 인터페이스 : 순서가 정해져있지않음, 중복을 허용하지 않음. 이 인터페이스를 구현한 클래스는 HashSet, TreeSet 등이 있음.

#
**Map 인터페이스**
###### **쌍으로 이루어진** 객체를 관리하는데 필요한 여러 메서드가 선언되어있음
###### Map을 사용하는 객체는 key-value 쌍으로 되어 있고 key는 중복될 수 없음
###### 하위에 Hashtable, HashMap, TreeMap이 있음.
#
**맛보기**
<img src="https://user-images.githubusercontent.com/74708028/110287801-7089e880-802a-11eb-8b7f-e2651aa0f794.png" width="550" height="700">
#
**컬렉션 프레임워크 생활코딩 **
![Chapter 11 컬렉션 프레임워크 - 02 컬렉션 프레임워크란_페이지_07](https://user-images.githubusercontent.com/74708028/110283485-821bc200-8023-11eb-9334-b9c8874d776f.png)

![Chapter 11 컬렉션 프레임워크 - 02 컬렉션 프레임워크란_페이지_08](https://user-images.githubusercontent.com/74708028/110283528-9495fb80-8023-11eb-8b21-dea052df6ef5.png)
![Chapter 11 컬렉션 프레임워크 - 02 컬렉션 프레임워크란_페이지_09](https://user-images.githubusercontent.com/74708028/110283533-965fbf00-8023-11eb-9ac2-7f4db34a391d.png)
![Chapter 11 컬렉션 프레임워크 - 02 컬렉션 프레임워크란_페이지_10](https://user-images.githubusercontent.com/74708028/110283549-9b247300-8023-11eb-977f-b6ae1ea94187.png)
![Chapter 11 컬렉션 프레임워크 - 02 컬렉션 프레임워크란_페이지_11](https://user-images.githubusercontent.com/74708028/110283559-9d86cd00-8023-11eb-9dec-be3939235ad1.png)
![Chapter 11 컬렉션 프레임워크 - 02 컬렉션 프레임워크란_페이지_12](https://user-images.githubusercontent.com/74708028/110283565-a081bd80-8023-11eb-9326-1b4a056e5c4b.png)
![Chapter 11 컬렉션 프레임워크 - 02 컬렉션 프레임워크란_페이지_13](https://user-images.githubusercontent.com/74708028/110283573-a24b8100-8023-11eb-91d9-63dbffb13447.png)
