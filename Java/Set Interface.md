### Set Interface
* #### Collection의 개체를 순회하는 인터페이스
* #### iterator()메서드 호출 : Set은 순서가 없기 때문에 지정해서 꺼낼 수 없으므로 iterator를 이용한다.

        Iterator ir = memberArrayList.iterator();  
* #### Iterator에 선언된 메서드
* ###### boolean hashNext() : 이후에 요소가 더 있는지를 체크하는 메서드이며, 요소가 있다면 true를 반환
* ###### E next() : 다음에 있는 요소를 반환
#
#### Set 인터페이스 
* ###### Collection 하위의 인터페이스
* ###### 중복을 허용하지 않음
* ###### List는 순서기반의 인터페이스지만, Set은 순서가 없음
* ###### get(i)메서드가 제공되지 않음(Iterator로 순회)
* ###### 저장된 순서와 출력순서는 다를 수 있음
* ###### 아이디, 주민번호, 사번 등 유일한 값이나 객체를 관리할 때 사용
* ###### HashSet, TreeSet 클래스
  ###### HashSet은 중복인지 아닌지 알기위해, equals와 hashCode.
  ###### TreeSet은 정렬하기 위해서, Comparable와 Comparator.
--------------------------------

**HashSet**
###### Set 인터페이스를 구현한 클래스
###### 중복을 허용하지 않으므로 저장되는 객체의 동일함 여부를 알기위해
###### equals()와 hashCode()메서드를 재정의 해야함.
```java
```
#

**TreeSet**
##### 객체의 정렬에 사용되는 클래스
* ###### 중복을 허용하지 않으면서 오름차순이나 내림차순으로 객체를 정렬함
* ###### 내부적으로 이진 검색 트리(binary search tree)로 구현되어있음
* ###### 이진 검색 트리에 자료가 저장될 때 비교하여 저장될 위치를 정함
* ###### 객체 비교를 위해 Comparable이나 Comparator 인터페이스를 구현해야함
#
**Comparable 인터페이스와 Comparator 인터페이스**
* ###### 정렬 대상이 되는 클래스가 구현해야하는 인터페이스
* ###### Comparable은 compareTo()메서드를 구현, 매개변수와 객체 자신(this)을 비교
* ###### Comparator는 compare() 메서드를 구현, 두 개의 매개 변수를 비교
  ###### TreeSet 생성자에 Comparator가 구현된 객체를 매개변수로 전달   
            TreeSet<Member> treeSet = new TreeSet<Member>(new Member( ));
  ###### 일반적으로 Comparable을 더 많이 사용
* ###### 이미 Comparable이 구현된 경우 Comparator를 이용하여 다른 정렬 방식을 정의할 수 있음
```java
```

