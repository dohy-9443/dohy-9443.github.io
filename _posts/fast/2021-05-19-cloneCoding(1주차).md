---
layout: post
title: 2021-05-19 cloneCoding(1주차)
category: cloneCoding
permalink: /log/:year/:month/:day/:title/
tags: [클론코딩]
comments: true






---



# 밑바닥부터 배포까지 클론코딩

# 1주차(5/19)

## 목차

1. Node.js 란?
2. Node.js 설치하기
3. 에디터 설치
4. 모듈 패턴
5. npm
6. nodemon

# **Node.js란?**

- 웹브라우저에서 쓰이는 자바스크립트를 서버에서 사용가능 ( 자바스크립트 문법 서버에서 사용가능 )
- 무엇이 가능하게 했나? ( V8의 탑재 )
- V8 이란? 크롬에 탑재된 자바스크립트 엔진
- 대용량 서비스를 위해 Ryan Lienhart Dahl 이 개발

## Node.js 설치하기

[https://nodejs.org/ko/download/](https://nodejs.org/ko/download/)

사이트 들어가서 

LTS 버전으로 운영체제 맞게 받으면 된다.

다운로드가 완료되었을 시

cmd 창에서

node -v 

npm -v 

치면 버전이나온다.

재대로 나온다면 다운로드 완료

## 에디터 설치하기

[https://code.visualstudio.com/download](https://code.visualstudio.com/download)

사이트 들어가서

운영체제에 맞게 다운로드 하면 된다.

다운로드 완료시 

바탕화면에 폴더 만들고 vscode에 드래그하면 세팅이 된다.

상단에 동그라미 표시가 뜨면 저장이 안된 것이고, 저장을 하면 x 표시가 나온다.

## 모듈 패턴

- 내보낼땐 **Module.exports 변수**
- 불러올때 **require 파일명**

**Module.exports**

myvar.js

```jsx
module.exports.a = "hello a";
```

index.js

```jsx
const myvar = require("./myvar");

console.log(myvar);
```

실행 결과

```jsx
hello a
```

함수도 가능

myvar.js

```jsx
function Myvar() {
  this.name = "my instance";
  this.hello = "my instance hello";
}
module.exports = Myvar;
```

index.js

```jsx
const My = require("./myvar");
const setVar = new My();
console.log(setVar.name);
console.log(setVar.hello);
```

실행 결과

```jsx
[Function: Myvar]
my instance
my instance hello
```

### npm

남이 만든 npm을 다운받아 보자

우선 package.json을 먼저 만들어보자

터미널 키고

npm init

name에서는 그냥 enter

버전도 enter

description: node online

entry point: index.js

test command , git repository , keywords 그냥 공란

author : 본인 이름

license : "ISC"

Is this OK? yes

하면 package.json이 만들어진다.

그리고 

터미널 다시 키고 

npm install express를 다운

npm install uuid4를 다운

그 후 index.js 를 만듬

```jsx
const uuid4 = require('uuid4');
console.log(uuid4());
```

쳐본다.

경로를 입력 안했다.

내가 만든 모듈안에서는 경로를 찾아가야된다.

남이 만든 모듈을 받으면 저렇게 써도 가능하다.

package.json

```jsx
{
  "name": "exex",
  "version": "1.0.0",
  "description": "node online",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "start" : "node index.js"
  },
  "keywords": [],
  "author": "백동현",
  "license": "ISC",
  "dependencies": {
    "express": "^4.17.1",
    "uuid4": "^2.0.2"
  }
}
```

이걸 보면 

```jsx
"dependencies": {
  "express": "^4.17.1",
  "uuid4": "^2.0.2"
}
```

여기에 내가 어떤 모듈들을 사용하는지 알 수 있다.

package-lock.json은 

지금 현재 

- express
    - lodash v3
- uuid4
    - lodash v4

이렇게 되어있는데 lodash v4로 해버리면 express는 3버전이기 때문에 최적화 때문에 문제가 발생할 수 있다.

각 라이브러리에 하위의 참조하는 라이브러리가 lock.json에 담겨있다.

각 모듈들의 버전이 명시되어있다. 모듈충돌 방지