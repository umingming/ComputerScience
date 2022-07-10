# 팩토리 메소드 패턴

### 정의

- 객체 생성 처리를 서브 클래스로 분리해 처리하도록 캡슐화하는 패턴
    - 객체의 생성 코드를 별도의 클래스/메서드로 분리함으로써 객체 생성의 변화에 대비하는 데 유용
        
        ![image](https://user-images.githubusercontent.com/90780701/177039811-1389015e-0f6e-459b-b906-a135303f0b82.png)
        
    - Product: 팩토리 메서드로 생성될 객체의 공통 인터페이스
    - ConcreteProduct: 구체적으로 객체가 생성되는 클래스
    - Creator: 팩토리 메서드를 갖는 클래스
    - ConcreteCreator: 팩토리 메서드를 구현하는 클래스로 ConcreteProduct 객체를 생성

### 예시

- 신발 이름으로 신발을 생성하는 코드
    
    ```java
    // 이름을 통해 신발을 주문 받음
    Shoes orderShoes(String name) {
        // 해당 이름의 신발을 찾아서 특정 구상 객체 생성
        Shoes shoes;
        
        if (name.equals("blackShoes"))     shoes = new BlackShoes();
        else if (name.equals("brownShoes"))shoes = new BrownShoes();
        else if (name.equals("redShoes"))  shoes = new RedShoes();
        
        // 신발을 준비하고 포장하는 메소드
        // 모든 신발 공용 메소드
        shoes.prepare(); 
        shoes.packing(); 
     
        return shoes;
    }
    ```
    
    - 신발의 종류 → 변화 가능한 부분
    - prepare()과 packing() → 제품에 변화가 생기더라도 변하지 않는 부분
- 캡슐화
    - ShoesFactory; 신발을 생성
    
    ```java
    public class ShoesFactory {
     
        public Shoes makeShoes(String name) {
     
           Shoes shoes = null;
           if (name.equals("blackShoes"))     shoes = new BlackShoes();
           else if (name.equals("brownShoes"))shoes = new BrownShoes();
           else if (name.equals("redShoes"))  shoes = new RedShoes();
           
           return shoes;
        }
     
    }
    ```
    
    - ShoesStore; 신발을 판매
    
    ```java
    public class ShoesStore {
         
        ShoesFactory factory;
     
        public ShoesStore(ShoesFactory factory) {
            this.factory = factory;
        }
       
        Shoes orderShoes(String name) {
            Shoes shoes = factory.makeShoes(name);
            shoes.prepare(); 
            shoes.packing(); 
     
            return shoes;
        }
    }
    ```
    
- 여러 신발 매장들
    - 다른 스타일의 신발을 만듦
    
    ```java
    JapanShoesStore jpStore= new JapanShoeStore (new JapanShoesFactory());
    jpStore.order("blackShoes");
    
    FranceShoesStore  frStore = new FranceShoesStore (new FranceShoesFactory());
    frStore.order("blackShoes");
    ```
    
- ShoesStore 추상 클래스 선언
    - 신발 생산 과정 전체는 같도록 함
    
    ```java
    public abstract class ShoesStore {
     
        public ShoesStore orderShoes(String name) {
            Shoes shoes = makeShoes(name);
            shoes.prepare();
            shoes.packing();
     
            return shoes;
        }
     
        abstract Shoes makeShoes(String name);
    }
    ```
    
- JapanShoesStore
    
    ```java
    class JapanShoesStore extends ShoesStore {
     
        @Override
        Shoes makeShoes(String name) {
            if (name.equals("blackShoes")) return new JPStyleBlackShoes();  
            else if (name.equals("brownShoes")) return new JPStyleBrownShoes();
            else if (name.equals("redShoes")) return new JPStyleRedShoes();
            else return null;
       }
    }
    ```
    
- FranceShoesStore
    
    ```java
    class FranceShoesStore extends ShoesStore {
     
        @Override
        Shoes makeShoes(String name) {
            if (name.equals("blackShoes")) return new FRStyleBlackShoes();  
            else if (name.equals("brownShoes")) return new FRStyleBrownShoes();
            else if (name.equals("redShoes")) return new FRStyleRedShoes();
            else return null;
       }
    }
    ```
    
- 하위 클래스에서 메소드를 오버라이딩하여, 슈퍼클래스에 있는 orderShoes 메소드에서는 어떤 신발이 만들어 지는지 전혀 모름
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6f9e3728-05a7-447f-9a87-74d226038d46/Untitled.png)
    
