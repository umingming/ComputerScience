# Axios

## Axios란?

22/09/04

📎 Axios

- 브라우저, Node.js를 위해 Promise API를 활용하는 HTTP **비동기** 통신 라이브러리
- 통신을 쉽게 하기 위해 Ajax와 더불어 사용함.

📎 Axios

- 써드파티 라이브러리로 설치 필요
- data 속성 사용하며, object 포함
- status가 200, statusText가 OK면 성공
- 자동으로 JSON 형식 변환
- 요청 취소 및 타임아웃 걸기
- HTTP 요청 가로 채기
- 다운로드 진행 지원

📎 fetch

- 설치 필요 없음
- body 속성 이용하며, 문자열화
- 응답객체가 ok 속성 포함하면 성공
- .json() 메서드 사용
- 요청 취소 **X**
- HTTP 요청 가로 채기 **X**
- 다운로드 진행 지원 **X**

📎 Axios 설치

- 서버에서 설치; npm
    
    ```bash
    npm install --save axios
    ```
    
- 클라이언트에서 설치; cdn
    
    ```html
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    ```
    

## Axios 문법

📎 Axios 문법 구성

```jsx
axios({
  url: 'https://test/api/cafe/list/today',
  method: 'post',
  data: {
    foo: 'diary'
  }
});
```

- url; 서버 주소
- method; 요청 방식
- data; 요청 방식이 put, post, patch의 경우 body에 보내는 데이터
- headers; 요청 헤더
- params; URL 파라미터
- responseType; 서버가 응답해주는 데이터 타입 지정
- withCredentials; cross-site access-control 요청을 허용 유무

📎 get

- 단순 데이터 요청을 수행할 경우
    
    ```jsx
    axios.get('/user?ID=12345')
      .then(function (response) {
        console.log(response);
      })
      .catch(function (error) {
        console.log(error);
      })
      .finally(function () {
      });
    ```
    
- 파라미터 데이터를 포함시키는 경우
    
    ```jsx
    axios.get('/user', {
        params: {
          ID: 12345
        }
      })
      .then(function (response) {
        console.log(response);
      })
      .catch(function (error) {
        console.log(error);
      })
      .finally(function () {
      });
    ```
    

📎 post

- 데이터를 Message Body에 포함시켜 보냄.
- get 메서드에서 params를 사용한 경우와 비슷
    
    ```jsx
    axios.post("url", {
    		firstName: 'Fred',
    		lastName: 'Flintstone'
      })
      .then(function (response) {
        console.log(response);
      }).catch(function (error) {
        console.log(error);
      })
    ```
    

📎 put

- REST API DB에 저장되어 있는 내용 갱신하는 목적으로 사용
- 서버에 있는 데이터베이스의 내용을 변경하는 것을 주 목적으로 하며, 내부적으로 get→post 과정을 거치기 때문에 post 메서드와 비슷
    
    ```jsx
    axios.put("url", {
        username: "",
        password: ""
      })
      .then(function (response) {
        console.log(response);
      }).catch(function (error) {
        console.log(error);
      })
    ```
    

📎 delete

- REST API에서 DB에 저장된 내용을 삭제하는 목적으로 사용되며 일반적으로 body가 비어있음.
    
    ```jsx
    axios.delete('/user?ID=12345')
      .then(function (response) {
        console.log(response);
      })
      .catch(function (error) {
        console.log(error);
      })
    ```
    
- 헤더에 많은 정보를 담을 수 없을 때는, 두 번째 인자에 data 추가
    
    ```jsx
    axios.delete('/user?ID=12345',{
        data: {
          post_id: 1,
          comment_id: 13,
          username: "foo"
        }
      })
      .then(function (response) {
        console.log(response);
      })
      .catch(function (error) {
        console.log(error);
      })
    ```