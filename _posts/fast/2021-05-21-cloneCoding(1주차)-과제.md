---
layout: post
title: 2021-05-21 cloneCoding(1주차)
category: cloneCoding
permalink: /log/:year/:month/:day/:title/
tags: [클론코딩]
comments: true








---



# 밑바닥부터 배포까지 클론코딩

# 1주차(5/21) - 과제

1. 출력으로 아래와 같이 나오도록 reduce를 사용해서 완성하시오.

```jsx
// 출력값(number의 합) { number : 23 }
const programming = [
  { name: "python", number: 2 },
  { name: "nodejs", number: 1 },
  { name: "java", number: 20 }
];

console.log(
  // 작성해주세요
  programming.reduce()
);
```

풀이

```jsx
const programming = [
  { name: "python", number: 2 },
  { name: "nodejs", number: 1 },
  { name: "java", number: 20 },
];

const count = programming.reduce((acc, current) => acc + current.number, 0);
// 초기값을 넣어줌
console.log(`number : ${count}`);
```

어려웠던 점 :

객체 배열에서의 값 합산을 하려면 

**반드시 초기값을 주어아 한다.**

2. 아래와 같이 출력되도록 sort 함수로 완성하세요. (number가 큰순서)

```jsx
/*
[
  { name: 'java', number: 20 },
  { name: 'python', number: 2 },
  { name: 'nodejs', number: 1 }
]
*/

const programming = [
  { name: "python", number: 2 },
  { name: "nodejs", number: 1 },
  { name: "java", number: 20 }
];

console.log(
  // 작성해주세요.
  programming.sort()
);
```

풀이

```jsx
const programming = [
  { name: "python", number: 2 },
  { name: "nodejs", number: 1 },
  { name: "java", number: 20 },
];

const num = programming.sort((x, y) => y.number - x.number);

console.log(num);
```

항상 작은 수가 먼저였는데 이번엔 큰 수가 먼저나오는 것으로 바꼈었다.

3. name 의 길이가 5보다 작은것만 출력해서 아래와같이 나오도록 하시오.

```jsx
// 출력 : [ { name: 'java', number: 20 } ]
const programming = [
  { name: "python", number: 2 },
  { name: "nodejs", number: 1 },
  { name: "java", number: 20 }
];

console.log(
  // filter 함수를 완성해주세요.
  programming.filter()
);
```

풀이

```jsx
const programming = [
  { name: "python", number: 2 },
  { name: "nodejs", number: 1 },
  { name: "java", number: 20 },
];

const nameLength = programming.filter((i) => i.name.length < 5);

console.log(nameLength);
```

그동안 예제와 같아서 많이 쉬웠다.

4. 아래와 같이 출력되도록 class 문법으로 작성해보세요.

```jsx
/*
출력
  현대차이고 노란색입니다.
  기아차이고 빨간색입니다.
*/

class Car {}

var a = new Car("현대", "노란");
a.move();
var b = new Car("기아", "빨간");
b.move();
```

풀이

```jsx
class Car {
  constructor(a, b) {
    this.name = a;
    this.color = b;
  }

  move() {
    console.log(`${this.name}차이고 ${this.color}색 입니다.`);
  }
}

var a = new Car("현대", "노란");
a.move();
var b = new Car("기아", "빨간");
b.move();
```

수업 예제와 같아서 어렵지 않았다.

5. 2단 부터 9단까지 구구단을 출력하세요.

```jsx
for(var i=2 ; i<=9 ; i++ ){
  // 아래를 완성하세요.
  for(){
      
  }
}
```

풀이

```jsx
for (var i = 2; i <= 9; i++) {
  for (var j = 1; j <= 9; j++) {
    console.log(`${i} * ${j} = ${i * j}`);
  }
  console.log();
}
```

너무 많이 접해본 예제라 어렵지 않았다.

6. 

```jsx
// http://localhost:3000 으로 접속하면
// root url 이 화면에 나타나야 한다.

// http://localhost:3000/admin/products 으로 접속하면
// admin url 이 화면에 나타나야 된다

const express = require("express");

// 이 아래로 작성해주세요.

app.listen(port, function () {
  console.log("Express listening on port", port);
});
```

풀이

6.js

```jsx
const express = require("express");
// 이 아래로 작성해주세요.
const admin = require("./routes/admin");

const app = express();
const port = 3000;

app.get("/", (req, res) => {
  res.send("root url");
});

app.use("/admin", admin);

app.listen(port, function () {
  console.log("Express listening on port", port);
});
```

routes/admin.js

```jsx
const express = require("express");
const router = express.Router();

router.get("/products", (req, res) => {
  res.send("admin url");
});

module.exports = router;
```

수업 예제랑 크게 다르지않아 어려지 않았다.