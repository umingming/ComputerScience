# Ajax 동작 원리

## Ajax 동작 원리

                                                                                                                                                        22/10/16

📎 **Ajax 구성 요소**

- Ajax는 기존에 사용되던 여러 기술을 함께 사용하여, 웹 페이지의 일부분만을 갱신할 수 있도록 해주는 개발 기법입니다.
- 이러한 Ajax에서 사용하는 기존 기술은 다음과 같습니다.
    - 웹 페이지의 표현을 위한 HTML과 CSS
    - 데이터에 접근하거나 화면 구성을 동적으로 조작하기 위해 사용되는 DOM 모델
    - 데이터의 교환을 위한 JSON이나 XML
    - 웹 서버와의 비동기식 통신을 위한 XMLHttpRequest 객체
    - 위에서 언급한 모든 기술을 결합하여 사용자의 작업 흐름을 제어하는 데 사용되는 자바스크립트

📎 **Ajax 동작 원리**

- Ajax의 동작은 위에서 언급한 Ajax 구성 요소들을 사용하여 이루어집니다.
- Ajax를 이용한 웹 응용 프로그램은 자바스크립트 코드를 통해 웹 서버와 통신을 하게 됩니다.
- 따라서 사용자의 동작에는 영향을 주지 않으면서도 백그라운드에서 지속해서 서버와 통신할 수 있습니다.
- 다음 그림은 Ajax를 이용한 웹 응용 프로그램과 기존의 웹 응용 프로그램의 동작 원리를 간략히 보여주고 있습니다.

![Untitled](Ajax%20%E1%84%83%E1%85%A9%E1%86%BC%E1%84%8C%E1%85%A1%E1%86%A8%20%E1%84%8B%E1%85%AF%E1%86%AB%E1%84%85%E1%85%B5%20bb0d504ee78d4e288014b5b3beb7d7d9/Untitled.png)

왼쪽 그림의 <Ajax를 이용한 웹 응용 프로그램의 동작 원리>는 다음과 같은 순서로 진행됩니다.

① : 사용자에 의한 요청 이벤트가 발생합니다.

② : 요청 이벤트가 발생하면 이벤트 핸들러에 의해 자바스크립트가 호출됩니다.

③ : 자바스크립트는 XMLHttpRequest 객체를 사용하여 서버로 요청을 보냅니다

- 이때 웹 브라우저는 요청을 보내고 나서, 서버의 응답을 기다릴 필요 없이 다른 작업을 처리할 수 있습니다.

④ : 서버는 전달받은 XMLHttpRequest 객체를 가지고 Ajax 요청을 처리합니다.

⑤와 ⑥ : 서버는 처리한 결과를 HTML, XML 또는 JSON 형태의 데이터로 웹 브라우저에 전달합니다.

- 이때 전달되는 응답은 새로운 페이지를 전부 보내는 것이 아니라 필요한 데이터만을 전달합니다.

⑦ : 서버로부터 전달받은 데이터를 가지고 웹 페이지의 일부분만을 갱신하는 자바스크립트를 호출합니다.

⑧ : 결과적으로 웹 페이지의 일부분만이 다시 로딩되어 표시됩니다.

## DOM

                                                                                                                                                        22/10/16

📎 **문서 객체 모델(DOM)이란?**

- 문서 객체 모델(DOM, Document Object Model)은 HTML 문서나 XML 문서에 접근하기 위한 일종의 인터페이스입니다.
- 이 모델은 문서 내의 모든 요소의 목적과 특징을 정의하고, 각각의 요소에 접근하는 방법을 제공합니다.

![Untitled](Ajax%20%E1%84%83%E1%85%A9%E1%86%BC%E1%84%8C%E1%85%A1%E1%86%A8%20%E1%84%8B%E1%85%AF%E1%86%AB%E1%84%85%E1%85%B5%20bb0d504ee78d4e288014b5b3beb7d7d9/Untitled%201.png)

- Ajax에서는 이러한 DOM을 이용하여 웹 페이지의 일부 요소만을 변경할 수 있습니다.
- 따라서 Ajax를 배우기 전에 DOM에 대한 기본적인 사항을 알아야만 합니다.

📎 **DOM 의 요소 선택**

