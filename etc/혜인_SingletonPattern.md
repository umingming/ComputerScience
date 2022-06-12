## 싱글톤 패턴

### 개념

- 생성자가 여러 차례 호출되더라도 실제로 생성되는 객체는 하나이고 최초 생성 이후에 호출된 생성자는 최초의 생성자가 생성한 객체를 리턴하는 생성패턴

### 장점

- 고정된 메모리 영역을 얻으면서 한 번의 new로 인스턴스를 사용하기 때문에 메모리 낭비를 방지할 수 있다.
- 싱글톤으로 만들어진 클래스의 인스턴스는 전역이기 때문에 다른 클래스의 인스턴스들이 데이터를 공유하기 쉽다
- 인스턴스가 절대적으로 한 개만 존재하는 것을 보증하고 싶을 경우 사용
- 두 번째 이용시부터는 객체 로딩 시간이 줄어 성능이 좋아지는 장점이 있다

### 단점

- 싱글톤 인스턴스가 너무 많은 일을 하거나 많은 데이터를 공유시킬 경우, 다른 클래스의 인스턴스들 간에 결합도가 높아져 ‘개방-폐쇄 원칙’을 위배하게 됨
- 멀티스레드 환경에서 동기화 처리를 하지 않으면 인스턴스가 2개가 생성될 수 있는 가능성이 생기게 됨

## 싱글톤 패턴의 구현

```java
public class Singleton1 {
	private static final Singleton1 instance = new Singleton1();
	
	// 생성자는 외부에서 호출하지 못하게 private 으로 지정
	private Singleton1() {}
	
	public static Singleton1 getInstance() {
		return instance;
	}
}
```

```java
public class Singleton2 {
	private static Singleton2 instance;

	private Singleton2(){}

	public static Singleton2 getInstance() {
		if(instance == null) {
			instance = new Singleton2();
		}
		return instance;
	}
}
```

## Thread-safe한 싱글톤 만드는 방법

### 1. Thread safe Lazy initialization (게으른 초기화)

```java
public class ThreadSafeLazyInitialization{     
	private static ThreadSafeLazyInitialization instance;
	
	private ThreadSafeLazyInitialization(){}
	
	// synchronized 키워드 사용
	public static synchronized ThreadSafeLazyInitialization getInstance(){
		if(instance == null){
			instance = new ThreadSafeLazyInitialization();
		}        
		return instance;    
	} 
}
```

- synchronized 특성상 비교적 큰 성능저하가 발생하므로 권장하지 않는 방법

### 2. Thread safe lazy initialization + Double-checked locking

```java
public class ThreadSafeLazyInitialization{     
	private static ThreadSafeLazyInitialization instance;
	
	private ThreadSafeLazyInitialization(){}
	
	public static ThreadSafeLazyInitialization getInstance(){
		if(instance == null){
			synchronized (ThreadSafeLazyInitialization.class) {
				if(instance == null)
					instance = new ThreadSafeLazyInitialization();
			}
		}        
		return instance;    
	} 
}
```

- getInstance()에 synchronized를 사용하는 것이 아니라 첫 번째 if문으로 인스턴스의 존재여부를 체크하고 두 번째 if문에서 다시 한번 체크할 때 동기화 시켜서 인스턴스를 생성하므로 thread-safe하면서도 처음 생성 이후에 synchonized 블럭을 타지 않기 때문에 성능저하를 완화했다.

### 3. Initialization on demand holder idiom (holder에 의한 초기화)

```java
public class Something {
	private Something() {}

	private static class LazyHolder {
		public static final Something INSTANCE = new Something();
	}
	
	public static Something getInstance() {
		return LazyHolder.INSTANCE;
	}
}
```

- 클래스안에 클래스(Holder)를 두어 JVM의 Class loader 매커니즘과 Class가 로드되는 시점을 이용한 방법
