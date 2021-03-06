#
###### * 사전참고 :[인터페이스](https://github.com/6161990/TIL/blob/main/Java/Interface.md), [인터페이스의 요소](https://github.com/6161990/TIL/blob/main/Java/Interface%20Elements.md)
#

### 인터페이스 구현과 클래스 상속 함께 사용하기
```java
   public class Shelf {
      protected ArrayList<String> shelf;
	
	    public  Shelf() {
		    shelf = new ArrayList<String>();
	    }
	    public int getCount() {
		    return shelf.size();
	    }
}
```    
```java
   public interface Queue {

	    void enQueue(String title);
	    String deQueue();
	
	    int getSize();
}
```
```java
  public class BookShelf extends Shelf implements Queue{

  	@Override
  	public void enQueue(String title) {
	  	shelf.add(title);
	  }

	  @Override
	  public String deQueue() {
		  return shelf.remove(0);
	  }

	  @Override
	  public int getSize() {
		  return getCount();
	  }
```
```java
   public class BookShelfTest {

	  public static void main(String[] args) {
		  Queue bookQueue = new BookShelf();
		  bookQueue.enQueue("제인에어1");
		  bookQueue.enQueue("바벨로의 탑");
		  bookQueue.enQueue("내 휴식과 이완의 해");
		
		  System.out.println(bookQueue.deQueue());
		  System.out.println(bookQueue.deQueue());
		  System.out.println(bookQueue.deQueue());
	  }

}
```
