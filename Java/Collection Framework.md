### :pushpin: 컬렉션 프레임워크 Collection Framework
#### 프로그램 구현에 필요한 자료구조와 알고리즘을 구현해 놓은 라이브러리
    * 자료구조 : 메모리 위에 data들이 있는데 그것들을 어떻게 관리할 것이냐
    * 알고리즘 : 수행 속도나 얼마나 최적의 솔루션을 찾느냐 
* #### java.util 패키지에 구현되어 있음
* #### 개발에 소요되는 시간을 절약하고 최적화된 라이브러리를 사용할 수 있음
* #### Collection 인터페이스와 Map 인터페이스로 구성
* ###### 참고 : 하드코딩 vs. 라이브러리 vs. 프레임워크
    * ######    하드코딩 : 내 손으로 한땀한땀 , 떡볶이를 먹고 싶으면 농사를 지어서 밀가루 얻어내고 고추 말려서 고추가루 .....
    * ######     라이브러리 : 누군가가 만들어놓은 도구를 사용, 밀키트! 내가 어떻게 조리하냐에 따라서 달라질 수 있다. 조리는 내가 해야된다.
    * ######     프레임워크 : 틀이 정해져있어서 그대로 사용해야하는 것, 떡볶이 가게에 가서 주문해 먹는 것. 가서 먹기만 할 수 있다.


<img src="https://user-images.githubusercontent.com/74708028/110276692-09af0400-8017-11eb-932c-4173ac2e4efb.jpg" width="650" height="300">
 
<br>

#### :round_pushpin: 배열의 문제점과 collection의 존재이유 
* ##### 문제점  1. 한번 크기를 지정하면 변경할 수 없다. 
   * ##### 기록 시, 배열 공간의 크기가 부족하면 에러가 발생하기 때문에, 배열공간 할당시 미리 넉넉한 크기로 할당을 하게 된다. (메모리낭비있을 수 있음)
   * ##### 한번 할당된 배열 공간은 필요에 따라 늘리거나 줄일 수 없다.
* ##### 문제점 2. 배열에 기록된 데이터에 대한 중간 위치의 추가, 삭제가 불편하다.
   * ##### 배열은 추가/ 삭제 알고리즘이 기본적으로 뒤에 추가, 뒤부터 삭제되는 구조다.
   * ##### 배열에 대해 중간 또는 앞에 추가/ 삭제시에는 기록된 데이터들을 하나씩 뒤로 밀어내거나, 앞으로 한칸씩 이동시키는 처리에 대한 복잡한 알고리즘이 필요하다. 
* ##### 문제점 3. 한 타입의 데이터만 저장가능하다.
#
#### :triangular_flag_on_post:  => 이러한 배열의 문제점을 개선하기 위해 제공된 것이 **_collection_**
* ##### 컬렉션의 장점 1. 저장하는 크기의 제약이 없다.
* ##### 컬렉션의 장점 2. 추가, 삭제, 정렬 등의 기능 처리가 간단하게 해결된다. 
   ##### 자료를 구조적으로 처리하는 자료구조가 내장되어 직접적인 알고리즘 구현이 필요없다.
* ##### 컬렉션의 장점 3. 여러 타입의 객체를 저장할 수 있다. 
   ##### 컬렉션은 객체만 저장하기 때문에, 필요에 따라 기본 자료형 데이터를 저장해야하는경우 Wrapper클래스들을 사용하여 데이터를 박싱Boxing하여 객체로 변환한 다음 저장한다.


#

<br>


#### :round_pushpin: Collection 인터페이스
##### **하나의 객체** 관리를 위해 선언된 인터페이스로 필요한 기본 메서드가 선언되어있음
##### 하위에 List, Set 인터페이스가 있음
* ##### List 인터페이스 : 순서가 있는 자료관리, 중복 허용. 이 인터페이스를 구현한 클래스는 [ArrayList](https://github.com/6161990/TIL/blob/main/Java/Array%20List.md), Vector, LinkedList, Stack, Queue 등이 있음.
    * ###### ArrayList와 Vector : 둘 다 List의 후손이지만, Vector는 동기화를 제공한다. 따라서 List객체들 중에서 가장 성능이 좋지 않다. 
    * ###### LinkedList : List의 후손으로, 인접 참조 링크해서 체인처럼 관리한다. 특정 인덱스에서 객체를 제거하거나 추가하게 되면 바로 앞/뒤 링크만 변경하면 되기 때문에 객체 삭제와 삽입이 빈번하게 일어나는 곳에서는 ArrayList보다 성능이 좋다. 
