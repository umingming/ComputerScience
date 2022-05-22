# DNS

### 도메인(Domain)

- 웹 브라우저를 통해 특정 사이트에 진입을 할 때, IP 주소를 대신하여 사용하는 주소
- 도메인을 이용해서 한눈에 파악하기 힘든 IP 주소를 보다 분명하게 나타낼 수 있다.

### ****DNS(Domain Name System)****

- 네트워크에서 도메인 이름을 숫자로 된 IP 주소로 변환해주는 TCP/IP 서비스를 DNS라 한다.
- 상위 기관에서 인증된 기관에게 도메인을 생성하거나 IP 주소로 변경할 수 있는 ‘권한’을 부여
- DNS는 상위 기관과 하위 기관과 같은 ‘**계층 구조**’를 가지는 **분산 데이터베이스 구조**를 가진다.

### DNS 동작 방식

![Untitled (1)](https://user-images.githubusercontent.com/90780701/169696075-56eeb1ef-d050-43a7-a9eb-8fa690c95acc.png)

1. 도메인 주소 입력
2. 웹 브라우저가 리졸버에게 요청
    - www.example.com의 IP주소 알려주세요
3. Root DNS 서버에 "www.example.com" query
4. Root DNS 서버에서 "com 도메인"을 관리하는 TLD Name 서버 정보 전달
5. TLD Name 서버에 "www.example.com" query
6. TLD Name 서버에서 "example.com" 관리하는 DNS 정보 전달
7. "example.com" 도메인을 관리하는 DNS 서버에 "www.example.com"에 대한 IP 주소 query
8. 리졸버에게 IP주소 반환
9. 리졸버가 IP주소 정보 전달

### ****DNS Server****

**Local DNS Server (Recursive DNS Server)**

- 사용자가 가장 먼저 접근하는 DNS 서버. DNS 쿼리를 통해 얻은 데이터를 일정 기간 캐시로 저장해둔다. 일반적으로 KT, LG, SK 등의 ISP DNS 서버를 사용한다.

**Root Name Server (Root DNS Server )**

- 국제인터넷주소관리기구(ICANN)에서 직접 관리하는 서버로 인터넷상의 모든 TLD DNS 서버 IP 주소를 저장해두고 전 세계에 13개만이 존재한다.

**TLD Name Server (Top-Level-Domain DNS Server )**

- ICANN의 지사인 인터넷 할당 번호 관리기관(IANA)에서 관리하는 서버로 Authoritative Name Server의 주소를 저장해둔다.

**Authoritative Name Server (Authoritative DNS Server )**

- 실제 도메인과 IP 주소를 매칭한 정보가 저장/변경되는 서버로 보통 가비아, 후이즈와 같은 도메인/호스팅 업체의 네임서버를 의미한다. 개인 DNS 서버를 구축한 경우에도 여기에 해당한다.

### DNS Query 방법

**반복적 질의 (Iterative Query)**

![https://user-images.githubusercontent.com/49037411/133917371-a6ade083-67e3-40c6-bfcf-ab66da7314e5.png](https://user-images.githubusercontent.com/49037411/133917371-a6ade083-67e3-40c6-bfcf-ab66da7314e5.png)

- 사용자가 Local DNS 서버에 query를 보내면 Local DNS 서버가 Root name 서버에 query를 보내 TLD 서버의 주소를 반환받고, 다시 TLD 서버에 query를 보낸다. 이렇게 최종 IP 주소를 받을 때까지 요청과 응답을 계속해서 Local DNS 서버가 반복하는 방법이다.

**재귀적 질의 (Recursive Query)**

![https://user-images.githubusercontent.com/49037411/133917392-cd194259-7aaf-4d01-9a04-e249364b27f8.png](https://user-images.githubusercontent.com/49037411/133917392-cd194259-7aaf-4d01-9a04-e249364b27f8.png)

- 사용자가 Local DNS 서버에 query를 보내면 Local DNS server가 Root name 서버에 query를 보내고, Root 서버는 자신의 서버에 없으면 해당 TLD 서버에 요청한다. 이렇게 재귀적으로 실제 도메인 정보를 가지고 있는 서버까지 query가 이동하여 IP 주소를 얻는 방법이다. 재귀적인 방법은 Root 서버에 너무 큰 부담을 준다는 단점이 있다.

<aside>
💡 실제 DNS 서버는 반복과 재귀적인 방식을 함께 사용하며 Local DNS 서버에는 재귀, Root와 TLD 서버에는 반복, Authoritative 서버에는 재귀/반복적 query를 사용한다.

</aside>
