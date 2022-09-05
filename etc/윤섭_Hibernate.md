# Hibernate

## ****Hibernate****

                                                                                                                                                 22/09/05

📎 ****Hibernate란?****

![Untitled](Hibernate%20dfa3280b08124ba3aaa76b3ff46338c7/Untitled.png)

<aside>
💡 하이버네이트는 자바 언어를 위한 ORM 프레임워크에요. JPA의 구현체로, JPA 인터페이스를 구현하며, 내부적으로 JDBC API를 사용해요.

JPA는 관계형 데이터베이스와 객체의 패러다임 불일치 문제를 해결할 수 있다는 점과 영속성 컨텍스트(엔티티를 영구 저정하는 환경) 제공이 큰 특징이에요.

</aside>

**📎 JPA란?**

<aside>
💡 자바 애플리케이션에서 관계형 데이터베이스를 사용하는 방식을 정의한 인터페이스에요. 라이브러리가 아닌 인터페이스이므로 특정 기능을 하진 않아요.

</aside>

📎 **JDBC란?**

<aside>
💡 자바 프로그래밍 언어와 다양한 데이터베이스 SQL 또는 테이블 형태의 데이터 사이에 독립적인 연결을 지원하는 표준이에요. 즉, DB 작업을 위한 표준이라 볼 수 있어요.DBMS 회사들이 JDBC 인터페이스를 구현하여 제공해요. 이를 JDBC 드라이버라고 하는데, 결국 JDBC 드라이버란 DBMS 회사들이 자신들의 데이터베이스 시스템에 접근 할 수 있도록 표준 JDBC 인터페이스에 명시된 메소드들을 구현한 것이라 볼 수 있어요.따라서 JDBC API를 사용할 경우 하나의 자바 응용 프로그램만으로 JDBC 드라이버를 제공하는 어떤 종류의 관계형 DBMS에도 접근이 가능하고, 사용자들은 특정 회사의 데이터베이스의 정확한 사용 방법을 몰라도 JDBC API만 알면 데이터베이스 조작이 가능하게 돼요.

</aside>

## 하이버네이트 장점

                                                                                                                                                 22/09/05

**📎 생산성**

- Hibernate는 SQL을 직접 사용하지 않고, 메서드 호출만으로 쿼리가 수행돼요. 즉, SQL 반복 작업을 하지 않음으로 생산성이 높아져요
- SQL을 몰라도 되는 건 아니에요. (내부 동작에 대해 알아야 하기 때문)

**📎 유지보수**

- 테이블 컬럼이 변경되었을 때, 테이블과 관련된 DAO의 파라미터, 결과, SQL 등을 대신 수행해줘요. 이로 인해 유지보수 측면에서 높아져요

**📎 특정 벤더에 종속적이지 않음**

- JPA는 추상화된 데이터 접근 계층을 제공하기 때문에 특정 벤더에 종속적이지 않아요
- 설정 파일에서 JPA에게 어떤 DB를 사용하고 있는지를 알려주기만 하면 얼마든지 DB를 바꿀 수 있어요.

**📎 패러다임 불일치 해결**

- 상속, 연관 관계, 객체 그래프 탐색, 비교 등 객체와 관계형 데이터베이스와의 패러다임 불일치를 해결할 수 있어요.

## 하이버네이트 단점

                                                                                                                                                 22/09/05

**📎 성능**

- 메서드 호출만으로 쿼리를 수행하는 것은 직접 SQL을 작성하는 것보다는 성능상 좋지 않아요.

**📎 세밀함**

- 메서드 호출만으로 DB 데이터를 조작하기에는 한계가 있어요. 이를 보완하기 위해 JPQL을 지원해요
- NativeQuery를 지원하여 SQL 자체 쿼리도 작성할 수 있어요.

## 사용법(maven 기준)

                                                                                                                                                 22/09/05

**📎 1. pom.xml에 의존성 추가**

```xml
<!-- https://mvnrepository.com/artifact/org.hibernate/hibernate-core -->
<dependency>
	<groupId>org.hibernate</groupId>
	<artifactId>hibernate-core</artifactId>
	<version>5.4.14.Final</version>
</dependency>

<!-- https://mvnrepository.com/artifact/mysql/mysql-connector-java -->
<dependency>
	<groupId>mysql</groupId>
	<artifactId>mysql-connector-java</artifactId>
	<version>8.0.20</version>
</dependency>

<!-- https://mvnrepository.com/artifact/org.projectlombok/lombok -->
<dependency>
	<groupId>org.projectlombok</groupId>
	<artifactId>lombok</artifactId>
	<version>1.18.12</version>
	<scope>provided</scope>
</dependency>
```

**📎 2. Hibernate Configuration을 설정**

- 이 설정은 어떻게 Hibernate가 jdbc를 이용하여 데이터베이스에 접속하는지를 기술한다.
    - 설정의 대부분이 jdbc 접속을 위한 정보들이다.
    
- Hibernate 세팅을 위해서 xml파일을 지정한다.
    - hibernate.cfg.xml파일을 classpath root에 저장한다.
    
