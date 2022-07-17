### 정의

- 인터페이스를 이용하여 서로 연관된, 또는 의존하는 객체를 구현 클래스를 지정 하지 않고도 생성할 수 있는 패턴
    
    ![image](https://user-images.githubusercontent.com/90780701/178145145-1f1acfd6-07d1-4865-a768-62caaebedf84.png)


### 팩토리 메소드 패턴과의 차이점

- 팩토리 메소드 패턴
    - 조건에 따른 객체 생성을 팩토리 클래스로 위임하여, 팩토리 클래스에서 객체를 생성하는 패턴
- 추상 팩토리 패턴
    - 서로 관련이 있는 객체들을 통째로 묶어서 팩토리 클래스로 만들고, 이들 팩토리를 조건에 따라 생성하도록 다시 팩토리를 만들어서 객체를 생성하는 패턴

### 디자인 패턴 적용 전

- 관리하기 힘듦 → 의존하는 객체가 늘어날수록 관리 힘듦
    
    ```java
    class DependentShoesStore {
    
        public Shoes makeShoes(String style, String name) {
            Shoes shoes = null;
            if (style.equals("Japan")) {
                if (name.equals("blackShoes")) shoes = new JPStyleBlackShoes();
                else if (name.equals("brownShoes")) shoes = new JPStyleBrownShoes();
                else if(name.equals("redShoes")) shoes = new JPStyleRedShoes();
            }
            else if(style.equals("france")) {  
                if (name.equals("blackShoes")) shoes = new FRStyleBlackShoes();
                else if (name.equals("brownShoes")) shoes = new FRStyleBrownShoes();
                else if(name.equals("redShoes")) shoes = new FRStyleRedShoes(); 
            }
    
            shoes.prepare();
            shoes.packing();
            return shoes;
        }
    }
    ```
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/65b14e8e-e99b-49c4-b634-1bc88b70b3f1/Untitled.png)
    

### 추상 팩토리 패턴 적용

- 지역별로 소규모 신발재료 공장을 만든다
    
    ```java
    interface ShoesIngredientFactory {
     
        public Bottom makeBottom();
        
        public Leather makeLeather();
     
        public boolean hasPattern();
     
    }
    ```
    
- 일본
    
    ```java
    class JPShoesIngredientFactory implements ShoesIngredientFactory {
     
        @Override
        public Bottom makeBottom() return new RubberBottom();
     
        @Override
        public Leather makeLeather() return new LeatherOfCows();
        
        @Override
        public boolean hasPattern() return false;
    }
    ```
    
- 프랑스
    
    ```java
    class FRShoesIngredientFactory implements ShoesIngredientFactory {
     
        @Override
        public Bottom makeBottom() return new PlasticAndRubberBottom();
     
        @Override
        public Leather makeLeather() return new LeatherOfSheeps();
     
        @Override
        public boolean hasPattern() return true;
    }
    ```
    
- 신발재료 인터페이스
    
    ```java
    interface Bottom {
     
        public String getName();
     
    }
    ```
    
    ```java
    interface Leather {
     
        public String getName();
     
    }
    ```
    
- 신발재료 구현 클래스
    
    ```java
    class RubberBottom implements Bottom {
     
        @Override
        public String getName() return "고무";
     
    }
    ```
    
    ```java
    class PlasticAndRubberBottom implements Bottom {
     
        @Override
        public String getName() return "플라스틱, 고무";
     
    }
    ```
    
    ```java
    class LeatherOfCows implements Leather {
     
        @Override
        public String getName() return "소가죽";
     
    }
    ```
    
    ```java
    class LeatherOfSheeps implements Leather {
     
        @Override
        public String getName() return "양가죽";
     
    }
    ```
    
- 신발 객체 추상 클래스
    
    ```java
    abstract class Shoes {
     
        String name;
        Bottom bottom;
        Leather leather;
        boolean hasPattern;
     
        abstract void assembling(); // 신발을 조립하는 추상 메소드
     
        void prepare() {
            System.out.println("완성된 신발을 준비 중입니다.");
        }
     
        void packing() {
            System.out.println("준비된 신발을 포장 중입니다.");
        }
     
        public String getName(){
            return name;
        }
     
        public void setName(String name) {
            this.name = name;
        }
     
    }
    ```
    
