---
layout: post
title: 2021-05-20 cloneCoding(1주차)
category: cloneCoding
permalink: /log/:year/:month/:day/:title/
tags: [클론코딩]
comments: true







---



# 밑바닥부터 배포까지 클론코딩

# 1주차(5/20)

## 목차

1. express 시작
2. Routing
3. View Engine - Nunjucks
4. 템플릿 상속
5. 미들웨어
6. form ( body-parser )
7. 정적파일
8. Global View Variable
9. 404 , 500 error handling
10. nunjucks macro
11. Express 권장 구조

### 왜 Express 를 사용해야 하는 가

1. 웹서비스 관점
2. 프레임워크 선정시 고려해야 될점

![2021-05-19-8](\images\2021-05-19-8.PNG)

### 내장 모듈을 활용해서 웹서버를 띄워보기

```jsx
const http = require("http");
// node 내장 모듈

http
  .createServer((request, response) => {
    response.writeHead(200, { "Content-Type": "text/plain" });
    // 200번은 http 상태코드이다.
    // 응답 성공이라고 한다.
    response.write("Hello Server");
    response.end();
  })
  .listen(3000);
// 포트가 3000인거로 띄어달라
```

![2021-05-19-9](\images\2021-05-19-9.PNG)

express로 해보기

```jsx
const express = require("express");

const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("hello express");
});

app.get("/fastcampus", (req, res) => {
  res.send("fastcampus get");
});

app.listen(port, () => {
  console.log("Express listening on port", port);
});
```

## Nodemon

### 웹서버 띄우기

Chapter02. Express

[01.express](http://01.express) 시작 - 6:18초 부터 15분까지

nodemon 설치하기

cmd에서

npm install -g nodemon

```jsx
const http = require("http");
// node 내장 모듈

http
  .createServer((request, response) => {
    response.writeHead(200, { "Content-Type": "text/plain" });
    // 200번은 http 상태코드이다.
    // 응답 성공이라고 한다.
    response.write("Hello Server");
    response.end();
  })
  .listen(3000);
// 포트가 3000인거로 띄어달라
```

package.json

```jsx
{
  "name": "exnodemon",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start": "nodemon index.js"
  },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```

```jsx
"start": "nodemon index.js"
```

추가해주고

터미널에서

nodemon index.js

입력후 

[localhost:3000](http://localhost:3000) 실행하고나서

```jsx
response.write("Hello Server");
```

이부분을 

```jsx
response.write("Hello Server1111111");
```

이렇게 적고 새로고침하면 바로 실행된다.

### Routing

hello-express 폴더에서 진행

**routes** 라는 폴더를 만듬 

그 안에 **admin.js**를 만듬

admin.js

```jsx
const express = require("express");
const router = express.Router();

router.get("/", (req, res) => {
  res.send("admin 이후 url");
});
router.get("/products", (req, res) => {
  res.send("admin products 이후 url");
});

module.exports = router;
```

app.js 에 추가한다.

```jsx
const admin = require("./routes/admin");

...

app.get("/", (req, res) => {
  res.send("hello express");
});

app.use("/admin", admin);
```

후 실행하면 

localhost:3000/admin

localhost:3000/admin/products

가 만들어지고 들어갈 수 있음

### 과제

contacts 와 contacts/list 만들기

contacts.js

```jsx
const express = require("express");
const router = express.Router();

router.get("/", (req, res) => {
  res.send("contacts 이후 url");
});
router.get("/list", (req, res) => {
  res.send("contacts list 이후 url");
});

module.exports = router;
```

추가한 app.js

```jsx
const express = require("express");

const admin = require("./routes/admin");
const contacts = require("./routes/contacts");

const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("hello express");
});

app.use("/admin", admin);
app.use("/contacts", contacts);
// 미들웨어이다.

app.listen(port, () => {
  console.log("Express listening on port", port);
});
```

실행 결과

localhost:3000/contacts

![2021-05-19-10](\images\2021-05-19-10.PNG)

localhost:3000/contacts/list

![2021-05-19-11](\images\2021-05-19-11.PNG)