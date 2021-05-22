---
layout: post
title: 2021-05-22 cloneCoding(2주차)
category: cloneCoding
permalink: /log/:year/:month/:day/:title/
tags: [클론코딩]
comments: true









---



# 밑바닥부터 배포까지 클론코딩

# 2주차(5/22)

# View engine

## View Engine - Nunjucks

**서버와 브라우저 모두에서 여러 템플릿 언어로 작업하기 쉽게하기 위해 작은 추상화 계층을 제공**

- 브라우저 및 서버 지원
    - 브라우저 지원을 위해서는 **RaptorJS Optimizer** 또는 **browserify** 와 같은 Node.js 모듈 **번 들러를 사용해야함**
- 정규화 된 렌더링 API
- 여러 렌더링 스타일
    - 콜백
    - 스트림
    - 비동기 렌더링
- 혼합 모드 템플릿 렌더링
    - 여러 템플릿 엔진이 동일한 출력 스트림으로 비동기 적으로 렌더링 할 수 있다.
    - 즉, 템플릿 엔진은 이제 서로 잘 어울릴 수 있다.
- 캡슐화
    - 각 뷰 엔진은 템플릿을 해결하고 렌더링하는 특별한 논리를 가질 수 있다.

-**view-engine npm 참고**

전에 하던 **hello-express**에서 이어서 함.

```jsx
npm install nunjucks
```

app.js 를 열고

상단에 한줄 추가

```jsx
const nunjucks = require("nunjucks");
```

```jsx
const app = express();
const port = 3000;
// 이 위치에 하단 부분 추가 작성
nunjucks.configure("template", {
  autoescape: true,
  express: app,
});
// 윗 부분 까지
app.get("/", (req, res) => {
  res.send("hello express");
});
```

- 여기서 autoescape는 **위험한 문자가있는 출력이 자동으로 이스케이프되는지 여부를 제어합니다.**

**routes 와 동일 위치**에 **template 폴더**를 만들고 그 **안에 admin 폴더**를 생성 그 안에 **products.html** 파일 생성

products.html

```html
products
{{ message }}
```

admin.js

```jsx
router.get("/products", (req, res) => {
  res.send("admin products 이후 url");
});
```

이 부분 수정

```jsx
router.get("/products", (req, res) => {
  // res.send("admin products 이후 url");
  res.render("admin/products.html", {
    message: "hello!!!",
  });
});
```

```jsx
npm start
```

잘 실행 되는 것을 확인하고 package.json 열기

package.json

```jsx
"start": "npx nodemon app.js"
```

이 부분을 수정

```jsx
"start": "npx nodemon -e js,html app.js"
```

- 템플릿을 수정하더라도 js,html을 추가해서 감지하도록 추가

그 후 products.html 파일에서

```jsx
products
{{ online }}
```

수정 후

admin.js

```jsx
router.get("/products", (req, res) => {
  // res.send("admin products 이후 url");
  res.render("admin/products.html", {
    message: "hello!!!",
    online: "express",
  });
});
```

추가하고 다시 실행 

**package-lock.json**

express - bodyparser 1.2 

nunjuscks - bodyparser 2.0

bodyparser - 2.0

각각 모듈들의 최적화 버전을 적어놓은 거

## 템플릿 상속

공통 파일(js파일 또는 부트스트랩) 상단에 선언 해두고 필요할 떄마다 가져오는 형식

우선 저번 강의 때 **autoescape** 이거에 대해 설명

products.html

```html
products
{{ message }}
```

admin.js ( message 부분을 태그로 수정 )

```jsx
router.get("/products", (req, res) => {
  // res.send("admin products 이후 url");
  res.render("admin/products.html", {
    message: `<h1>태그가 출력됩니다.</h1>`,
    online: "express",
  });
});
```

![2021-05-22-12](\images\2021-05-22-12.PNG)

이렇게 출력된다.

하지만 app.js에서

```jsx
autoescape: true,
```

이 부분을 false로 수정하면 

```jsx
autoescape: false,
```

![2021-05-22-13](\images\2021-05-22-13.PNG)