- 색깔별 신발 객체 구현 클래스
    
    ```java
    class BlackShoes extends Shoes {
     
        ShoesIngredientFactory shoesIngredientFactory;
     
        public BlackShoes(ShoesIngredientFactory shoesIngredientFactory) {
            this.shoesIngredientFactory = shoesIngredientFactory;
        }
     
        @Override
        void assembling() { 
            System.out.println("신발을 제작중입니다. " + name);
            leather = shoesIngredientFactory.makeLeather();
            bottom = shoesIngredientFactory.makeBottom();
            System.out.println("신발 정보 : 밑창은 " + bottom.getName() + " 사용 하였으며, 가죽은 " + leather.getName() + " 사용하였습니다.");
        }
     
    }
    ```
    
    ```java
    class BrownShoes extends Shoes {
     
        ShoesIngredientFactory shoesIngredientFactory;
     
        public BrownShoes(ShoesIngredientFactory shoesIngredientFactory) {
            this.shoesIngredientFactory = shoesIngredientFactory;
        }
     
        @Override
        void assembling() {
            System.out.println("신발을 제작중입니다. " + name);
            leather = shoesIngredientFactory.makeLeather();
            bottom = shoesIngredientFactory.makeBottom();
            System.out.println("신발 정보 : 밑창은 " + bottom.getName() + " 사용 하였으며, 가죽은 " + leather.getName() + " 사용하였습니다.");
        }
     
    }
    ```
    
    ```java
    class RedShoes extends Shoes {
     
        ShoesIngredientFactory shoesIngredientFactory;
     
        public RedShoes(ShoesIngredientFactory shoesIngredientFactory) {
            this.shoesIngredientFactory = shoesIngredientFactory;
        }
     
        @Override
        void assembling() { 
            System.out.println("신발을 제작중입니다. " + name);
            leather = shoesIngredientFactory.makeLeather();
            bottom = shoesIngredientFactory.makeBottom();
            System.out.println("신발 정보 : 밑창은 " + bottom.getName() + " 사용 하였으며, 가죽은 " + leather.getName() + " 사용하였습니다.");
        }
     
    }
    ```
    
    - 국가별로 BlackShoes, BrownShoes, RedShoes 각각 다 만들어주지 않아도 됨
    - ShoesIngredientFactory 인스턴스를 생성자로 받아서 원재료를 직접 받음
    - assembling 메소드를 보면 가죽과 밑창을 각각 공장 인스턴스에서 받아 조립하고 있음
    - Shoes 클래스는 그냥 공장에서 건네주는 재료로 신발을 조립만하기 때문에, 어떤 지역의 팩토리를 사용하든 Shoes 클래스는 언제든 재활용 할 수 있다
- 신발 가게 추상 클래스
    
    ```java
    abstract class ShoesStore {
     
        public Shoes orderShoes(String name) {
     
            Shoes shoes;
     
            shoes = makeShoes(name);
            shoes.assembling();
            shoes.prepare();
            shoes.packing();
     
            return shoes;
     
        }
     
        abstract Shoes makeShoes(String name);
     
    }
    ```
    
    - 각 나라의 스토어들은 이 Store 추상 클래스를 상속받아 추상 메소드인 makeShoes 메소드를 나라에 맞게 오버라이드하여 구현
    - orderShoes는 전세계 공통 프레임워크이고, orderShoes안에 있는 makeShoes 단계만 각 나라의 특징에 맞게 바뀌는 것 뿐
- 신발 매장 구현 클래스
    
    ```java
    class JPShoesStore extends ShoesStore {
     
        @Override
        Shoes makeShoes(String name) { 
            Shoes shoes = null;
            ShoesIngredientFactory shoesIngredientFactory = new JPShoesIngredientFactory();
            
            if(name.equals("blackShoes")) {
                shoes = new BlackShoes(shoesIngredientFactory);
                shoes.setName("일본 스타일의 검은 신발");
            }
            else if(name.equals("brownShoes")) {
                shoes = new BrownShoes(shoesIngredientFactory);
                shoes.setName("일본 스타일의 갈색 신발");
            }
            else if (name.equals("redShoes")) {
                shoes = new RedShoes(shoesIngredientFactory);
                shoes.setName("일본 스타일의 빨간 신발");
            }
     
            return shoes;
        }
     
    }
    ```
    
    ```java
    class FRShoesStore extends ShoesStore {
     
        @Override
        Shoes makeShoes(String name) { 
            Shoes shoes = null;
            ShoesIngredientFactory shoesIngredientFactory = new FRShoesIngredientFactory();
            
            if(name.equals("blackShoes")) {
                shoes = new BlackShoes(shoesIngredientFactory);
                shoes.setName("프랑스 스타일의 검은 신발");
            }
            else if(name.equals("brownShoes")) {
                shoes = new BrownShoes(shoesIngredientFactory);
                shoes.setName("프랑스 스타일의 갈색 신발");
            }
            else if(name.equals("redShoes")) {
                shoes = new RedShoes(shoesIngredientFactory);
                shoes.setName("프랑스 스타일의 빨간 신발");
            }
     
            return shoes;
        }
     
    }
    ```
    
- 메인 클래스
    
    ```java
    public class Main {
     
        public static void main(String[] args) {
     
            JPShoesStore jpStore = new JPShoesStore();
            jpStore.orderShoes("blackShoes");
     
            FRShoesStore frStore = new FRShoesStore();
            frStore.orderShoes("redShoes");
     
        }
     
    }
    ```
