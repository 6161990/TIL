### :pushpin: Map 인터페이스
###### 참고: [컬렉션 프레임워크](https://github.com/6161990/TIL/blob/main/Java/Collection%20Framework.md)
* ##### key-value pair 의 객체를 관리하는데 필요한 메서드가 정의됨
* ##### key는 중복될 수 없음, 중복되는 경우 기존에 있는 키에 해당하는 값을 덮어씀
* ##### 구현 클래스는 HashMap, HashTable, LinkedHashMap, Properties, TreeMap등이 있다.
* ##### 검색을 위한 자료구조
* ##### key를 이용하여 값을 저장하거나 검색, 삭제할 때 사용하면 편리함
  ##### 내부적으로 hash방식으로 구현됨   
      index = hash(key) //index는 저장위치
* ##### key가 되는 객체는 객체의 유일성함의 여부를 알기 위해 equals()와 hashCode()메서드를 재정의함

<br>

#### :round_pushpin: HashMap 클래스
* ##### Map 인터페이스를 구현한 클래스 중 가장 일반적으로 사용하는 클래스
* #####  HashTable 클래스는 자바2부터 제공된 클래스로 HashMap과 동일하지만, Vector처럼 동기화를 제공함
  ##### 복수의 쓰레드가 동시에 HashTable에 접근해서 객체를 추가, 삭제 하더라도 쓰레드에 안전하다.
* ##### pair 자료를 쉽고 빠르게 관리할 수 있음
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
---------------------------------------------------------


#### :round_pushpin: TreeMap 클래스
 ##### key객체를 정렬하여 key- value를 pair로 관리하는 클래스
 * ##### 검색 기능을 강화시킨 컬렉션으로 계층 구조를 활용하여 이진트리 자료 구조를 구현하여 제공한다.
 * ##### 키와 값이 저장된 Map.Entry를 저장하고, 왼쪽과 오른쪽 자식 노드를 참조하기 위한 두 개의 변수로 구성되어 있다. 
 * ##### key에 사용되는 클래스에 Comparable, Comparator 인터페이스를 구현
 * ##### java에 많은 클래스들은 이미 Comparable이 구현되어있음
 * ##### 구현된 클래스를 key로 사용하는 경우는 구현할 필요없음  

          public final class Integer extends Number implements Comparable<integer>{
            ...
            public int compareTo(Integer anotherInteger){
                return compare(this.value, anotherInteger.value);
            } 
          }

<br>

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

<br>

#### :round_pushpin: Properties
* ##### 키와 값을 String 타입으로 제한한 Map 컬렉션
* ##### 주로 Properties는 프로퍼티 (*.properties) 파일을 읽어들일 때 주로 사용된다.
##### :triangular_flag_on_post: *.properties?
   * ##### 옵션정보, 데이터베이스 연결정보, 국제화(다국어)정보를 기록하여 텍스트 파일로 활용한다.
   * ##### 애플리케이션에서 주로 변경이 잦은 문자열을 저장하여 관리하기 때문에 유지보수를 편리하게 만들어준다. 
   * ##### 키와 값이 '='기호로 연결되어 있는 텍스트 파일이며, ISO 8859-1 문자셋으로 저장되고, 한글은 유니코드(Unicode)로 변환되어 저장된다. 
```java
public class TestProperties{
	public static void main(String[] args){
	    Proterties prop = new Properties();
	    prop.setProperty ("driver","oracle.jdbc.driver.OracleDriver");
	    prop.setProperty ("url","jdbc:oracle:thin:@127.0.0.1:1521:xe");
	    prop.setProperty ("user","user007");
	    prop.setProperty ("password","pass0070");
	    
	    System.out.println(prop.gerProperty("driver"));
	    System.out.println(prop.gerProperty("url"));
	    System.out.println(prop.gerProperty("user"));
	    System.out.println(prop.gerProperty("password"));
	    
	    
	    //파일에 기록저장 : properties에 저장된 정보를 파일에 저장 : store 메서드이용
	    try{
	    	prop.store(new FileWriter("setting.txt"),"jdbc.oracle.setting");
		prop.storeToXML(new FileOutputStream("setting.xml"),"jdbc.oracle.setting","utf-8");
	    }catch(IOException e){
	    	e.printStackTrace
		
	    //파일로부터 데이터 읽어보기 : load 메서드 
	    Proterties prop1 = new Properties();
	    Proterties prop2 = new Properties();
		
	    try{
	    	prop1.load(new FileReader("setting.txt"));
		prop2.loadFromXML(new FileItputStream("setting.xml"));
		
		prop1.list(System.out);
		prop2.list(System.out);
	    }catch(IOException e){
	    	e.printStackTrace
	    }
	}
}
```
