### :pushpin: Collection의 개체를 순회하는 인터페이스, Iterator
* #### iterator()메서드 호출 : Set은 순서가 없기 때문에 지정해서 꺼낼 수 없으므로 iterator를 이용한다.

        Iterator ir = memberArrayList.iterator();  
* #### Iterator에 선언된 메서드
   * ##### boolean hashNext() : 이후에 요소가 더 있는지를 체크하는 메서드이며, 요소가 있다면 true를 반환
   * ##### E next() : 다음에 있는 요소를 반환
```java

import java.util.ArrayList;
import java.util.Iterator;
import java.util.ListIterator;

public class IteratorListTest {

	public static void main(String[] args) {
		ArrayList<String> al = new ArrayList<String>();
		al.add("추꾸");
		al.add("논구");
		al.add("태껸");
		al.add("앞구르기");
		al.add("뒤구르기");
		System.out.println("Iterator를 이용한 출력");
		
		/*for(int i=0; i<5; i++) { 
			System.out.println(a1.get(i));
		}*/
		//결과는 for와 iterator는 같다. 그러나 이터레이터가 속도가 훨씬 빠르다.
		
		//Iterator는 전방향 출력만 가능하다.
		Iterator<String> lt = al.iterator();
		while (lt.hasNext()) {
			System.out.println(lt.next());
		}
		System.out.println("===============");
		System.out.println("ListIterator를 이용한 전방향 출력");
		
		
		//ListIterator는 전, 후 방향 모두 출력할 수 있다.
		ListIterator<String> lt2 = al.listIterator();
		while(lt2.hasNext()) {
			System.out.println(lt2.next());
		}
		
		System.out.println("================");
		System.out.println("ListIterator를 이용한 후방향 출력");
		while(lt2.hasPrevious()) {
			System.out.println(lt2.previous());
		}
	}
	
	/*
	 * Iterator를 이용한 출력
		추꾸
		논구
		태껸
		앞구르기
		뒤구르기
		===============
		ListIterator를 이용한 전방향 출력
		추꾸
		논구
		태껸
		앞구르기
		뒤구르기
		================
		ListIterator를 이용한 후방향 출력
		뒤구르기
		앞구르기
		태껸
		논구
		추꾸*/

}

```