- 자바스크립트로 DOM 요소를 다루기 위해서는 우선 해당 요소를 선택해야만 합니다.
- DOM 요소를 선택하는 방법은 다음과 같습니다.
    1. 태그 이름(tag name)을 이용한 선택
    2. 아이디(id)를 이용한 선택
    3. 클래스(class)를 이용한 선택
    4. CSS 선택자(selector)를 이용한 선택
    5. HTML 객체 집합(object collection)을 이용한 선택
    

📎 **DOM의 요소의 내용 변경**

- DOM을 이용하면 DOM 요소의 내용(content)이나 속성값 등을 손쉽게 변경할 수 있습니다.
- DOM 요소의 내용을 바꾸는 가장 쉬운 방법은 innerHTML 프로퍼티를 이용하는 것입니다.
- 또한, DOM 요소의 속성 이름을 이용하면 속성값을 바로 변경할 수도 있습니다.
- DOM 요소의 선택 및 내용 변경에 대한 더 자세한 사항은 자바스크립트 DOM 요소 수업에서 확인할 수 있습니다.

## **XMLHttpRequest 객체**

                                                                                                                                                        22/10/16

📎 **XMLHttpRequest 객체**

- Ajax의 가장 핵심적인 구성 요소는 바로 XMLHttpRequest 객체입니다.
- Ajax에서 XMLHttpRequest 객체는 웹 브라우저가 서버와 데이터를 교환할 때 사용됩니다.
- 웹 브라우저가 백그라운드에서 계속해서 서버와 통신할 수 있는 것은 바로 이 객체를 사용하기 때문입니다.

📎 **XMLHttpRequest 객체의 역사**

- 비동기식 통신 방식인 XMLHttp는 가장 처음으로 익스플로러 5 버전에서 ActiveXObject라는 객체를 사용하여 구현됩니다.
- 그 후에 모질라와 사파리에서 XMLHttpRequest라는 이름으로 도입하여 널리 사용되기 시작합니다.
- 초기의 XMLHttpRequest 객체는 W3C 표준이 아니었기 때문에 웹 브라우저마다 구현상의 차이가 존재했습니다.
- 하지만 익스플로러도 7 버전부터 XMLHttpRequest 객체를 기본적으로 지원하게 되며, W3C 표준으로도 제정되게 됩니다.
- 따라서 현재 대부분의 웹 브라우저는 모두 비슷한 구현 방식으로 XMLHttpRequest 객체를 사용하고 있습니다.

📎 **XMLHttpRequest 객체의 생성**

- 현재 대부분의 주요 웹 브라우저는 XMLHttpRequest 객체를 내장하고 있습니다.
- 이러한 XMLHttpRequest 객체를 생성하는 방법은 브라우저의 종류에 따라 다음과 같이 나눠집니다.
    1. XMLHttpRequest 객체를 이용한 방법
    2. ActiveXObject 객체를 이용한 방법
- 익스플로러 7과 그 이상의 버전, 크롬, 파이어폭스, 사파리, 오페라에서는 XMLHttpRequest 객체를 사용합니다.

```jsx
var 변수이름 = new XMLHttpRequest();
```

- 하지만 익스플로러의 구형 버전인 5와 6 버전에서는 ActiveXObject 객체를 사용해야 합니다.

```jsx
var 변수이름 = new ActiveXObject("Microsoft.XMLHTTP");
```

- 따라서 모든 웹 브라우저에서 XMLHttpRequest 인스턴스를 제대로 생성하기 위해서는 다음과 같이 작성해야 합니다.

```jsx
var httpRequest;

function createRequest() {

    if (window.XMLHttpRequest) { // 익스플로러 7과 그 이상의 버전, 크롬, 파이어폭스, 사파리, 오페라 등

        return new XMLHttpRequest();

    } else {                     // 익스플로러 6과 그 이하의 버전

        return new ActiveXObject("Microsoft.XMLHTTP");

    }

}
```

- 근데 이건 아주 옛날꺼, 지금은 그냥 간단히 만들 수 있음

```jsx
var httpRequest = new XMLHttpRequest();
```

## 서버에 요청하기

                                                                                                                                                        22/10/16

📎 **서버에 요청(request)하기**