* ##### Set 인터페이스 : 순서가 정해져있지않음, 중복을 허용하지 않음. 이 인터페이스를 구현한 클래스는 HashSet, TreeSet 등이 있음.

<br>

#### :round_pushpin: Map 인터페이스
##### **쌍으로 이루어진** 객체를 관리하는데 필요한 여러 메서드가 선언되어있음
##### Map을 사용하는 객체는 key-value 쌍으로 되어 있고 key는 중복될 수 없음
##### 하위에 Hashtable, HashMap, TreeMap이 있음.

<br>

#### :round_pushpin: Collection List와 TreeSet, TreeMap의 정렬
* ##### Collection List의 정렬
    * ##### list는 set(TreeSet),map(TreeMap)과 다르게, 객체 안에 필드 값이 여러개 있기 때문에 어떤 필드를 기준으로 오름차순 할건지 내림차순할 건지 결정해야한다. => comparable사용하는 이유
    * #####  java.util.Comparator 인터페이스 상속받는다. 
    * #####  public int compare(Object o1, Object o2){} 메소드 오버라이딩한다.
    * #####  객체의 정렬 기준 필드들의 값 비교 연산 결과를 리턴한다. 
```java
@Override
public int compare(Object o1, Object o2){
//Customer의 name 필드를 기준으로 오름차순 정렬정리하기
  Customer cob1 = (Customer)o1;
  Customer cob2 = (Customer)o2;
  return cob1.getName().compareTo(cob2.getName());
}
```
* ##### TreeSet, TreeMap의 정렬
    * #####  TreeSet의 객체와 TreeMap의 key는 저장과 동시에 자동 오름차순 정렬이된다.
    * #####  숫자(Integer, Double)타입일 경우에는 값으로 정렬되고 문자열(String) 타입일 경우에는 유니코드로 정렬된다. 
    * ##### 정렬을 위해 java.lang.Comparable을 구현한 객체를 요구하기 때문에 Integer,Double, String은 모두 Comparable 인터페이스를 구현해야한다. (ClassCastException 발생)

<br>

#### :triangular_flag_on_post: 맛보기 정리

<img src="https://user-images.githubusercontent.com/74708028/110287801-7089e880-802a-11eb-8b7f-e2651aa0f794.png" width="550" height="700">

-------------------------------------------------------------------------------------

#### :triangular_flag_on_post: 컬렉션 프레임워크 생활코딩
![Chapter 11 컬렉션 프레임워크 - 02 컬렉션 프레임워크란_페이지_07](https://user-images.githubusercontent.com/74708028/110283485-821bc200-8023-11eb-9334-b9c8874d776f.png)

![Chapter 11 컬렉션 프레임워크 - 02 컬렉션 프레임워크란_페이지_08](https://user-images.githubusercontent.com/74708028/110283528-9495fb80-8023-11eb-8b21-dea052df6ef5.png)
![Chapter 11 컬렉션 프레임워크 - 02 컬렉션 프레임워크란_페이지_09](https://user-images.githubusercontent.com/74708028/110283533-965fbf00-8023-11eb-9ac2-7f4db34a391d.png)
![Chapter 11 컬렉션 프레임워크 - 02 컬렉션 프레임워크란_페이지_10](https://user-images.githubusercontent.com/74708028/110283549-9b247300-8023-11eb-977f-b6ae1ea94187.png)
![Chapter 11 컬렉션 프레임워크 - 02 컬렉션 프레임워크란_페이지_11](https://user-images.githubusercontent.com/74708028/110283559-9d86cd00-8023-11eb-9dec-be3939235ad1.png)
![Chapter 11 컬렉션 프레임워크 - 02 컬렉션 프레임워크란_페이지_12](https://user-images.githubusercontent.com/74708028/110283565-a081bd80-8023-11eb-9326-1b4a056e5c4b.png)
![Chapter 11 컬렉션 프레임워크 - 02 컬렉션 프레임워크란_페이지_13](https://user-images.githubusercontent.com/74708028/110283573-a24b8100-8023-11eb-91d9-63dbffb13447.png)