이렇게 출력된다.

하지만 저 부분을 화면에 뿌려줘야될 경우에는 위험하지 않다는 것을 해야된다.

products.html

```jsx
products
{{ message | safe }}
```

이렇게 옆에 safe를 써주면 된다.

템플릿 상속 하기전 준비

**template 폴더 안**에 **layout**이라는 폴더 생성 후 그 안에 **base.html** 파일 생성

template/layout/base.html

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css">
  <title>{{ title }}</title>
</head>
<body>
  <div class="container" style="padding-top: 100px;">
    {% block content %}{% endblock %}
  </div>
</body>
</html>
```

template/admin/products.html 내용 수정

```html
{% set title = "관리자 리스트" %}
{% extends "layout/base.html" %}

{% block content -%}
  <table class="table table-bordered table-hover">
    <tr>
      <th>제목</th>
      <th>작성일</th>
      <th>삭제</th>
    </tr>
    <tr>
      <td>제품 이름</td>
      <td>2020-03-07</td>
      <td>
        <a href="#" class="btn btn-danger">삭제</a>
      </td>
    </tr>
  </table>

  <a href="/admin/products/write" class="btn btn-default">작성하기</a>

{% endblock %}
```

이부분은 base.html title에 들어가는 부분

```html
{% set title = "관리자 리스트" %}
```

이부분은 base.html를 불러오겠다.

```html
{% extends "layout/base.html" %}
```

이 부분은 base.html에 들어가는 내용

```html
{% block content -%}
  <table class="table table-bordered table-hover">
    <tr>
      <th>제목</th>
      <th>작성일</th>
      <th>삭제</th>
    </tr>
    <tr>
      <td>제품 이름</td>
      <td>2020-03-07</td>
      <td>
        <a href="#" class="btn btn-danger">삭제</a>
      </td>
    </tr>
  </table>

  <a href="/admin/products/write" class="btn btn-default">작성하기</a>

{% endblock %}
```

실행해보면

![2021-05-22-14](\images\2021-05-22-14.PNG)

## 미들웨어

라우팅을 작성하는데 몇몇 페이지는 로그인을 한 상태로 보여주고싶다. 

그래서 그 부분을 로그인이 안되있으면 로그인페이지로 보낸다.라는 조건을 걸었다.

근데 로그인 페이지 경로가 변경되어 로그인을 한 상태로 보여주고싶다라는 조건문을 매번 모든 곳을 수정할 순 없다. 그래서 미들웨어라는 것을 사용한다.

호출하는데 사용자가 어떤 url을 호출하는지 console에서 확인 할 수 있다. 그것을 morgan이라는 애로 확인하는데

우선 morgan을 설치한다.

```html
npm install morgan
```

그 후 app.js 에 선언 해준다.

```jsx
const logger = require("morgan");
```

하단에 

```jsx
// 미들웨어 셋팅
app.use(logger("dev"));
```

작성해주고 npm start를 한다.

예들 들어 [localhost:3000/admin](http://localhost:3000/admin) 으로 갔을 때

```jsx
GET /admin 304 2.897 ms - -
```

이런식으로 확인할 수 있다.

admin.js에 내용을 추가한다.

```jsx
function testMiddleware(req, res, next) {
  console.log("첫번째 미들웨어");
  next();
}

router.get("/", testMiddleware, (req, res) => {
  res.send("admin 이후 url");
});
```

admin으로 갈때 "/" → testMiddleware, 이런식으로 가서 실행하고 그 다음에 내가 작성한 소스를 보여줘라 라는 식이다.

확인 해보면 

```jsx
Express listening on port 3000
첫번째 미들웨어
GET /admin 304 2.897 ms - -
```

이런식으로 나오게 된다.

우선 순위를 확인해 보면

먼저 app.js에 작성 해본다.

```jsx
function vipmiddleware(req, res, next) {
  console.log("최우선 미들웨어");
  next();
}

app.use("/admin", vipmiddleware, admin);
```

그 후 admin.js에 

```jsx
function testMiddleware(req, res, next) {
  console.log("첫번째 미들웨어");
  next();
}