- XML은 상당히 오류찾기가 어려우므로 그냥 붙여넣기 하는 게 속편하다.
    - 아래의 설정은 hibernate 기본 connection pool의 크기가 1로 되어 있고
    - mysql dialect를 사용하여 hibernate 연동 DB가 MySql이라는 것을 알 수 있다.

```java
<!DOCTYPE hibernate-configuration PUBLIC
        "-//Hibernate/Hibernate Configuration DTD 3.0//EN"
        "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">

<hibernate-configuration>

  <session-factory>

    <!-- JDBC Database connection settings -->
      <property name="connection.driver_class">com.mysql.cj.jdbc.Driver</property>
      <property name="connection.url">jdbc:mysql://localhost:3306/hb_student_tracker?useSSL=false&amp;serverTimezone=Asia/Seoul</property>
      <property name="connection.username">hbstudent</property>
      <property name="connection.password">hbstudent</property>

    <!-- JDBC connection pool settings ... using built-in test pool -->
      <property name="connection.pool_size">1</property>

    <!-- Select our SQL dialect -->
      <property name="dialect">org.hibernate.dialect.MySQLDialect</property>

    <!-- Echo the SQL to stdout -->
      <property name="show_sql">true</property>

    <!-- Set the current session context -->
      <property name="current_session_context_class">thread</property>

  </session-factory>

</hibernate-configuration>
```

**📎 3. 데이터베이스 테이블과 매핑될 Entity 클래스를 만들고 Annotation을 설정한다.**

- hibernate에서 테이블과 Entity클래스를 매핑하는 또 다른 방법은 xml을 이용하는 것이다. 정말 귀찮은 방식이다.
- 여기서는 Annotation방식을 사용한다.
- 아래 예제를 보면 hibernate 패키지가 아닌 javax.persistence 아래의 인터페이스를 사용한다. 규약이다.
- 일반적으로 id는 Long 타입을 사용한다.
- 명시적으로 테이블 이름과, 컬럼 이름을 사용해도 된다. 아래는 꼭 필요한 부분만 설정했다.

```java
import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;
import javax.persistence.Table;

import lombok.Data;
import lombok.NoArgsConstructor;

@Entity
@Table(name = "student")
@Data
@NoArgsConstructor
public class Student {
  @Id
  @GeneratedValue(strategy = GenerationType.IDENTITY)
  private Long id;
  
  @Column(name = "first_name")
  private String firstName;
  
  @Column(name = "last_name")
  private String lastName;
  
  @Column
  private String email;

  public Student(String firstName, String lastName, String email) {
    super();
    this.firstName = firstName;
    this.lastName = lastName;
    this.email = email;
  }
}
```

**📎 4. Entity 클래스를 가지고 실제 데이터베이스 처리를 한다.**

- SessionFactory는
    - configuration을 읽고 데이터베이스에 접속한다.
    - 접속 후 Query를 실행할 수 있는 Session 객체를 생성할 수 있다.
    - 프로그램에서 오직 한 번만 생성되고 종료할 때까지 계속 사용된다.
    
- Session 객체는
    - JDBC Connection의 Wrapper이다.
    - 데이터 읽기와 저장에 사용된다.
    - 짧은 시간 사용되며 필요시마다 생성된다.
    - SessionFactory에서 만들어진다.

```java
public class TestJdbc {
  public static void main(String[] args) {

    SessionFactory factory = new Configuration()
        .configure("hibernate.cfg.xml")
        .addAnnotatedClass(Student.class)
        .buildSessionFactory();

    Session session = factory.getCurrentSession();

    try {
      Student tempStudent = new Student("Paul", "Wall", "paul@gmail.com");
      
      session.beginTransaction();
      
      session.save(tempStudent);
      
      session.getTransaction().commit();
      
    } finally {
      factory.close();
    } 
    
//    String jdbcUrl = "jdbc:mysql://localhost:3306/hb_student_tracker?useSSL=false&serverTimezone=Asia/Seoul";
//    String user = "hbstudent";
//    String password = "hbstudent";
//    
//    try {
//      System.out.println("Connecting to Database: " + jdbcUrl);
//      Connection connection = DriverManager.getConnection(jdbcUrl, user, password);
//      
//      System.out.println("connection successful!!!");          
//      
//    } catch (Exception e) {
//      e.printStackTrace();
//    }    
  }
}
```

## 참고

                                                                                                                                                 22/09/05

<aside>
💡 Spring Data JPA는 JPA를 쓰기 편하게 만들어 놓은 모듈이에요.JPA를 한 단계 추상화시킨 Repository라는 인터페이스를 제공함으로써 이루어져요. Repository 인터페이스에 정해진 규칙대로 메소드를 입력하면, Spring이 알아서 해당 메소드 이름에 적합한 쿼리를 날리는 구현체를 만들어서 Bean으로 등록해줘요

</aside>

참고: [https://livenow14.tistory.com/70](https://livenow14.tistory.com/70)

[https://kogle.tistory.com/32](https://kogle.tistory.com/32)