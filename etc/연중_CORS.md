# 주제: CORS (교차 출처 리소스 공유)
### CORS(Cross-Origin Resource Sharing) - 교차 출처 리소스 공유
사용자가 최초 접근한 웹 애플리케이션의 출처 외에 다른 출처에서 리소스를 가져오도록 허용하는 정책 또는 체제

<br>
<br>

### SOP(Same-Origin Policy) - 동일 출처 정책
어떤 출처에서 불러온 문서나 스크립트가 다른 출처에서 가져온 리소스와 상호작용하는 것을 제한하는 보안방식/모델

<br>
<br>

## Origin이 뭔데요?
### Origin - 출처
```
origin: <scheme> "://" <hostname> [ ":" <port> ]
```
`<scheme>`: 사용하는 프로토콜. 일반적으로 HTTP 프로토콜 혹은 보안 버전인 HTTPS를 사용  
`<hostname>`: 서버(가상 호스팅)의 이름 또는 IP  
`<port> (Optional)`:  서버와 연결을 맺기 위한 TCP 포트 번호. 포트번호를 입력하지 않으면, 요청한 서비스의 기본 포트(HTTP의 경우 "80")를 사용  

__즉, 우리가 아는 URL에서 포트번호, 혹은 (포트번호가 생략됐다면)호스트네임까지를 출처(Origin)라고 칭함__

Ex) `https://localhost:1234/search?query=origin#info` 

<br>

### 어? 그럼 CORS랑 SOP는 서로 허용하고 제한하는 반대되는 개념인가?
ㅇㅇ SOP는 보안의 이유로 다른 출처에서 리소스를 가져오는 것을 제한하고 CORS는 이를 허용하는 것.  
SOP가 베이스로 깔려있고, 웹 생태계에서 다른 출처에서 리소스를 가져온다는 것은 흔한 일이니 이를 전부 막는다? 있을 수 없음.  
때문에 CORS라는 예외 정책을 만들어서 CORS에 부합하는 것은 허용하자 이렇게 되버린 것.  


<br>

### 같은 출처, 다른 출처의 기준 - Origin이 같아야함  
아래 표는 예시 URL http://store.company.com/dir/page.html의 출처를 비교한 예시.

|URL |	결과 | 이유|
|-----------------------------------------------|----|-----|
http://store.company.com/dir2/other.html | 성공	| 경로만 다름
http://store.company.com/dir/inner/another.html	| 성공 | 경로만 다름
https://store.company.com/secure.html | 실패 | 프로토콜 다름
http://store.company.com:81/dir/etc.html | 실패 | 포트 다름 (http://는 80이 기본값)
http://news.company.com/dir/other.html | 실패 | 호스트 다름

<br>
<br>

## CORS 작동 시나리오 3가지
### CORS의 작동방식 - 일반적 요청
1. 기존 출처에서 다른 출처의 리소스를 요청(HTTP)한다.
2. 브라우저는 요청할 때, http 헤더 내에 `origin` 속성 값에 기존 출처를 담아서 보낸다.
3. 요청을 받은 서버는 `Access-Control-Allow-Origin` 속성 값에 '이 리소스를 접근하는 것이 허용된 출처' 값을 넣어서 응답한다.
4. 다른 출처의 응답을 받은 브라우저는 `origin`과 `Access-Control-Allow-Origin`의 값을 비교하여 허용할지 말지를 결정한다.

<br>

### 일반적인 요청은 3가지 조건을 만족해야 보낼 수 있다.  
1) GET, POST, HEAD 메소드를 사용한 요청  
2) 유저 에이전트가 자동으로 설정 한 헤더외에, 수동으로 설정할 수 있는 헤더는 아래와 같다.  
  Accept  
  Accept-Language  
  Content-Language  
  Content-Type  
3) Content-Type 헤더를 사용할 경우, 아래와 같은 값만 가능하다.  
  application/x-www-form-urlencoded  
  multipart/form-data  
  text/plain  

<br>

상당히 조건이 껄그럽기 때문에 일반적인 요청으로 보내는 경우는 많지 않다.  
때문에 아래의 예비요청을 사용하는 경우가 많다.  

<br>

### CORS의 작동방식 - 예비요청(Preflight Request)
1. 기존 출처에서 OPTION 메소드를 통해 다른 출처의 리소스에 예비요청(Preflight Request)을 날린다.
2. 서버는 브라우저가 예비요청에 대한 응답을 통해 CORS 허용 근거를 판단할 수 있는 정보를 담아서 응답한다. `Access-Control-Allow-Origin` 같은거
3. 예비요청의 응답을 받은 브라우저는 해당 예비요청이 CORS 정책에 유효한지 판단한다.
4. 유효한 경우, 리소스를 포함한 각종 정보를 요청하고 서버는 응답한다.

예비요청은 3가지 조건만 만족하면 생략가능하다. (일반적인 요청)

<br>

### CORS의 작동방식 - 인증정보를 포함한 요청(보안을 강화한 요청)
원래 일반적인 fetch API나 XMLHttpRequest의 경우, 따로 쿠키나 인증관련 헤더를 담지 않는다.  
그러나, credentials 옵션을 사용하여 쿠키나 인증관련 헤더를 담을 수 있다.  
해당 옵션을 사용하여 추가 정보를 담게 되면 다른 출처에 요청을 보낼 때, 추가된 다른 조건을 추가 검사한다.  

해당 옵션 값은 3가지가 있다.  
|옵션 값|설명|
|------------------|--------------------|
|same-origin (기본값)|같은 출처 간 요청에만 인증 정보를 담을 수 있다|
|include|모든 요청에 인증 정보를 담을 수 있다|
|omit|모든 요청에 인증 정보를 담지 않는다|


<br>
<br>
<br>
<br>






















## [출처] 
https://developer.mozilla.org/ko/docs/Web/HTTP/Headers/Origin
https://ko.wikipedia.org/wiki/%EA%B5%90%EC%B0%A8_%EC%B6%9C%EC%B2%98_%EB%A6%AC%EC%86%8C%EC%8A%A4_%EA%B3%B5%EC%9C%A0
