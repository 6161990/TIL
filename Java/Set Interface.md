## :pushpin: Set Interface
###### 참고: [컬렉션 프레임워크](https://github.com/6161990/TIL/blob/main/Java/Collection%20Framework.md)
### Collection의 개체를 순회하는 인터페이스
* #### iterator()메서드 호출 : Set은 순서가 없기 때문에 지정해서 꺼낼 수 없으므로 iterator를 이용한다.

        Iterator ir = memberArrayList.iterator();  
* #### Iterator에 선언된 메서드
   * ##### boolean hashNext() : 이후에 요소가 더 있는지를 체크하는 메서드이며, 요소가 있다면 true를 반환
   * ##### E next() : 다음에 있는 요소를 반환

<br>

#### :round_pushpin: Set 인터페이스 
* ##### Collection 하위의 인터페이스
* ##### 중복을 허용하지 않음
* ##### List는 순서기반의 인터페이스지만, Set은 순서가 없음
* ##### get(i)메서드가 제공되지 않음(Iterator로 순회)
* ##### 저장된 순서와 출력순서는 다를 수 있음
* ##### 아이디, 주민번호, 사번 등 유일한 값이나 객체를 관리할 때 사용
* ##### HashSet, TreeSet 클래스
  * ###### HashSet은 중복인지 아닌지 알기위해, equals와 hashCode.
  * ###### TreeSet은 정렬하기 위해서, Comparable와 Comparator.


<br>


#### :round_pushpin: HashSet
##### Set 인터페이스를 구현한 클래스
##### 중복을 허용하지 않으므로 저장되는 객체의 동일함 여부를 알기위해
##### equals()와 hashCode()메서드를 재정의 해야함.

```java
public class HashSetTest {

	public static void main(String[] args) {

		HashSet<String> set = new HashSet<String>();
		set.add("이순신");
		set.add("김유신");
		set.add("강감찬");
		set.add("이순신");                 //중복
		
                System.out.println(set);           //[김유신, 강감찬, 이순신] 순서대로 나오지 않음, 중복허용하지않음
                
                
                //하나씩 꺼내는 순회방법
		Iterator<String> ir = set.iterator();  //String으로 iterator를 순회한다고 했기 때문에
		
		while(ir.hasNext()) {                   //hasNext          
                        String str = ir.next();        //반환값도 String, next
			System.out.println(str);
		}	
	}
}
```

### :computer: 프로그래밍해보기
#### HashSet으로 멤버 순회하면서 중복체크해보기
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
	
        
        //id 재정의를 위한 equals, hashCode
	@Override
	public int hashCode() {
		return memberId;
	}
	@Override
	public boolean equals(Object obj) {
		
		if (obj instanceof Member) {
			Member member = (Member)obj;
			return (this.memberId == member.memberId); 
		}
		
		return false;
	}	
}
```
```java
public class MemberHashSet {
	
	private HashSet<Member> hashSet;
	
	public MemberHashSet() {
		hashSet = new HashSet<Member>();
	}

	public void addMember(Member member) {
		hashSet.add(member);
	}
	
	public boolean removeMember(int memberId) {
		
		Iterator<Member> ir = hashSet.iterator();
		while( ir.hasNext()) {
			Member member = ir.next();
			if( member.getMemberId() == memberId) {
				hashSet.remove(member);
				return true;
			}
		}
		
		System.out.println(memberId + "번호가 존재하지 않습니다.");
		return false;
	}
	
	public void showAllMember() {
		for(Member member : hashSet) {
			System.out.println(member);
		}
		System.out.println();
	}
	
}
```
```java
public class MemberHashSetTest {