- Shoes.java
    
    ```java
    abstract class Shoes {
     
        String name;
        String bottom;
        String leather;
        boolean hasPattern;
     
        void prepare() {
            System.out.println("주문하신 신발을 준비중입니다.");
        }
     
        void packing() {
            System.out.println("준비 완료된 신발을 포장중입니다.");
        }
     
        public String getName() {
            return name;
        }
    }
    ```
    
- JPStyleBlackShoes.java
    
    ```java
    class JPStyleBlackShoes extends Shoes {
     
        public JPStyleBlackShoes() { 
            name = "일본 스타일의 검은 구두";
            bottom = "굽이 높은 밑창";
            leather = "스웨이드";
            hasPattern = false;
        }
     
    }
    ```
    
- FRStyleBlackShoes.java
    
    ```java
    class FRStyleBlackShoes extends Shoes {
     
        public FRStyleBlackShoes() { 
            name = "프랑스 스타일의 검은 구두";
            bottom = "일반 굽높이 밑창";
            leather = "스웨이드";
            hasPattern = true;
        }
     
    }
    ```
    
- [참고] 추상 메소드가 없는 추상 클래스
    
    <aside>
    💡 **추상 메소드가 없는 추상 클래스**
    Shoes 클래스는 추상 메소드가 존재하지 않지만 추상 클래스로 선언되었기 때문에 new Shoes();로 직접 객체 생성은 불가능하고,
    
    Shoes 클래스를 상속받는 클래스에서 Shoes를 참조변수로하여 객체 생성을 할 수 있다.
    추상 메소드 존재 O -> 무조건 클래스도 추상 클래스로 선언
    ****추상 메소드 존재 X -> 현재 클래스로 다이렉트 객체 생성을 막고 싶을 때, 추상 클래스로 선언
    
    </aside>
    
- 팩토리 메소드 패턴 사용
    
    ```java
    public class Main {
     
        public static void main(String[] args) {
            
            // 일본과 프랑스에 현지 트렌드에 맞춰 매장을 열었음
            ShoesStore jpStore = new JapanShoesStore();
            ShoesStore frStore = new FranceShoesStore();
          
            // 일본 매장에서 검은 신발 주문
            Shoes shoes = jpStore.orderShoes("blackShoes");
            System.out.println("일본 매장에서 주문한 검은 신발 : " + shoes.getName());
            
            System.out.println();
            
            // 프랑스 매장에서 검은 신발 주문
            shoes = frStore.orderShoes("blackShoes");
            System.out.println("프랑스 매장에서 주문한 검은 신발  : " + shoes.getName());
     
        }
     
    }
    ```
    
- 출력 결과
    
    ```basic
    > 주문하신 신발을 준비중입니다.
    > 준비 완료된 신발을 포장중입니다.
    > 일본 매장에서 주문한 검은 신발 : 일본 스타일의 검은 구두
    > 
    > 주문하신 신발을 준비중입니다.
    > 준비 완료된 신발을 포장중입니다.
    > 프랑스 매장에서 주문한 검은 신발 : 프랑스 스타일의 검은 구두
    ```
    

### 정리

- 팩토리 메소드 패턴은 객체를 만들어내는 부분을 자식 클래스에 위임하는 패턴
- new 키워드를 호출하는 부분을 서브 클래스에 위임하였기 때문에, 상위 클래스인 ShoesStore 클래스 내부에는 new 라는 키워드가 존재하지 않는다.
- 상위 클래스가 아닌 하위 클래스에서 어떤 클래스를 만들지 결정하게 하도록 하는 것
- 하위 클래스에서 추상 메소드인 makeShoes메소드를 오버라이딩 하였기 때문에, 상위 클래스에 있는 orderShoes 메소드에서는 어떤 신발이 만들어 지는지 전혀 모름
- 동적 바인딩된 그 메소드에서 주는 신발을 받아서 준비하고 포장해서 내놓을 뿐
- **객체 지향 프로그래밍 세계에서 자식은 부모를 알아도, 부모는 자식을 모른다.**
