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
public class Member {

	private int memberId;
	private String memberName;
	
	public Member() {}
	public Member(int memberId, String memberName) {
		this.memberId = memberId;
		this.memberName = memberName;
	}
	
	public int getMemberId() {
		return memberId;
	}
	public void setMemberId(int memberId) {
		this.memberId = memberId;
	}
	public String getMemberName() {
		return memberName;
	}
	public void setMemberName(String memberName) {
		this.memberName = memberName;
	}
	
	public String toString() {
		return memberName + "회원님의 아이디는 " + memberId + "입니다.";
	}	
}
```
```java

public class MemberHashMap {
	
	private HashMap<Integer, Member> hashMap;
	
	public MemberHashMap() {
		hashMap = new HashMap<Integer, Member>();
	}
	
	public void addMember(Member member) {
		hashMap.put(member.getMemberId(), member);      //집어넣을 때 put
	}
	
	public boolean removeMember(int memberId) {
		if ( hashMap.containsKey(memberId)) {          //containsKey 
			hashMap.remove(memberId);
			return true;
		}
		System.out.println("회원 번호가 없습니다");
		return false;
	}
	
	public void showAllMember() {
		
    //key와 value 동시에 순회할 순 없음
		Iterator<Integer> ir = hashMap.keySet().iterator();   //모든 key값을 중복되지않는 Set 타입을 반환 'keySet'
			int key = ir.next();                              //이외에 values 도 있음. 모든 values 값을 반환, 중복될 수 있어서 Collection으로반환
			Member member = hashMap.get(key);                 //꺼낼 때 get
			System.out.println(member);
		}

		System.out.println();
		
	}
}
```
```java
public class MemberHashMapTest {

	public static void main(String[] args) {

		MemberHashMap manager = new MemberHashMap();
		
		Member memberLee = new Member(100, "Lee");
		Member memberKim = new Member(200, "Kim");
		Member memberPark = new Member(300, "Park");
		Member memberPark2 = new Member(300, "Park");
				
		manager.addMember(memberLee);
		manager.addMember(memberKim);
		manager.addMember(memberPark);
		manager.addMember(memberPark2);   //출력안됨 Integer는 equals가 이미 구현되어있어서 id같아서 출력되지않음
				
		manager.showAllMember();
		
		manager.removeMember(200);
		manager.showAllMember();
    //Lee회원님의 아이디는 100입니다
		//Park회원님의 아이디는 300입니다.
    .
    
	}
}
```
----------------------------------------------------
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
#
```java
public class MemberTreeMap {
	
	private TreeMap<Integer, Member> treeMap;
	
	public MemberTreeMap() {
		treeMap = new TreeMap<Integer, Member>();
	}
	
	public void addMember(Member member) {
		treeMap.put(member.getMemberId(), member);
	}
	
	public boolean removeMember(int memberId) {
		if ( treeMap.containsKey(memberId)) {
			treeMap.remove(memberId);
			return true;
		}
		System.out.println("회원번호가 없습니다");
		return false;
	}
	
	public void showAllMember() {
		
		Iterator<Integer> ir = treeMap.keySet().iterator();
		while( ir.hasNext()) {
			int key = ir.next();
			Member member = treeMap.get(key);
			System.out.println(member);
		}

		System.out.println();
		
	}
	
}
```
