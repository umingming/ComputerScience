# Rest API

### ⚙️Rest

Representational State Transfer

<aside>
💡 a way of providing interoperability between computer system on the Internet
**컴퓨터 시스템의 상호 연관성?**

</aside>

### ⚙️Web(1991)

Q: 어떻게 인터넷에서 정보를 공유할 것인가? 

A: 정보들을 하이퍼 텍스트로 연결한다.

- 표현 형식:  HTML
- 식별자: URI
- 전송 방법: HTTP

🙋‍♂️Roy T.Fielding(대학원생임 ㄷ ㄷ)

<aside>
💡 HTTP/1.0 (1994-1996)

어떻게 하면 웹을 망가뜨리지 않고 HTTP를 발전시킬 수 있을까?

A: HTTP Object Model

</aside>

4년 후

<aside>
💡 Rest(1998)
Microsoft Reserach에서 발표

</aside>

그로부터 2년 후

<aside>
💡 Rest(2000) → 오늘날 우리가 아는 Rest

Roy T.Fielding, 박사 논문으로 발표
약 120P 개지루함

</aside>

---

### ⭐️API

API는 컴퓨터나 컴퓨터 프로그램 사이의 연결이다.

**XML-RPC(1998) by Microsoft**

→ SOAP

**Salesforce API(2000.2)**

![Untitled](Rest%20API%20a25d242aa46948a190232ec26c054917/Untitled.png)

ID로 Object 하나 들고오는 코드 ㅋ;

→ 개복잡해서 인기 없었음

4년 후

flickr API (2004. 8)

**SOAP**

![Untitled](Rest%20API%20a25d242aa46948a190232ec26c054917/Untitled%201.png)

**Rest**

![Untitled](Rest%20API%20a25d242aa46948a190232ec26c054917/Untitled%202.png)

짧다 짧어!

이로 인한 사람들의 인식 변화

| SOAP | REST |
| --- | --- |
| 복잡하다 | 단순하다 |
| 규칙 많다 | 규칙 적다 |
| 어렵다 | 쉽다 |

이 변화가 일으켜온 돌풍🌪

![Untitled](Rest%20API%20a25d242aa46948a190232ec26c054917/Untitled%203.png)

(Rest = 거의 에임의 돌풍 엄윤섭 수준)

<aside>
💡 2006 AWS: 우리 API의 사용량의 85%가 Rest임 ㅋ
2010 SalesFoce.com: Rest API 추가할께 ㅠ

</aside>

> 모두 Rest API! 행복한 Rest 세상! 이렇게 끝나면 좋았으나...
> 

<aside>
💡 Roy T.Fileding: “No REST in CMIS”
CMIS(Rest 바인딩을 지원하는 것으로 CMS를 위한 표준)

</aside>

**강력한 예시**

![Untitled](Rest%20API%20a25d242aa46948a190232ec26c054917/Untitled%204.png)

마소: 이게 Rest API다!

![Untitled](Rest%20API%20a25d242aa46948a190232ec26c054917/Untitled%205.png)

로이형:t 응 아니야~(이건 걍 HTTP API임)

<aside>
💡 REST API라는 개념을 창시한 천재가 진짜 개까다로운 사람 이었던거임 ㅋㅋㅋㅋㅋ

</aside>

### 아니 뭐가문제임?

---

### 본론

<aside>
💡 Rest API의 정의: Rest 아키텍처를 따르는 API

Rest = 분산 하이퍼 미디어 시스템(웹 등)을 위한 아키텍쳐 스타일

아키텍쳐 스타일 = 제약 조건의 집합

즉! 제약 조건을 모두 지켜야 REST API가 됨 그 제약조건은 다음과 같다.

</aside>

![Untitled](Rest%20API%20a25d242aa46948a190232ec26c054917/Untitled%206.png)

- 클라이언트 서버로 되어있음
- 무상태(서버는 아무것도 기억하지 않음)
- 캐시에 태움
- 유니폼 인터페이스(후술)
- 레이어 시스템으로 되어있음
- 서버가 클라이언트에 뭘 보내면 클라이언트가 알아먹는다(자바스크립트)

![Untitled](Rest%20API%20a25d242aa46948a190232ec26c054917/Untitled%207.png)

- 리소스가 URI로 식별되면 된다
- 리소스를 만들거나 CURD할 때 HTTP메세지에 표현을 담아서 발송해야한다.
- **메세지는 스스로를 설명해야한다(ㅈㄴ 까다로움;)**

![Untitled](Rest%20API%20a25d242aa46948a190232ec26c054917/Untitled%208.png)

- 이 HTTP 요청 메세지는 뭔가 빠져있어서 Self-descriptive하지 못하다
    
    목적지가 빠져있음. 
    
    ![Untitled](Rest%20API%20a25d242aa46948a190232ec26c054917/Untitled%209.png)
    
- 어플리케이션의 상태는 Hyperlink를 이용해 형성 전이를 해야한다.

---

## 왜 Uniform Interface인가

### 독립적 진화

- 서버와 클라이언트가 각각 독립적으로 진화한다
- 서버의 기능이 변경되어도 클라이언트를 업데이트 할 수 없다.
- Rest를 만들게 된 계기 = 웹을 안망가뜨리고 HTTP를 어떻게 진화시키지?!

REST를 잘 지키고 있는 사례

![Untitled](Rest%20API%20a25d242aa46948a190232ec26c054917/Untitled%2010.png)

<aside>
💡 결론: Rest API는 Rest를 지키는 API다
지키기 개어렵다.

</aside>