function testMiddleware2(req, res, next) {
  console.log("두번째 미들웨어");
  next();
}

router.get("/", testMiddleware, testMiddleware2, (req, res) => {
  res.send("admin 이후 url");
});
```

작성 해본다.

실행을 해보면 

```jsx
Express listening on port 3000
최우선 미들웨어
첫번째 미들웨어
두번째 미들웨어
GET /admin 304 4.546 ms - -
```

이렇게 확인해볼 수 있다.

## form( body-parser )

시작하기 전 

**template 폴더**안에 **admin 폴더** 에 **write.html**파일을 생성

template/admin/write.html

```html
{% set title = "제품 등록" %}
{% extends "layout/base.html" %}

{% block content -%}
  <form action="" method="post">
    <table class="table table-bordered">
      <tr>
        <th>제품명</th>
        <td>
          <input type="text" name="name" class="form-control">
        </td>
      </tr>
      <tr>
        <th>가격</th>
        <td>
          <input type="text" name="price" class="form-control">
        </td>
      </tr>
      <tr>
        <th>설명</th>
        <td>
          <input type="text" name="description" class="form-control">
        </td>
      </tr>
    </table>
    <button class="btn btn-primary">작성하기</button>  
  </form>
{% endblock %}
```

이렇게 실행 결과가 나온다.

![2021-05-22-15](\images\2021-05-22-15.PNG)

여기서 아무거나 입력 후 작성하기를 클릭하면

![2021-05-22-16](\images\2021-05-22-16.PNG)

post를 찾을 수 없다고 나온다.

여기서 이제 생각해보면 그동안 router.get만 했었다.

이제 post를 하면된다고 생각이 들었다.

post를 위해서는 이번시간에 배우는 body-parser를 사용하면 되는데

body-parser는 미들웨어이다.

우선 app.js에 선언을 한다.

```jsx
const bodyParser = require("body-parser");
```

여기서 body-parser를 선언하기전에 npm install을 안해도 되는 이유는 

**express의 내장 모듈이기 때문에** 따로 install을 안해도 된다.

하단에 미들웨어 세팅을 해줘야 한다.

```jsx
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: false }));
```

그리고 admin.js에 post를 설정해줘야 한다.

```jsx
router.post("/products/write", (req, res) => {
  res.send("212121");
});
```

실행을 해보면

![2021-05-22-17](\images\2021-05-22-17.PNG)

![2021-05-22-18](\images\2021-05-22-18.PNG)

근데 post로 올때 작성한 제품명으로 확인을 해보고싶을 때는 admin.js에서 아래와 같이 수정을 해본다.

```jsx
router.post("/products/write", (req, res) => {
  res.send(req.body.name);
});
```

실행해보면

![2021-05-22-19](\images\2021-05-22-19.PNG)

![2021-05-22-20](\images\2021-05-22-20.PNG)

이렇게 확인해 볼 수 있다.

또 한번 해보면 이번엔 가격을 받아와 본다.

```jsx
router.post("/products/write", (req, res) => {
  res.send(req.body.price);
});
```

실행 해보면

![2021-05-22-21](\images\2021-05-22-21.PNG)

![2021-05-22-22](\images\2021-05-22-22.PNG)

이렇게 확인해 볼 수 있다.

전체 변수를 다 받아보고 싶다면

```jsx
router.post("/products/write", (req, res) => {
  res.send(req.body);
});
```

![2021-05-22-23](\images\2021-05-22-23.PNG)

![2021-05-22-24](\images\2021-05-22-24.PNG)

이렇게 확인해 볼 수 있다.

나중에 URL을 만들 때

REST API를 사용해서 url을 보기좋게 할거다.

**GET /users** ⇒ 모든 사용자 정보

**POST /users** ⇒ 사용자 추가

**GET /users/(ID)** ⇒ 사용자 한명만 볼 때

**PUT /users/(ID)** ⇒ 사용자 한명만 수정하기

**DELETE /users/(ID)** ⇒ 사용자 삭제