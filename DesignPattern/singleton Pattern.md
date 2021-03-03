### 싱글톤 패턴 singleton Pattern
* 단 하나만 존재하는 인스턴스 : 싱글톤
* 단 하나만 존재해야하는 객체를 만들 때 생성 : 날짜, 국가, 회사, 학교, 단체 등
* 전역변수를 사용하지 않고 객체를 하나만 생성하도록, 생성된 객체를 어디에서든지 참조할 수 있음. 
* private으로, static 으로, 유일한 객체 생성
* 외부에서의 사용은 싱글톤을 참조할 수 있는 static getInstance 메서드 구현, 모든 클라이언트에게 동일한 인스턴스를 반환하는 작업.  


***static과 싱글톤 패턴을 조합해, 고유번호 자동생성되는 카드 발급 프로그래밍***   

**싱글톤 패턴 (카드 발급 메서드 내포 클래스)**   
###### * 한 카드회사(KBCardCompany)가 있다고 하자. KBCardCompany 클래스를 이용해 카드회사에서 카드를 발급하려면 new KBCardCompany가   
###### 	 반드시 한번만 호출되어야한다. 
###### * 단계 1. KBCardCompany는 전 세계 유일한 딱 하나이기 때문에. 생성자를 외부에서 호출할 수 없게 해야한다. 
###### 	       KBCardCompany를 사칭할 수 없도록. KBCardCompany를 private으로 선언.
###### * 단계 2. 내부적으로 자기 자신을 가진 변수 instance를 만듦.
###### * 단계 2. KBCardCompany에 대한 인스턴스를 하나 만들어 외부에 제공해줄 메서드 필요 (static 변수, 메서드 활용해 get())
    
```java
public class KBCardCompany {

	private static KBCardCompany instance = new KBCardCompany(); // 단계 2. 내부생성자 생성
	
	private KBCardCompany() {} // 단계 1. 외부에서 쓸 수 없음 

	public static KBCardCompany getInstance() { // 단계 3. 외부에서 쓸 수 있게끔 get 생성, static으로 다른 클래스에서 사용가능.
		if(instance == null) {
		instance = new KBCardCompany();
		}
		return instance;
	}
	public Card createCard() {
		Card card = new Card();
		return card;
	}		
}
```   
**static을 이용한 고유번호 자동생성 클래스**   
```java
public class Card {
	
	private int cardNumber;
	private static int serialNum= 1000;
	
	Card(){
		serialNum++;
		setCardNumber(serialNum);
	}
	
	public int getCardNumber() {
		return cardNumber;
	}
	public void setCardNumber(int cardNumber) {
		this.cardNumber = cardNumber;
	}
}
```    
**메인 메소드**  
```java
public class KBCardCompanyTest {

	public static void main(String[] args) {
	   KBCardCompany kbCompany = KBCardCompany.getInstance(); //싱글톤패턴
		
	   Card myCard = kbCompany.createCard(); //메서드에서 card 생성
	   Card yourCard = kbCompany.createCard();
		
	   System.out.println(myCard.getCardNumber()); //1001출력
	   System.out.println(yourCard.getCardNumber()); //1002출력
	}
}
```
