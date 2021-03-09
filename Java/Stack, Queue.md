### Stack
###### 참고: [컬렉션 프레임워크](https://github.com/6161990/TIL/blob/main/Java/Collection%20Framework.md)

<img src="https://user-images.githubusercontent.com/74708028/110317392-7219d780-804f-11eb-9101-0e21ebc69fd3.jpg" width="400" height="200">


* #### Last In First Out(LIFO): 맨 마지막에 추가 된 요소가 가장 먼저 꺼내지는 자료구조
* #### 이미 구현된 클래스가 제공됨
* #### ArrayList나 LinkedList로 구현할 수 있음
* #### 게임에서 무르기, 최근 자료 가져오기 등에 구현
* #### 참고: stack 메서드 중 peek는  요소가 뭔지만 확인하는 메서드이고 꺼내오는 건 아님. 꺼내는 건 pop뿐!
```java
class MyStack {

	private ArrayList<String> arrayStack = new ArrayList<String>();
	
	public void push(String data) {
		arrayStack.add(data);
	}
	
	public String pop() {
		int len = arrayStack.size();
		if (len == 0) {
			System.out.println("스택이 비었습니다.");
			return null;
		}
		return arrayStack.remove(len-1);  //len-1 : 마지막에 넣은 게 먼저 꺼내져야하기때문에.
	}   
}

public class StackTest{
	
	public static void main(String[] args) {
		MyStack stack = new MyStack();
		stack.push("A");
		stack.push("B");
		stack.push("C");          //Last In
	                          	//First Oust
		System.out.println(stack.pop());    //C
		System.out.println(stack.pop());    //B
		System.out.println(stack.pop());    //A
		System.out.println(stack.pop());    //스택이 비었습니다. null
		
	}
}
```

### Queue
<img src="https://user-images.githubusercontent.com/74708028/110317566-aee5ce80-804f-11eb-8cd4-8e57a2654d87.jpg" width="400" height="350">

* #### First In First Out(FIFO): 먼저 저장된 자료가 먼저 꺼내지는 자료구조
* #### 가장 많이쓰이는 자료구조
* #### ArrayList나 LinkedList로 구현할 수 있음
* #### 선착순, 대기열 등을 구현할 때 가장 많이 사용되는 자료구조
* #### Queue도 위의 예에서와 마찬가지로 ArrayList로 enqueue로 add
  #### dequeue로 move
  #### 단! Queue는 First In First Out이기 때문에 인자를 (0)번째로. 
