# Object Relational Mapping

## 객체와 엔티티

22/05/15

📎 객체

- **상속** 클래스
    
    ![Untitled](Object%20Relational%20Mapping%20f6d182a44bfa4dd8b7d2b4d5cc99c7bb/Untitled.png)
    
- **참조**를 이용하는 연관 관계
    
    ![Untitled](Object%20Relational%20Mapping%20f6d182a44bfa4dd8b7d2b4d5cc99c7bb/Untitled%201.png)
    

📎 엔티티

- 슈퍼/서브 타입 관계
    
    ![Untitled](Object%20Relational%20Mapping%20f6d182a44bfa4dd8b7d2b4d5cc99c7bb/Untitled%202.png)
    
- 연관 관계에서 **외래 키** 사용
    
    ![Untitled](Object%20Relational%20Mapping%20f6d182a44bfa4dd8b7d2b4d5cc99c7bb/Untitled%203.png)
    

📎 SQL Mapper

- 객체와 SQL문을 매핑하여 데이터를 객체화
- SQL문의 질의 결과와 객체를 매핑
- SQL문을 직접 작성하여 데이터베이스의 데이터를 다룸.

📎 SQL Mapper 예

- 엔티티에 외래 키 칼럼 추가할 경우, 해당 엔티티의 Sequence를 **필드**에 추가
    
    ```java
    class Item {
    	private int seq;
    	private String name;
    	**private String memberSeq;**
    }
    ```
    
- DAO 쿼리 수정
    
    ```sql
    insert into Item (seq, name, member_seq) values (?, ?, ?);
    ```
    

📎 SQL Mapper 장점

- DB 튜닝 수월
- SQL 쿼리 세부 **변경** 편리

📎 SQL Mapper 단점

- RDB 변경이 번거로움
- 테이블로부터 객체 도출 한계

📎 ORM

- 객제 지향 프로그래밍의 **클래스**와 관계형 데이터베이스의 **테이블**를 **매핑**하는 기술
- 클래스와 테이블 간의 호환 문제를 ORM 알아서 해결; SQL 쿼리 자동 생성
- 애플리케이션 객체를 RDB 테이블에 자동으로 영속화해줌.

📎 ORM 예

- 기존 클래스에 컬럼 추가
    
    ```java
    **@Entity**
    class Item {
    	private int seq;
    	private String name;
    	**@ManyToOne(name = "MEMBER_SEQ")**
    	****private Member member;
    }
    ```
    

📎 ORM 장점

- **객체** 모델에 집중
- 가독성 향상
- 유지보수 용이

📎 ORM 단점

- 속도 및 일관성 저하
- 별도의 튜닝 필요

## JPA

📎 JPA란?

- 자바에서 지원하는 **ORM** 기술
- 애플리케이션과 JDBC 사이에서 동작

📎 Hibernate

- JPA 구현체로 지원 메소드 내부에 JDBC API 동작
- 개발자가 직접 SQL 작성할 필요 없음.

![Untitled](Object%20Relational%20Mapping%20f6d182a44bfa4dd8b7d2b4d5cc99c7bb/Untitled%204.png)