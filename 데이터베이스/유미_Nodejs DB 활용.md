# Node.js DB 활용

## MongoDB

23/04/30

📎 호스팅 받기

- database → connect → drivers
    
    ![Untitled](Node%20js%20DB%20%E1%84%92%E1%85%AA%E1%86%AF%E1%84%8B%E1%85%AD%E1%86%BC%202277ebbba0bf40ed904e44fbc3a7af58/Untitled.png)
    
- driver가 Node.js로 설정된 것 확인
    
    ![Untitled](Node%20js%20DB%20%E1%84%92%E1%85%AA%E1%86%AF%E1%84%8B%E1%85%AD%E1%86%BC%202277ebbba0bf40ed904e44fbc3a7af58/Untitled%201.png)
    
- connection code 받을 수 있음.
    
    ```jsx
    mongodb+srv://u13040035:<password>@cluster0.rrl2jwu.mongodb.net/?retryWrites=true&w=majority
    ```
    

📎 db 접속

- mongodb 라이브러리 설치
    
    ```bash
    npm i mongodb@3.6.4
    ```
    
- server.js mongoclient 등록
    
    ```jsx
    const MongoClient = require("mongodb").MongoClient;
    ```
    
- 접속 URL을 인자로 사용해 연결 후 정상적으로 db에 접속하면 서버 실행시키도록 코드 추가
    - password는 database access에서 설정하면 됨.
    
    ```jsx
    MongoClient.connect(
        "mongodb+srv://u13040035:java1234@cluster0.rrl2jwu.mongodb.net/?retryWrites=true&w=majority",
    		{ useUnifiedTopology: true }, //워닝메세지 제거
        function (err, client) {
            app.listen(8080, () => {
                console.log(client);
            });
        }
    );
    ```
    

📎 자료 저장을 위한 폴더 생성

- database → collections → create database
    
    ![Untitled](Node%20js%20DB%20%E1%84%92%E1%85%AA%E1%86%AF%E1%84%8B%E1%85%AD%E1%86%BC%202277ebbba0bf40ed904e44fbc3a7af58/Untitled%202.png)
    
- database와 하위의 collection 추가

📎 db 통신

- 페이지 전체에서 사용할 전역 변수 선언
    
    ```jsx
    var db
    ```
    
- db(database): database에 접속
    
    ```jsx
    db = client.db("todoapp");
    ```
    
- collection().insertOne(): 원하는 자료 추가
    
    ```jsx
    db.collection("post").insertOne( { ... }, () => {
    });
    ```
    

## ejs

📎 ejs 사용

- server.js에 코드 추가
    
    ```jsx
    app.set("view engine", "ejs");
    ```
    
- views 폴더 하위에 list.ejs 파일 생성

📎 기본 문법

- <%= %>: html 중간 중간 서버 데이터 넣고 싶을 때
    
    ```html
    <h2><%= user.name %></h2>
    ```
    
- 자바스크립트 문법 사용 가능
    
    ```html
    <% if (user) { %>
      <h2><%= user.name %></h2>
    <% } %>
    ```
    

📎 db 데이터 보여주기

- collection().find/findOne().toArray(): 모든 데이터를 array 자료형으로 가져옴.
    
    ```jsx
    db.collection("post").find().toArray((err, result) => { ...
    });
    ```
    
- render(): 파일 렌더링과 데이터 전송; toArray의 두 번쨰 인자인 result를 posts라는 이름으로 보내는 것
    
    ```jsx
    res.render("list.ejs", { posts: result });
    ```
    
- esj파일에서 posts 사용
    
    ```html
    <% for (var i = 0; i < posts.length; i++) { %>
        <% if (!posts[i].title) continue; %>
        <li>
            <h4>할 일 : <%= posts[i].title %></h4>
            <p>마감 : <%= posts[i].date %></p>
        </li>
    <% } %>
    ```
    

## CRUD

📎 _id

- mongodb에 데이터 저장 시, 꼭 넣어야 하는 값. 안 넣으면 ObjectId()로 강제 아이디 부여
- couter라는 컬렉션에서 관리하면 용이함.
    
    ![Untitled](Node%20js%20DB%20%E1%84%92%E1%85%AA%E1%86%AF%E1%84%8B%E1%85%AD%E1%86%BC%202277ebbba0bf40ed904e44fbc3a7af58/Untitled%203.png)
    

📎 Create

