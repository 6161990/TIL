## :pushpin: List 인터페이스
 ### Collection 하위 인터페이스 [컬렉션 프레임워크](https://github.com/6161990/TIL/blob/main/Java/Collection%20Framework.md)
 ### 객체를 순서에 따라 저장하고 관리하는데 필요한 메서드가 선언된 인터페이스
 
  #### :round_pushpin: Set과의 차이 : 1. 순서 2. 중복의 유무 
* #### 배열의 기능을 구현하기 위한 메서드가 선언됨.
* #### ArrayList, Vector, LinkedList

<br>

#### :round_pushpin: ArrayList와 Vector 
* ##### 객체 배열 클래스
* ##### Vector는 자바 2부터 제공된 클래스
* ##### 일반적으로 ArrayList를 더 많이 사용
* ##### Vector는 멀티 쓰레드 프로그램에서 동기화를 지원
* ##### 동기화(synchronization) : 두 개의 쓰레드가 동시에 하나의 리소스에 접근할 때 
  #####                          순서를 맞추어서 데이터의 오류가 나지 않도록 방지.
* ##### capacity와 size는 다른 의미임 
  ##### capacity는 배열의 용량 , 만들어진 ArrayList의 용량이 꽉 차면, 뻥튀기 시켜서 더 큰 것을 만듦.
  ##### 거기에 원래 있던 data를 복사함. 사용자는 이에 상관없이 add하면 됨.
  ##### size는 그 안에 들어간 요소 갯수
 <img src="https://user-images.githubusercontent.com/74708028/110307804-ad61d980-8042-11eb-9199-66117b41e77f.jpg" width="900" height="550">   


<br>

#### :round_pushpin: ArrayList와 LinkedList
* ##### 둘 다 자료의 순차적 구조를 구현한 클래스
* ##### ArrayList는 배열을 구현한 클래스로 논리적 순서와 물리적 순서가 동일함
  ##### ArrayList의 장점 : i번째 요소를 찾기 쉬움
* ##### LinkedList는 논리적으로 순차적인 구조지만, 물리적으로는 순차적이지 않을 수 있음
* ##### LinkedList의 장점 : 자료의 추가와 삭제가 빠름  
* ##### LinkedList의 구조 
<img src="https://user-images.githubusercontent.com/74708028/110307717-958a5580-8042-11eb-8fec-f039a4f7b9bd.jpg" width="700" height="450"> 

```java
public class LinkedListTest {

	public static void main(String[] args) {

		LinkedList<String> myList = new LinkedList<String>();
		
		myList.add("A");
		myList.add("B");
		myList.add("C");
		
		System.out.println(myList);  //[A,B,C]
		myList.add(1, "D");
		System.out.println(myList);  //[A,D,B,C]	
		myList.removeLast();
		System.out.println(myList);  //[A,D,B]	
		
		for(int i=0; i<myList.size(); i++) {
			String s = myList.get(i);
			System.out.println(s); // A, D, B
		}
	}
}
```