	public static void main(String[] args) {

		MemberHashSet manager = new MemberHashSet();
		
		Member memberLee = new Member(100, "Lee");
		Member memberKim = new Member(200, "Kim");
		Member memberPark = new Member(300, "Park");
		
		manager.addMember(memberLee);
		manager.addMember(memberKim);
		manager.addMember(memberPark);
                manager.showAllMember();   
                //Park회원님의 아이디는 300입니다.
                //Lee회원님의 아이디는 100입니다.
                //Kim회원님의 아이디는 200입니다.
                
                manager.removeMember(100);
                manager.showAllMember();   
                //Park회원님의 아이디는 300입니다.
                //Kim회원님의 아이디는 200입니다.
                
                Member memberPark2 = new Member(300, "Park2");     //id는 유일한 값인데 아이디 300에 Park2가 들어가버림
		manager.addMember(memberPark2);                    //id가 같으면 같은 멤버라는 것이 논리적으로 구현되어있지 않기때문
		                                                   //equals 재정의해줘야함 (At Member)
                                                                   //그러면 Park2가 중복으로 출력되지않음
		manager.showAllMember();
                //Park회원님의 아이디는 300입니다.
                //Kim회원님의 아이디는 200입니다.
                //Park2회원님의 아이디는 300입니다.
             
	}
}
```
-----------------------------------------------

<br>

--------------------------------------------------------------------------

#### :round_pushpin: TreeSet
##### 객체의 정렬(Tree)에 사용되는 클래스
* ##### 중복을 허용하지 않으면서 오름차순이나 내림차순으로 객체를 정렬함
* ##### 내부적으로 이진 검색 트리(binary search tree)로 구현되어있음
* ##### 이진 검색 트리에 자료가 저장될 때 비교하여 저장될 위치를 정함
* ##### 객체 비교를 위해 Comparable이나 Comparator 인터페이스를 구현해야함

<br>

#### :round_pushpin: Comparable 인터페이스와 Comparator 인터페이스
* ##### 정렬 대상이 되는 클래스가 구현해야하는 인터페이스
* ##### Comparable은 compareTo()메서드를 구현, 매개변수와 객체 자신(this)을 비교
* ##### Comparator는 compare() 메서드를 구현, 두 개의 매개 변수를 비교
  ##### Comparator의 경우 디폴트 컨스트럭트에 정렬할 대상을 반드시 명시 해줘야함
  ##### TreeSet 생성자에 Comparator가 구현된 객체를 매개변수로 전달   
            TreeSet<Member> treeSet = new TreeSet<Member>(new Member( ));
  ##### 일반적으로 Comparable을 더 많이 사용
* ##### 이미 Comparable이 구현된 경우 Comparator를 이용하여 다른 정렬 방식을 정의할 수 있음

<br>

### :computer: 프로그래밍해보기
#### :round_pushpin: TreeSet으로 멤버 정렬해보기
```java
public class Member implements Comparator<Member>{    //Comparable 인터페이스에는 밑에 /*compareTo*/

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
	
	@Override
	public int hashCode() {
		return memberId;
	}
	@Override
	public boolean equals(Object obj) {
		
		if (obj instanceof Member) {
			Member member = (Member)obj;
			return (this.memberId == member.memberId); 
		}
		
		return false;
	}
	
	/*@Override
	public int compareTo(Member member) {
		
		return this.memberName.compareTo(member.getMemberName()); //멤버 이름으로 정렬 
                                                                        //String안에 이미 comparable이 정의되어있기 때문에 -로 구현필요없음
	}*/
	
	@Override
	public int compare(Member member1, Member member2) {  //첫번째가 this, 두번째가 넘어온 매개변수(비교대상)

		return (member1.memberId - member2.memberId);           //멤버 아이디로 정렬
	}	
}
```
```java
public class MemberTreeSet {
	
	private TreeSet<Member> treeSet;
	
	public MemberTreeSet() {
		treeSet = new TreeSet<Member>(new Member());  //Comparator의 경우 디폴트 컨스트럭트에 정렬할 대상을 반드시 명시 해줘야함
	}

	public void addMember(Member member) {
		treeSet.add(member);
	}
	
	public boolean removeMember(int memberId) {
		
		Iterator<Member> ir = treeSet.iterator();
		while( ir.hasNext()) {
			Member member = ir.next();
			if( member.getMemberId() == memberId) {
				treeSet.remove(member);
				return true;
			}
		}
		
		System.out.println(memberId + "번호가 존재하지 않습니다.");
		return false;
	}
	
	public void showAllMember() {
		for(Member member : treeSet) {
			System.out.println(member);
		}
		System.out.println();
	}
	
}
```
```java
public class MemberTreeSetTest {

	public static void main(String[] args) {

		MemberTreeSet manager = new MemberTreeSet();
		
		Member memberLee = new Member(300, "Lee");
		Member memberKim = new Member(100, "Kim");
		Member memberPark = new Member(200, "Park");
	
		
		manager.addMember(memberLee);
		manager.addMember(memberKim);
		manager.addMember(memberPark);
	
		manager.showAllMember();
                //comparator, id로 정렬했기 때문에
                //Kim회원님의 아이디는 100입니다.
                //Park회원님의 아이디는 200입니다.
                //Lee회원님의 아이디는 300입니다.
	}
}
```

<br>

#### :triangular_flag_on_post: 이미 Comparable이 구현된 경우, Comparator를 이용하여 다른 정렬 방식을 정의해보기
##### 원래 구현은 오름차순이었지만 여기서는 내림차순으로 구현하고 싶을 때,  Comparator로 다시 정의
```java
class MyCompare implements Comparator<String>{

	@Override
	public int compare(String s1, String s2) {

		return s1.compareTo(s2) *(-1); //-1 은 역순 = 내림차순
	}
}

public class ComparatorTest {

	public static void main(String[] args) {
		TreeSet<String> treeSet = new TreeSet<String>(new MyCompare()); 
                 //원래 String의 compare방식이 아니라 new MyCompare방식으로 정렬됨 
                 
		treeSet.add("제니");                                 
		treeSet.add("리사");
		treeSet.add("로제");
		
		for( String str : treeSet) {
			System.out.println(str);
		}
	}
}

```

