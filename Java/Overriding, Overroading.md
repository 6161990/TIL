### (method) Overriding 오버라이딩
* ###### 재정의, 새롭게 정의한다. => super의 기능을 변경핟다. 
* ###### 부모클래스도 가지고있고, 자식 클래스도 가지고 있는 메소드를 자식 클래스에서 재정의하게되면, 
  ###### 부모클래스에서 정의한 메소드는 무시가 되고, 자식 클래스에서 정의한 메소드가 호출된다. 
* ###### 상속과 오버라이딩
      상속은, 메소드의 동작 방식을 기본적으로 공유한다. 공통분모를 정의한다.
      오버라이딩은, 부모클래스에 있는 메소드를 그대로 상속받지 않고 하위 클래스에서 그 메소드를 재정의해 구현한다. 
      =>기본값은 넓게 적용시키고 예외적으로 사용하는 변칙이 필요한 부분은 더 높은 우선순위를 배정하는 접근방법.
              
    #  

**Overriding 오버라이딩의 조건**
* ###### 메소드의 서명(return 데이터 타입, 메소드 이름, 매개변수의 데이터 타입)이 부모의 것과 자식의 것이 일치해야함.
* 자식 메소드에서 오버라이딩할 때는 
    return super.method();
            하위메소드가 추가하고 싶은 기능이 있다면 밑에 이부분에 로직을 넣으면 된다. 
            
-------------------------
### Overroading 오버로딩
* ###### 클래스에 메소드를 정의할 때, 같은 이름이지만 다른 매개변수의 형식을 가진 여러 메소드를 정의할 수 있는 방법. 
  ###### => 같은이름 다른 메소드
```java    
    public void setOperands(int left, int right){     //매개변수 2개 메소드 
      System.out.println("setOperands(int left, int right)");
      this.left = left;
      this.right = right;
    }
    
    public void setOperands(int left, int right, int third){    //매개변수 3개 메소드 
      System.out.println("setOperands(int left, int right, int third)");
      this.left = left;
      this.right = right;
      this.third = third;
    }
    
    public static void main(String[] args) {
     Calculator c1 = new Calculator();   // 매개변수 2개 
      c1.setOprands(10,20);
      c1.sum();
    
      Calculator c2 = new Calculator();   // 매개변수 3개 
     c1.setOprands(10,20,30);
     c1.sum();
    }
 ```   
 #
###### **But, 중복이 존재**
       this.left = left;
       this.right = right;
```java    
    public void setOperands(int left, int right){     
      System.out.println("setOperands(int left, int right)");
      this.left = left;
      this.right = right;
    }
    
    public void setOperands(int left, int right, int third){    
      System.out.println("setOperands(int left, int right, int third)");
      **this.setOperands(left, right);**    //중복 제거. 
      this.third = third;
    }      
``` 
#
**Overroading 오버로딩의 조건(오버라이딩과의 차이)**
 * ###### 오버로딩은 공통점은 메소드이름,리턴값 / 차이점은 매개변수의 형식 
 * ###### 오버라이딩은 메소드이름, 리턴값, 매개변수의 형식 모든 것이 일치해야함. 
   ###### 완벽히 일치하면 중복이 되기 때문에 super()를 이용해 코드를 줄이고, 수정할건하고 추가할 건 밑에 로직을 작성하면됨. 
       Overroading 은 "끌고 온다" , Overriding 은 "올라탄다". 
