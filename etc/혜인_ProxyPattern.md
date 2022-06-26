### 정의

- 실제 기능을 수행하는 객체(Real Object) 대신 가상의 객체(Proxy Object)를 사용해 로직의 흐름을 제어하는 디자인 패턴

---

- 어떤 객체를 사용하고자 할때, 객체를 직접적으로 참조 하는것이 아니라, 해당 객체를 대행(대리, proxy)하는 객체를 통해 대상객체에 접근하는 방식을 사용
    - 이 방식을 사용하면 해당 객체가 메모리에 존재하지 않아도 기본적인 정보를 참조하거나 설정할 수 있음
    - 또한 실제 객체의 기능이 반드시 필요한 시점까지 객체의 생성을 미룰 수 있음

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/56d9bfc5-0d0d-4103-a08f-6e87b6c388ab/Untitled.png)

### **프록시 패턴 장점**

1. 사이즈가 큰 객체(ex : 이미지)가 로딩되기 전에도 프록시를 통해 참조를 할 수 있다.
2. 실제 객체의 public, protected 메소드들을 숨기고 인터페이스를 통해 노출시킬 수 있다.
3. 로컬에 있지 않고 떨어져 있는 객체를 사용할 수 있다.
4. 원래 객체의 접근에 대해서 사전처리를 할 수 있다.
5. 원래 하려던 기능을 수행하며 그외의 부가적인 작업(로깅, 인증, 네트워크 통신 등)을 수행하기에 좋습니다.
6. 비용이 많이 드는 연산(DB 쿼리, 대용량 텍스트 파일 등)을 실제로 필요한 시점에 수행할 수 있습니다.
7. 사용자 입장에서는 프록시 객체나 실제 객체나 사용법은 유사하므로 사용성이 좋습니다.

### **프록시 패턴 단점**

1. 객체를 생성할때 한단계를 거치게 되므로, 빈번한 객체 생성이 필요한 경우 성능이 저하될 수 있다.
2. 프록시 내부에서 객체 생성을 위해 스레드가 생성, 동기화가 구현되야 하는 경우 성능이 저하될 수 있다.
3. 로직이 난해해져 가독성이 떨어질 수 있다.

### 프록시패턴 구현

Subject.java

```java
public interface Subject {
    String request();
}
```

RealSubject.java

```java
public class RealSubject implements Subject {

    @Override
    public String request() {
        return "HelloWorld";
    }
}
```

Proxy.java

```java
public class Proxy implements Subject {

    private final RealSubject realSubject = new RealSubject();

    @Override
    public String request() {
        return realSubject.request();  //프록시가 실제의 메소드를 호출한다.
    }
}
```

main

```java
public class Main {
    public static void main(String[] args) {
        Subject subject = new Proxy();
        System.out.println(subject.request());
    }
}
```

### 프록시 패턴 사용 이유

- 흐름을 제어할 수 있다
    - 동기적인 처리를 최대한 비동기적으로 처리하기 위함
    
    **프록시패턴 사용하지 않을 때**
    
    - 많은 양의 리소스를 필요로 하는 상황에서 디비쿼리가 엄청나게 느려질 수 있다.
    - 이럴때 지연초기화를 위한 코드작성을 해야하는데 이를 모든 클래스마다 직접 넣어버리면 엄청나게 많은 코드중복이 발생할것이다.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b5c2b882-ac8d-4997-a676-ff94c42d12e5/Untitled.png)
    
    **프록시패턴 사용**
    
    - 프록시객체를 이용하면 요청을 프록시객체가 먼저 받은뒤에 흐름을 제어하여 디비에 쿼리를 날릴 수 있게된다.
    
    ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/5a583d71-25ab-4d13-92f5-dd9b384bce65/Untitled.png)
    
- 실제 메소드가 호출되기 이전에 필요한 기능(전처리등의)을 구현객체 변경없이 추가할 수 있다.
    - 코드변경의 최소화
- 캐시를 사용할 수 있다.
    - 프록시가 내부캐시를 통해 데이터가 캐시에 존재하지 않는 경우에만 주체클래스에서 작업이 실행되도록 할 수 있다.
