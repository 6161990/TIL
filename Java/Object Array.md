###  :pushpin: 객체배열 Object Array
* #### Book[] library = new Book[5];
* #### 배열에서도 마찬가지로 참조 자료형은 생성자를 만들어사용해야한다.
* #### 객체 배열에서는 장차 데이터가 생성이 되서 그 데이터가 자리해있을 주소값을 뱉어냄. (기본 자료형 배열과는 다름)

<br>

#### :round_pushpin:  객체배열 클래스
```java
public class Book {
	
	private String title;
	private String author;
	
	public Book() {}
	
	public Book(String title, String author) {
		this.setTitle(title);
		this.setAuthor(author);
	}

	public String getAuthor() {
		return author;
	}

	public void setAuthor(String author) {
		this.author = author;
	}

	public String getTitle() {
		return title;
	}

	public void setTitle(String title) {
		this.title = title;
	}
	public void showBookInfo() {
		System.out.println(title+","+author);
	}

}
```  
   <br>
   
#### :round_pushpin: 객체배열에서의 주의점(메인 메소드)
```java
public class BookArrayTest {

	public static void main(String[] args) {
		
		Book[] library = new Book[5]; 
    	}
}
``` 
##### (((( 주의 )))) 해당 메소드 구문은
##### 다섯개를 담을 수 있는 그릇만 생성된 것. 
##### 다섯개 데이터는 생성자로 생성해야 생성되는 것. 
##### 그래서 

 		for(int i=0; i<library.length; i++){
		    System.out.println(library[i]);
		  }

##### 하면 null만 다섯번 출력. 
		
   <br>
   
#### :round_pushpin: 객체배열에서의 데이터 생성 (메인 메소드)
```java
public class BookArrayTest {

	public static void main(String[] args) {
		
		Book[] library = new Book[5]; 
		library[0] = new Book("생활코딩","이고잉"); 
		library[1] = new Book("자바의 정석","남궁성");
		library[2] = new Book("그 후 ","나쓰메소세키");
		library[3] = new Book("스토너","존 윌리엄스");
		library[4] = new Book("끈이론","데이비드 포스터 윌리스");
		
		for(int i=0; i<library.length; i++){
			System.out.println(library[i]); //주소값이 출력됨. 
			library[i].showBookInfo(); //정보가 출력됨. 
			}
	}
}
```    

   <br>
   
#### :round_pushpin: 향상된 for문 (enhanced for)
* ##### 배열요소의 처음부터 끝까지 모든 요소를 참조할 때 편리한 반복문
* ##### 반복문이 처리해야 할 데이터를 배열이라는 그릇에 담아서 반복문에 제공하면 반복문은 그 그릇에 담긴 값을 하나하나 꺼내면서 어떠한 처리를 해줌. 
```java
public class enhancedFor{
	
	public static void main(String[] args) {
		Book[] library = new Book[5]; 
		Book[] copyLibrary = new Book[5];
		
		library[0] = new Book("생활코딩","이고잉");
		library[1] = new Book("자바의 정석","남궁성");
		library[2] = new Book("그 후 ","나쓰메소세키");
		library[3] = new Book("스토너","존 윌리엄스");
		library[4] = new Book("끈이론","데이비드 포스터 윌리스");
		
		System.arraycopy(library, 0, copyLibrary, 0,5);
		
		for(Book book : copyLibrary) {  //타입(Book)과 타입(book)에 대한 변수, 거기에 복사한 배열 넣기 
			book.showBookInfo();
		}
	}
}
```    

   <br> 
   
#### 📍 객체 배열 복사 (얕은 복사)
* #####  얕은 복사 : 인스턴스의 주소만 복사하는 것. 인스턴트가 구별된 것은 아님. 
* #####  그래서 얕은 복사 후 , 원본에서 데이터를 수정하면 카피본에서도 똑같이 수정이 됨. 
```java
public class ArrayCopy {

	public static void main(String[] args) {
		int[] arr1 = {10,20,30,40,50};
		int[] arr2 = {1,2,3,4,5};
		
		System.arraycopy(arr1, 0, arr2, 1,3);
                 //(뭐를, 어디서부터, 어디로, 어디부터, 어디까지)
                 //(-----arr1-----), (----------arr2----------)
		
		for(int i =0; i<arr2.length; i++) {
			System.out.println(arr2[i]);
		}
	}
}
```    

   <br>
   
#### :round_pushpin: 객체 배열 복사 (깊은 복사)
* #####  깊은 복사 : 인스턴트가 구별되는 복사. 
* #####  그래서 깊은 복사 후 , 원본에서 데이터를 수정하면 카피본에서는 영향 없음. 서로가 서로에게 영향을 끼치지 않음. 
* ##### 깊은 복사를 할 수 있는 방법 네 가지
  ##### 1. for문
  ##### 2. System.arraycopy(arr1, 0, arr2, 0, arr1.length);
  ##### 3. arr2 = Arrays.copyOf(arr1, arr1.length);
  ##### 4. arr2 = arr1.clone();
```java
public class ArrayCopy {

	public static void main(String[] args) {
		int[] arr1 = {10,20,30,40,50};
		int[] arr2 = {1,2,3,4,5};
		
		System.arraycopy(arr1, 0, arr2, 1,3);
                 //(뭐를, 어디서부터, 어디로, 어디부터, 어디까지)
                 //(-----arr1-----), (----------arr2----------)
		
		for(int i =0; i<arr2.length; i++) {
			System.out.println(arr2[i]);
		}
	}
}
```    
```java
public class Copy {
	
	public static void main(String[] args) {
		Book[] library = new Book[5]; 
		Book[] copyLibrary = new Book[5];
		
		library[0] = new Book("생활코딩","이고잉");
		library[1] = new Book("자바의 정석","남궁성");
		library[2] = new Book("그 후 ","나쓰메소세키");
		library[3] = new Book("스토너","존 윌리엄스");
		library[4] = new Book("끈이론","데이비드 포스터 윌리스");
		
		copyLibrary[0] = new Book();
		copyLibrary[1] = new Book();
		copyLibrary[2] = new Book();
		copyLibrary[3] = new Book();
		copyLibrary[4] = new Book();
		
		for(int i =0; i<library.length; i++) {                    //깊은 복사
			copyLibrary[i].setTitle(library[i].getTitle());
			copyLibrary[i].setAuthor(library[i].getAuthor());
		}
		
		library[0].setAuthor("김상욱");                           //library 데이터 수정
		library[0].setTitle("김상욱의 양자공부");
    
		
		for(Book book : library) {                                
			book.showBookInfo();
		}
		
		System.out.println("=========================");          //library 데이터 수정 후, library만 수정되고 copyLibrary는 데이터 그대로 유지. 
		
		for(Book book : copyLibrary) {  
			book.showBookInfo();
		}
	}
}
```   
