- Ajax에서는 XMLHttpRequest 객체를 사용하여 서버와 데이터를 교환합니다.
- 따라서 서버에 요청을 보내기 위해서는 우선 XMLHttpRequest 인스턴스를 생성해야 합니다.
- XMLHttpRequest 인스턴스의 open() 메소드와 send() 메소드를 사용하여 요청을 보낼 수 있습니다.

📎 open() 메소드

- open() 메소드는 서버로 보낼 Ajax 요청의 형식을 설정합니다.

```jsx
open(전달방식, URL주소, 동기여부);
```

- 전달 방식은 요청을 전달할 방식으로 GET 방식과 POST 방식 중 하나를 선택할 수 있습니다.
- URL 주소는 요청을 처리할 서버의 파일 주소를 전달합니다.
- 동기 여부는 요청을 동기식으로 전달할지 비동기식으로 전달할지를 전달합니다.

📎 send() 메소드

- send() 메소드는 작성된 Ajax 요청을 서버로 전달합니다.
- 이 메소드는 전달 방식에 따라 인수를 가질 수도 안 가질 수도 있습니다.

```jsx
send();       // GET 방식

send(문자열); // POST 방식
```

📎 GET 방식과 POST 방식

- GET 방식은 주소에 데이터(data)를 추가하여 전달하는 방식입니다.
- GET 방식의 HTTP 요청은 브라우저에 의해 캐시되어(cached) 저장됩니다.
- 또한, GET 방식은 보통 쿼리 문자열(query string)에 포함되어 전송되므로, 길이의 제한이 있습니다.
- 따라서 보안상 취약점이 존재하므로, 중요한 데이터는 POST 방식을 사용하여 요청하는 것이 좋습니다.
- POST 방식은 데이터(data)를 별도로 첨부하여 전달하는 방식입니다.
- POST 방식의 HTTP 요청은 브라우저에 의해 캐시되지 않으므로, 브라우저 히스토리에도 남지 않습니다.
- 또한, POST 방식의 HTTP 요청에 의한 데이터는 쿼리 문자열과는 별도로 전송됩니다.
- 따라서 데이터의 길이에 대한 제한도 없으며, GET 방식보다 보안성이 높습니다.

<aside>
💡 Ajax에서는 주로 GET 방식보다는 POST 방식을 사용하여 요청을 전송합니다.

</aside>

📎 **GET 방식으로 요청하기**

- Ajax에서는 서버에 GET 방식의 요청을 보내기 위해서 다음과 같이 작성합니다.
- 이때 서버로 전송하고자 하는 데이터는 URI에 포함되어 전송됩니다.

```jsx
// GET 방식으로 요청을 보내면서 데이터를 동시에 전달함.

httpRequest.open("GET", "/examples/media/request_ajax.php?city=Seoul&zipcode=06141", true);

httpRequest.send();
```

- 위의 예제에서 사용된 다음 코드로 XMLXttpRequest 객체의 현재 상태와 서버 상의 문서 존재 유무를 확인할 수 있습니다.

```jsx
if (httpRequest.readyState == XMLHttpRequest.DONE && httpRequest.status == 200 ) {

    ...

}
```

- 위의 예제에서 readyState 프로퍼티의 값이 XMLHttpRequest.DONE이면, 서버에 요청한 데이터의 처리가 완료되어 응답할 준비가 완료되었다는 의미입니다.
- 또한, status 프로퍼티의 값이 200이면, 요청한 문서가 서버 상에 존재한다는 의미입니다.

- readyState 프로퍼티와 status 프로퍼티에 대한 더 자세한 사항은 AJAX 서버로부터의 응답 수업에서 확인할 수 있습니다.

아 내용 왜이렇게 많아

📎 **POST 방식으로 요청하기**

- Ajax에서는 서버에 POST 방식의 요청을 보내기 위해서 다음과 같이 작성합니다.
- 이때 서버로 전송하고자 하는 데이터는 HTTP 헤더에 포함되어 전송됩니다.
- 따라서 setRequestHeader() 메소드를 이용하여 먼저 헤더를 작성한 후에, send() 메소드로 데이터를 전송하게 됩니다.