- findOne()으로 id로 사용할 데이터 가져 옴.
    
    ```jsx
    db.collection("counter").findOne({ name: "게시물갯수" }, (err, result) => {
    	  const { totalPost } = result;
    		const data = {
    	          _id: totalPost,
    	          title: req.body.title,
    	          date: req.body.date,
    	  };
    }
    ```
    
- insertOne(): 데이터 추가
    
    ```jsx
    db.collection("post").insertOne(data, (err, result) => { ... });
    ```
    
- updateOne() + $set: 해 당다용으로 수정
    
    ```jsx
    db.collection("counter").updateOne(
        { name: "게시물갯수" },
        { $set: { totalPost: totalPost + 1 } },
        (err, result) => {
            console.log(err || result);
        }
    );
    ```
    
- updateOne() + $inc: 해당 데이터를 인자만큼 증가
    
    ```jsx
    db.collection("counter").updateOne(
        { name: "게시물갯수" },
        { $inc: { totalPost: 1 } },
        (err, result) => {
            console.log(err || result);
        }
    );
    ```
    

📎  Delete

- ajax 사용을 위해 jquery 설치
    
    ```jsx
    <script src="https://code.jquery.com/jquery-3.4.1.min.js"></script>
    ```
    
- delete를 위한 기본 문법
    
    ```jsx
    $.ajax({
    	  method : 'DELETE',
    	  url : '/delete',
    	  data : '1번게시물'
    }).done(function(결과){
    	  AJAX 성공시 실행할 코드는 여기
    }).fail(function(에러){
    	  실패시 실행할 코드는 여기
    });
    ```
    
- id를 버튼의 dataset으로 저장
    
    ```jsx
    <button class="delete" data-id="<%= posts[i]._id %>">삭제</button>
    ```
    
- 클릭한 버튼의 id 정의
    
    ```jsx
    $('.delete').click(function(e) {
          const _id = e.target.dataset.id;
          $.ajax({
              method: "DELETE",
              url: '/delete',
              data: { _id }
          })
    ```
    
- 숫자로 보내도 문자로 가므로, 서버에서 변환해줘야 함.
    
    ```jsx
    app.delete("/delete", (req, res) => {
        const _id = +req.body._id;
        db.collection("post").deleteOne({ _id }, (err, result) => { ... });
    });
    ```
    

📎  새로고침 처리

- 버튼 클릭 시 this를 변수에 할당함. 여기서 화살표 함수 쓰면 this가 버튼이 아닌, window로 지정
    
    ```jsx
    $('.delete').click(function(e) {
        const $button = $(this);
    		...
    }
    ```
    
- fadeOut(): 요소를 서서히 사라지게 함. 해당 버튼의 부모 요소를 지우기
    - parent(tag).fadeOut(): 부모 요소 중 tag가 있으면, 사라지게 함.
    
    ```jsx
    $button.parent('li').fadeOut();
    ```
    

📎 인자 사용

- url에 :기호를 붙여 인자를 표기
    
    ```jsx
    app.get("/detail/:id", (req, res) => { ... });
    ```
    
- 파라미터로 id 값을 설정해, 데이터 찾을 수 있음.
    
    ```jsx
    db.collection("post").findOne({ _id: +req.params.id }, (err, result) => {
        console.log(err || result);
        res.render("detail.ejs", { data: result });
    });
    ```
    

📎 수정하기

- post 방식; 파라미터를 통해 undateOne 쿼리 날리기
    
    ```jsx
    app.post("/edit/:id", function (req, res) {
        db.collection("post").updateOne(
            { _id: +req.params.id },
            { $set: { title: req.body.title, date: req.body.date } },
            (err, result) => {
                console.log(err || result);
            }
        );
    });
    ```
    
- form 태그의 메소드는 POST, GET만 가능함. 기타 방식 사용하려면 method-override 설치 필요
    
    ```bash
    npm i method-override
    ```
    
- method-override 등록
    
    ```jsx
    const methodOverride = require("method-override");
    app.use(methodOverride("_method"));
    ```
    
- put도 post와 마찬가지로 사용한다.
    
    ```jsx
    app.put("/edit/:id", (req, res) => {
        db.collection("post").updateOne(
            { _id: +req.params.id },
            { $set: { title: req.body.title, date: req.body.date } },
            (err, result) => {
                res.redirect("/list");
            }
        );
    });
    ```