### Map 인터페이스
* #### key-value pair 의 객체를 관리하는데 필요한 메서드가 정의됨
* #### key는 중복될 수 없음
* #### 검색을 위한 자료구조
* #### key를 이용하여 값을 저장하거나 검색, 삭제할 때 사용하면 편리함
  #### 내부적으로 hash방식으로 구현됨   
      index = hash(key) //index는 저장위치
* key가 되는 객체는 객체의 유일성함의 여부를 알기 위해 equals()와 hashCode()메서드를 재정의함
----------------------
**HashMap 클래스**
* ###### Map 인터페이스를 구현한 클래스 중 가장 일반적으로 사용하는 클래스
* ###### HashTable 클래스는 자바2부터 제공된 클래스로 Vector처럼 동기화를 제공함
* ###### pair 자료를 쉽고 빠르게 관리할 수 있음
```java
```

#
**TreeMap 클래스**
* ###### key객체를 정렬하여 key- value를 pair로 관리하는 클래스
* ###### key에 사용되는 클래스에 Comparable, Comparator 인터페이스를 구현
* ###### java에 많은 클래스들은 이미 Comparable이 구현되어있음
* ###### 구현된 클래스를 key로 사용하는 경우는 구현할 필요없음  

          public final class Integer extends Number implements Comparable<integer>{
            ...
            public int compareTo(Integer anotherInteger){
                return compare(this.value, anotherInteger.value);
            } 
          }
```java
```