```jsx
// POST 방식의 요청은 데이터를 Http 헤더에 포함시켜 전송함.

httpRequest.open("POST", "/examples/media/request_ajax.php", true);

httpRequest.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");

httpRequest.send("city=Seoul&zipcode=06141");
```

jQuery를 별로 좋아하지 않지만 아직 순수 자바스크립트는 Ajax를 쓰기에 불편함이 많다 (코드가 지저분하다)

## 제이 쿼리와의 환상의 짝짝궁

                                                                                                                                                        22/10/16

📎 제이쿼리와 Ajax

- Ajax를 이용하여 개발을 손쉽게 할 수 있도록 미리 여러 가지 기능을 포함해 놓은 개발 환경을 Ajax 프레임워크라고 합니다.
- 그중에서도 현재 가장 널리 사용되고 있는 Ajax 프레임워크는 바로 제이쿼리(jQuery)입니다.

📎 $.ajax() 메소드

- 제이쿼리는 Ajax와 관련된 다양하고도 편리한 메소드를 많이 제공하고 있습니다.
- 그중에서도 $.ajax() 메소드는 모든 제이쿼리 Ajax 메소드의 핵심이 되는 메소드입니다.
- $.ajax() 메소드는 HTTP 요청을 만드는 강력하고도 직관적인 방법을 제공합니다.
- $.ajax() 메소드의 원형은 다음과 같습니다.

```jsx
$.ajax([옵션])
```

- URL 주소는 클라이언트가 HTTP 요청을 보낼 서버의 주소입니다.
- 옵션은 HTTP 요청을 구성하는 키와 값의 쌍으로 구성되는 헤더의 집합입니다.
- 다음 예제는 $.ajax() 메소드에서 사용할 수 있는 대표적인 옵션을 설명하는 예제입니다.

```jsx
$.ajax({

    url: "/examples/media/request_ajax.php", // 클라이언트가 요청을 보낼 서버의 URL 주소

    data: { name: "홍길동" },                // HTTP 요청과 함께 서버로 보낼 데이터

    type: "GET",                             // HTTP 요청 방식(GET, POST)

    dataType: "json"                         // 서버에서 보내줄 데이터의 타입

})

// HTTP 요청이 성공하면 요청한 데이터가 done() 메소드로 전달됨.

.done(function(json) {

    $("<h1>").text(json.title).appendTo("body");

    $("<div class=\"content\">").html(json.html).appendTo("body");

})

// HTTP 요청이 실패하면 오류와 상태에 관한 정보가 fail() 메소드로 전달됨.

.fail(function(xhr, status, errorThrown) {

    $("#text").html("오류가 발생했습니다.<br>")

    .append("오류명: " + errorThrown + "<br>")

    .append("상태: " + status);

})

// HTTP 요청이 성공하거나 실패하는 것에 상관없이 언제나 always() 메소드가 실행됨.

.always(function(xhr, status) {

    $("#text").html("요청이 완료되었습니다!");

});
```

- 다음 예제는 $.ajax() 메소드의 동작을 보여주는 간단한 예제입니다.

```jsx
$(function() {

    $("#requestBtn").on("click", function() {

        $.ajax("/examples/media/request_ajax.php")

        .done(function() {

            alert("요청 성공");

        })

        .fail(function() {

            alert("요청 실패");

        })

        .always(function() {

            alert("요청 완료");

        });

    });

});
```

📎 **Ajax 메소드**

![Untitled](Ajax%20%E1%84%83%E1%85%A9%E1%86%BC%E1%84%8C%E1%85%A1%E1%86%A8%20%E1%84%8B%E1%85%AF%E1%86%AB%E1%84%85%E1%85%B5%20bb0d504ee78d4e288014b5b3beb7d7d9/Untitled%202.png)

## 자바 스크립트의 DOM 요소 핸들링(부록)

                                                                                                                                                        22/10/16

📎 HTML 태그 이름(tag name)을 이용한 선택

- getElementsByTagName() 메소드는 HTML 태그 이름을 이용하여 HTML 요소를 선택합니다.

```jsx
var selectedItem = document.getElementsByTagName("li"); // 모든 <li> 요소를 선택함.

for (var i = 0; i < selectedItem.length; i++) {

    selectedItem.item(i).style.color = "red"; // 선택된 모든 요소의 텍스트 색상을 변경함.

}
```

