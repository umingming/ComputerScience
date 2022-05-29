## 빌더 패턴

### 개념

- 복잡한 인스턴스를 **조립**하여 만드는 구조
- 복합 객체를 생성할 때 객체를 생성하는 방법(과정)과 객체를 구현(표현)하는 방법을 분리함으로써 동일한 생성 절차에서 서로 다른 표현 결과를 만들 수 있는 디자인 패턴

### 장점

- 필요한 데이터만 설정할 수 있음
- 유연성을 확보할 수 있음
- 가독성을 높일 수 있음
- 변경 가능성을 최소화할 수 있음

## 빌더 패턴의 구현

### 빌더 패턴 적용 전

- 불변한 객체를 생성한다고 가정

```java
public User (String firstName, String lastName, int age, String phone, String address){
	this.firstName = firstName;
	this.lastName = lastName;
	this.age = age;
	this.phone = phone;
	this.address = address;
}

// User user1 = new User("Hyein", "Lee", 89, "010-1234-5678", "경기도 성남시 황새울로");
// User user2 = new User("Hyein", "Kim", null, null, null);
```

- `firstName`, `lastName` 은 필수, `age`, `phone`, `address` 는 선택이라고 할 때, 더 많은 생성자가 필요

```java
public User (String firstName, String lastName, int age, String phone){ ...	}
public User (String firstName, String lastName, String phone, String address){ ...	}
public User (String firstName, String lastName, int age){ ...	}
public User (String firstName, String lastName){ ...	}
```

- 위와 같이 필수 매개변수를 가지는 생성자를 필두로, 선택 매개변수를 가지는 생성자를 추가하여 여러 생성자를 가지는 디자인 패턴을 `점층적 생성자 패턴(Telescoping Constructor Pattern)` 이라고 한다
- 이렇게 생성자가 많이 만들어지는 문제를 **텔레스코핑 생성자 문제**라고 함
    - 생성자를 호출하는 입장에서는 매개변수가 맞는지 헷갈리는 경우가 많다
    - 생성자의 수가 많아지고 클래스가 복잡해진다
    - 매개변수의 타입이 같은 경우 생성자를 만들 수 없을 수도 있다
- 이 문제를 해결하기 위해 setter 메소드를 도입하면 불변성을 잃게 됨
- 그래서 나온 게 builder 패턴

### 빌더 패턴 적용

```java
public class User
{
	// 불변성 확보를 위해 변수를 final로 설정
  // final을 쓰지 않아도 setter를 구현하지 않으면 불변성 유지할 수 있음... 더 찾아보자
	private final String firstName; // 필수
	private final String lastName;  // 필수
	private final int age;          // 선택
	private final String phone;     // 선택
	private final String address;   // 선택

	private User(UserBuilder builder) {
		this.firstName = builder.firstName;
		this.lastName = builder.lastName;
		this.age = builder.age;
		this.phone = builder.phone;
		this.address = builder.address;
	}

	// getter만 구현하고, setter를 구현하지 않음으로써 불변성 확보
	public String getFirstName() {
		return firstName;
	}
	public String getLastName() {
		return lastName;
	}
	public int getAge() {
		return age;
	}
	public String getPhone() {
		return phone;
	}
	public String getAddress() {
		return address;
	}

	@Override
	public String toString() {
		return "User: "+this.firstName+", "+this.lastName+", "+this.age+", "+this.phone+", "+this.address;
	}
	
	// 내부 클래스로 builder 클래스 정의
	public static class UserBuilder
	{
    // 필수적인 변수만 final 사용
		private final String firstName;
		private final String lastName;
		private int age;
		private String phone;
		private String address;

	  // Builder 생성자 매개변수는 필수 변수만을 포함
		public UserBuilder(String firstName, String lastName) {
			this.firstName = firstName;
			this.lastName = lastName;
		}

    // 선택적인 변수는 추가적인 메서드를 구현하여 생성
		public UserBuilder age(int age) {
			this.age = age;
			return this;
		}
		public UserBuilder phone(String phone) {
			this.phone = phone;
			return this;
		}
		public UserBuilder address(String address) {
			this.address = address;
			return this;
		}

		// 생성된 객체 반환
		public User build() {
			User user =  new User(this);
			validateUserObject(user);
			return user;
		}

		private void validateUserObject(User user) {
			//Do some basic validations to check
			//if user object does not break any assumption of system
		}
	}
}
```

- 객체 생성하기

```java
public static void main(String[] args) {
	User user1 = new User.UserBuilder("Hyein", "Lee")
                       	     .age(30)
			     .phone("010-1234-5678")
			     .address("Fake address 1234")
			     .build();

	User user2 = new User.UserBuilder("엄", "바보")
			     .age(40)
			     .phone("1234")
			     //no address
			     .build();

	User user3 = new User.UserBuilder("yum", "ding")
			      //No age
			      //No phone
			      //no address
			      .build();
}
```

- 멤버를 `final`로 설정하여 불변성을 유지할 수 있다
- 선택적인 변수의 경우 `null`로 설정할 필요가 없다. 또한 생성자 오버로딩을 하지 않아 선택적인 변수를 가진 객체도 동일한 방법으로 생성할 수 있다.
- 각 변수의 이름에 해당하는 메서드를 chaining 방식으로 접근하여 초기화할 수 있다
    - 생성자의 매개변수 순서를 기억할 필요가 없고, 생성 과정에서의 가독성이 훨씬 좋아진다.
- 만약 새로운 멤버 변수가 추가되더라도 기존 객체 생성 코드를 수정하지 않아도 된다.
- 추가적으로 빌더 클래스 내부에 유효성 검사 메서드를 추가한다면 멤버 생성 과정에서의 논리적인 에러를 사전에 차단할 수 있다.
