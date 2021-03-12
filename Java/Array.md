### :pushpin: Array 배열
* ##### 여러 개의 data를 하나의 변수에 담기 위해 연관된 정보를 그룹화하는데 사용. 배열 또한 data type.
* ##### int[] arr = new int[10]; 에서 [10]는 배열의 그릇, 10개만큼 방이 생긴다는 의미 = 배열의 길이 length
* ##### 배열의 길이 length는 말 그대로 그만큼만 담을 수 있다. 데이터를 수용할 수 있는 최대 개수가 [n] 만큼이다.
* ##### 배열은 순차적이라 [2]자리에 있는 data를 빼면, [3]자리에 있던 데이터가 [2]자리로 옮김. 
* ##### arr[1]=0; 에서 '[1]'은 배열의 주소, index / '0'은 [1] 에 담긴 값, 원소.    
  
     <br>
#### :round_pushpin:  Array 선언
#### array 선언하는 3가지 방법
```java
public class ArrayTest {

	public static void main(String[] args) {
		// 1  배열 데이터 분할해서 정의하기
		String[] classgroup = new String[2]; // 만들려고 하는 문자열 원소로 이루어진 새로운 배열은 2개의 원소로 구성된다. 
			classgroup[0]="김우빈";
			classgroup[1]="신민아";
			
		// 2  배열 한꺼번에 정의하기
		String[] classgroup2 = {"김우빈","신민아"};
		
		// 1,2의 결합해 정의하기
		String[] classgroup3 = new String[] {"김우빈","신민아"};
			
	}
}
```

   
#### array 선언, 사용해보기 (1~10까지 출력)  

```java
public class ArrayTest {

	public static void main(String[] args) {
		  int[] arr = new int[10];
		
		  for(int i=0, num=1; i< arr.length; i++, num++) {  
			  arr[i]=num;     // num 은 원소값을 알려주기 위함. num이 없으면 매번 0 출력. i가 init되기 때문. 
			  System.out.println(arr[i]);
		  }
}
```
#### array 선언, 사용해보기 (1~10까지 모두 더해 출력)

```java
public class ArrayTest {

	public static void main(String[] args) {
		  int[] arr = new int[10];
		  int total = 0;
		
		  for(int i=0, num=1; i<arr.length; i++, num++) {
		  	arr[i]=num;
		  }
		  for(int i=0; i<arr.length; i++) {
		  	total += arr[i];
		  }
		  System.out.println(total);
  }

}
```    
   <br> 
   
#### :round_pushpin:  arr.length 사용시, 유효한 값의 범위 주의
#####  arr.length[5]인데, [0]~[2]까지만 초기화를 하면 나머지 [4],[5] 는 0 임.    
#####  그래서 arr.length[5]을 기준으로 for문(곱하기)을 돌리면 값이 0. ([4],[5]가 0 이기 때문에 다른 값과 곱하면 0)
#####  i<arr.length[5] 로 하는 게 아니라 변수('count')를 하나 두고, 인덱스가 초기화 될때마다 ++ 하는 카운팅 필요. 
```java
public class ArrayTest {

	public static void main(String[] args) {
		  double[] dArr = new double[5];
		  int count =0 ;    // 카운팅 변수 선언 
		  dArr[0] = 1.1; count++; //카운팅
		  dArr[1] = 2.1; count++; //카운팅
		  dArr[2] = 3.1; count++; //카운팅
		
		  double mtotal = 1;
		  for(int i=0; i<count; i++) { //카운팅 변수까지만 곱하기 진행.  
		  	mtotal *=dArr[i];
		  }
      
		  System.out.println(mtotal);
	}
```   
   <br>
   
#### array로 알파벳 출력해보기   

```java
public class ArrayTest {

	public static void main(String[] args) {
		char[] alphabets = new char[26];
		char ch = 'A';  //문자는 정수로 표현 ch는 65, 
		
		for(int i=0; i<alphabets.length; i++) {
			alphabets[i] = ch++; //++이 뒤에 붙어있기 때문에 수행하고 나서 더해지게됨. 
		}
		
		for(int i=0; i<alphabets.length; i++) {
			System.out.println(alphabets[i]+ ","+(int)alphabets[i]);
		}
	}
}
```   
   <br>
   
#### :round_pushpin: 다차원배열
* ##### 2차원 이상의 배열. 지도, 게임 등의 공간을 구현할 때 사용
* ##### int[][] arr = new int[][];
* ##### 사용시, 행을 기준으로 열을 돌리면 된다. 

```java
public class MultiArray {

	public static void main(String[] args) {
		String[][] arr = {{"101호","102호","103호"},{"104호","105호","106호"}};
		for(int i=0; i<arr.length;i++) {
			for(int j=0; j<arr[i].length; j++) {
				System.out.print(arr[i][j]+" ");
			}
			System.out.println();
		}
	}

}
```   