- item() 메소드는 해당 HTML 객체 집합(obejct collection)에서 전달받은 인덱스에 해당하는 요소를 반환합니다.
- HTML 요소의 style 프로퍼티를 이용하면, 해당 요소의 CSS 스타일을 변경할 수 있습니다.

📎 아이디(id)를 이용한 선택

- getElementById() 메소드는 아이디를 이용하여 HTML 요소를 선택합니다.

```jsx
var selectedItem = document.getElementById("even"); // 아이디가 "even"인 요소를 선택함.

selectedItem.style.color = "red"; // 선택된 요소의 텍스트 색상을 변경함.
```

- 자바스크립트에서 아이디(id)를 이용한 선택은 해당 아이디를 가지고 있는 요소 중에서 첫 번째 요소 단 하나만을 선택합니다.
- 따라서 여러 요소를 선택하고 싶을 때는 태그 이름이나 클래스와 같은 다른 방법을 사용해야 합니다.

📎 클래스(class)를 이용한 선택

- getElementsByClassName() 메소드는 클래스 이름을 이용하여 HTML 요소를 선택합니다.

```jsx
var selectedItem = document.getElementsByClassName("odd"); // 클래스가 "odd"인 모든 요소를 선택함.

for (var i = 0; i < selectedItem.length; i++) {

    selectedItem.item(i).style.color = "red"; // 선택된 모든 요소의 텍스트 색상을 변경함.

}
```

📎 name 속성을 이용한 선택

- getElementByName() 메소드는 HTML 요소의 name 속성을 이용하여 HTML 요소를 선택합니다.

```jsx
var selectedItem = document.getElementsByName("first"); // name 속성값이 "first"인 모든 요소를 선택함.

for (var i = 0; i < selectedItem.length; i++) {

    selectedItem.item(i).style.color = "red"; // 선택된 모든 요소의 텍스트 색상을 변경함.

}
```

📎 CSS 선택자(selector)를 이용한 선택

- querySelectorAll() 메소드는 CSS 선택자(아이디, 클래스, 속성, 속성값 등)를 이용하여 HTML 요소를 선택합니다.

```jsx
var selectedItem = document.querySelectorAll("li.odd"); // 클래스가 "odd"인 요소 중에서 <li> 요소만을 선택함.

for (var i = 0; i < selectedItem.length; i++) {

    selectedItem.item(i).style.color = "red"; // 선택된 모든 요소의 텍스트 색상을 변경함.

}
```

- querySelectorAll() 메소드는 익스플로러 8과 그 이전 버전에서 지원하지 않습니다.

📎 HTML 객체 집합(object collection)을 이용한 선택

- HTML DOM에서 제공하는 객체 집합(object collection)을 이용하여 HTML 요소를 선택할 수 있습니다.

```jsx
var title = document.title; // <title> 요소를 선택함.

document.write(title);
```

📎 **DOM 요소의 내용 변경**

- HTML DOM을 이용하면 HTML 요소의 내용(content)이나 속성값 등을 손쉽게 변경할 수 있습니다.
- HTML 요소의 내용을 변경하는 가장 쉬운 방법은 innerHTML 프로퍼티를 이용하는 것입니다.

```jsx
var str = document.getElementById("text");

str.innerHTML = "이 문장으로 바뀌었습니다!";
```

```jsx
var link = document.getElementById("link");
// 아이디가 "link"인 요소를 선택함.

link.href = "/javascript/intro";
// 해당 요소의 href 속성값을 변경함.

link.innerHTML = "자바스크립트 수업 바로 가기!";
// 해당 요소의 내용을 변경함.
```

📎 **DOM 요소의 스타일 변경**

- HTML DOM을 이용하면 HTML 요소의 스타일(style)도 손쉽게 변경할 수 있습니다.
- style 프로퍼티를 이용하여 HTML 요소에 CSS 스타일을 적용합니다.

```jsx
var str = document.getElementById("text");
// 아이디가 "text"인 요소를 선택함.

function changeRedColor() { str.style.color = "red"; }
// 해당 요소의 글자색을 빨간색으로 변경함.

function changeBlackColor() { str.style.color = "black"; }
// 해당 요소의 글자색을 검정색으로 변경함.
```