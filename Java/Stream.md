### 스트림 Stream
#### 자료의 대상과 관계없이 동일한 연산을 수행할 수 있는 기능(자료의 추상화)
#### 자바 io에서 말하는 스트림과 다름. 여기는 연산, 거기는 입출력을 위한 스트림
* #### 배열, 컬렉션에 동일한 연산이 수행되어 일관성있는 처리가능.
* #### 배열, 컬렉션에서 스트림을 쓰려면 생성해야한다. 이 때 생성된 스트림은 원래의 배열을 건드리지 않고 다른 메모리에 생성된다.
* #### 한번 생성하고 사용한 스트림은 재사용할 수 없음
* #### 스트림 연산은 기존 자료를 변경하지않음
* #### 중간 연산과 최종 연산으로 구분됨
  * #### 중간 연산 : 어떤 조건으로 그 자료를 필터링 하거나, 조건에 맞는 자료를 꺼내오는 경우
  * #### 최종 연산 : 그(중간연산에대한) 합을 구한다거나 평균을 구한다거나
* #### 최종 연산이 수행되어야 모든 연산이 적용되는 **지연 연산**
#
**배열로 스트림 생성하기**
##### ***Arrays.stream*** 하면 Array활용해서 stream 객체를 만드는 함수가 static으로 많이 있음
 ```java
 public class IntArrayTest {

	public static void main(String[] args) {

		int[] arr = {1,2,3,4,5};
		
		int sum = Arrays.stream(arr).sum();   
		int count = (int)Arrays.stream(arr).count(); //재활용이 안되기 때문에 필요시마다 Arrays.stream(arr)스트림 생성
		
		System.out.println(sum);
		System.out.println(count);
		
		System.out.println(Arrays.stream(arr).reduce(0, (a,b)->a+b));   //reduce
		
	}
}
 ```
 **컬렉션으로 스트림 생성하기**
 ```java
 public class ArrayListStreamTest {

	public static void main(String[] args) {

		List<String> sList = new ArrayList<String>();
		sList.add("Tomas");
		sList.add("Edward");
		sList.add("Jack");
		
		
		//배열과는 다르게 stream 메서드를 바로 사용할 수 있음. 배열에서는 Arrays.stream(arr)으로 안에다 배열의 종류(arr)를 넣어주었음
		Stream<String> stream = sList.stream();  
		stream.forEach(s->System.out.print(s + " "));  //'Tomas Edward Jack'
		System.out.println();
		
		//sorted(). -> 중간 연산에서 사용(정렬. String은 comparable이 구현되어있어서 sort이용가능. 다른 곳에서는 구현필요)
		sList.stream().sorted().forEach(s->System.out.print(s + " ")); //'Edward Jack Tomas'
		
		
		System.out.println();
		
		//map -> 중간 연산에서 이름꺼내올 때 사용
		sList.stream().map(s->s.length()).forEach(n->System.out.println(n)); // '5' '6' '4'
		
	}
}
 ```
**중간 연산**
###### filter(), map()
###### 조건에 맞는 요소를 추출(filter()) 하거나 요소를 변환함(map())
###### 스트림에서의 구현부는 람다식으로
###### 문자열의 길이가 5이상인 요소만 출력하기
          
          추출 filter
          sList.stream(). filter(s-> s.length() >= 5). forEach(s -> System.out.println(s));
          --스트림생성--   ---------중간연산----------   --------------최종연산--------------
###### 고객 클래서에서 고객 이름만 가져오기

          변환 map
          customerList.stream(). map(c-> c.getName( )). forEach(S -> System.out.println(s));
          ------스트림생성----- -------중간연산--------  --------------최종연산--------------
#
**최종 연산**
###### 스트림의 자료를 소모하면서 연산을 수행
###### 최종 연산 후에 스트림은 더이상 다른 연산을 적용할 수 없음. 만든 스트림을 어떤 변수에 넣어 재활용할 수 없음
* ###### forEach() : 요소를 하나씩 꺼내옴
* ###### count() : 요소의 개수
* ###### sum() : 요소의 합
###### 이 외에도 여러가지 최종연산이 있음
#
**reduce() 연산**
* ###### 정의된 연산이 아닌 프로그래머가 직접 지정하는 연산을 적용
* ###### 최종 연산으로 스트림의 요소를 소모하며 연산 수행
* ###### 배열의 모든 요소의 합을 구하는 reduce() 연산
* ###### 두 번째 요소로 전달되는 람다식에 따라 다양한 기능을 수행

          Array.stream(arr).reduce(초기값, (전달되는 요소) -> (각 요소가 수행해야 할 기능)); 
          Array.stream(arr).reduce(0, (a,b) -> (a+b));
#### reduce()이용해 길이 제일 긴 단어 고르기
**reduce 연산 사용법 1**
```java
public class ReduceTest{

public static void main(String[] args) {
	String[] greetings = {"안녕하세요~~~~~", "hello", "Good moring", "반갑습니다"};
	
	System.out.println(Arrays.stream(greetings).reduce("", (s1, s2)->
		{if (s1.getBytes().length >= s2.geyBytes().length) //람다식
			return s1;
		 else return s2;
	
		}));
	}
}

```
**reduce 연산 사용법 2**
```java
class CompareString implements BinaryOperator<String>{

	//강제구현 메소드
	@Override
	public String apply(String s1, String s2) {  
		if(s1.getBytes().length >= s2.getBytes().length) //람다식
			return s1;
		else return s2;
	}
}

public class ReduceTestVerTwo{

public static void main(String[] args) {
	String[] greetings = {"안녕하세요~~~~~", "hello", "Good moring", "반갑습니다"};
	
	//reduce(BinaryOperator가 구현된 클래스를 get으로 받는다.)
	System.out.println(Arrays.stream(greetings).reduce(new CompareString()).get());
```
          

                                 
          
          
