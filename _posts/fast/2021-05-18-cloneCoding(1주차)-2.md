---
layout: post
title: 2021-05-18 cloneCoding(1주차)-2
category: cloneCoding
permalink: /log/:year/:month/:day/:title/
tags: [클론코딩]
comments: true





---



# 밑바닥부터 배포까지 클론코딩

# 1주차(5/18)

## 콜백함수 및 클로저

### 콜백함수

함수안에 인자를 함수로 받는 경우가 있다.

```jsx
function test (num , callback) {
  callback(); // 인자로 받은 함수를 실행한다.
  console.log(num);
}

test(1, function(){
  console.log('콜백함수가 실행됩니다.');
});
```

실행결과

```jsx
콜백함수가 실행됩니다.
1
```

### 클로저

함수 내에서 변수를 메모리처럼 사용하는 것

```jsx
function ex_cl() {
  var num = 0; // 안에서 변수를 선언
  return function() { // return 을 익명함수로 선언
    num++;
    console.log(num);
  }
}

var test = ex_cl();
test(); // return을 함수로 줬기 때문에 호출이 가능
test();
```

실행 결과

```jsx
1
2
```

num을 멋대로 ++을 시킴 함수 안에서 저장되어있는 메모리처럼(저장되어있는 변수처럼) 사용

대표적인 사용 예는 **페이지네이션처리**

## 프론트엔드 사용

DOM 기초

HTML

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  숫자 :
  <div id="num"></div>
  <button id="plus">증가</button>
</body>
</html>
```

javascript

```jsx
var num = 1;
document.addEventListener('DOMContentLoaded', function(){
// 이벤트를 DOM이 다 로드되고나서 콜백함수로 추가한다.
  document.querySelector('#num').innerHTML = num;
  // #num에다가 다 로드 됬을 때 추가할거다.
});
document.querySelector('#plus').addEventListener('click', function(){
// #plus 버튼을 클릭했을 때 콜백함수 실행
  num++;
  document.querySelector('#num').innerHTML = num;
});
```

실행 결과

![2021-05-18-1](\images\2021-05-18-1.PNG)

![2021-05-18-2](\images\2021-05-18-2.PNG)

감소버튼 연습

HTML

```html
<body>
  숫자 :
  <div id="num"></div>
  <button id="plus">증가</button>
  <button id="minus">감소</button>
</body>
```

javascript

```jsx
var num = 1;
document.addEventListener('DOMContentLoaded', function(){
// 이벤트를 DOM이 다 로드되고나서 콜백함수로 추가한다.
  document.querySelector('#num').innerHTML = num;
  // #num에다가 다 로드 됬을 때 추가할거다.
});
document.querySelector('#plus').addEventListener('click', function(){
// #plus 버튼을 클릭했을 때 콜백함수 실행
  num++;
  document.querySelector('#num').innerHTML = num;
});
document.querySelector('#minus').addEventListener('click', function(){
// #minus 버튼을 클릭했을 때 콜백함수 실행
  num--;
  document.querySelector('#num').innerHTML = num;
});
```

실행 결과

![2021-05-18-3](\images\2021-05-18-3.PNG)

![2021-05-18-4](\images\2021-05-18-4.PNG)

## jQuery

위 버튼을 jquery로 변경

```jsx
var num = 1;
$(document).ready(function(){
// 다 로드되면 실행한다.
  $('#num').html(num);
  // #num에 num을 추가한다.
  $('#plus').click(function(){
  // #plus를 클릭했을 때
    num++;
    $("#num").html(num);
  });
  $('#minus').click(function(){
  // #minus를 클릭했을 때
    num--;
    $('#num').html(num);
  });
});
```

### datepicker 연습

HTML

```jsx
<body>
  <p>Date: <input type="text" id="datepicker"></p>
</body>
```

jQuery

```jsx
$(function(){
  $('#datepicker').datepicker();
});
```

실행 결과

![2021-05-18-5](\images\2021-05-18-5.PNG)

![2021-05-18-6](\images\2021-05-18-6.PNG)

![2021-05-18-7](\images\2021-05-18-7.PNG)

### 라이브러리 만들기

빨간색으로 글자색을 변환

HTML

```html
<body>
  <div id="abc">글자색 변환</div>
</body>
```

jQuery

```jsx
// $.fn -> jquery 프로토타입
// 글자색을 변하게 하는 라이브러리를 만듬
$.fn.changeColor = function(){
  $(this).css('color','red');
}

$('#abc').changeColor();
```

## ES6

### 클래스 문법

어제 한 프로토타입 문법을 가지고 와서 

```jsx
function Car(a, b, c) {
  this.name = a; // (this)는 public 변수
  this.color = b;
}
Car.prototype.move = function() {
  console.log(this.name + "차이고, " + this.color + '색 입니다.');
}
var a = new Car("현대", "검은");
a.move();
```

클래스 문법으로 바꾸면

```jsx
class Car {
  constructor(a,b) {
    this.name = a;
    this.color = b;
  }

  move() {
    console.log(this.name + "차이고, " + this.color + '색 입니다.');
  }
}
var a = new Car("현대", "검은");
a.move();
var b = new Car("기아", "흰");
```

실행 결과

```jsx
현대차이고 검은색 입니다.
기아차이고 흰색 입니다.
```

### 변수

그 전에는 var 를 사용해서 선언했지만 

지금부터는 const로 상수를 선언하고,

let으로 변수로 선언한다.

var로 선언한 경우

```jsx
var b = 10;
if(true) {
  var b = 20;
  console.log(b);
}
console.log(b);
```

실행 결과

```jsx
20
20
```

let으로 선언한 경우

```jsx
const a = 10;
// a = 20; 상수라 재지정할 수 없음.
let b = 10;
if(true) {
  let b = 20;
  console.log(b);
}
console.log(b);
```

실행 결과

```jsx
20
10
```

출력할 때 + 로 사용하던 것을 `으로 바꿔서 사용함.

```jsx
var a = 'hello'
console.log('a는 ' + a)
```

실행 결과

```jsx
a는 hello
```

```jsx
const a = 'hello'
console.log(`a는 ${a}`)
```

실행 결과

```jsx
a는 hello
```

### 화살표 함수

```jsx
var func1 = function(a,b) {
  return a + b;
}

console.log(func1(1,2));

const func2 = (a,b) => a+b;
console.log(func2(1,3));
```

실행 결과

```jsx
3
4
```

### 할당

```jsx
const [d, e, f] = [1, 2, 3]
console.log(e);
```

실행 결과

```jsx
2
```

### ... 연산자

```jsx
const arr1 = [1,2]
const arr2 = [3,4,5]
const arr3 = [...arr1 , ...arr2]
console.log(arr3)
```

실행 결과

```jsx
[1,2,3,4,5]
```

인자를 가변적으로 받고싶을 때

```jsx
function abc(a, ...b) {
  console.log(arguments[0])
}

abc('node.js','hello',1);
```

실행 결과

```jsx
node.js
```

## map , reduce , filter , sort

### map

```jsx
const numbers = [1,2,3,5,4]

const num = numbers.map((x) => {
  console.log(x)
  return x * 10
});

console.log(num);
```

실행 결과

```jsx
1
2
3
5
4
[10,20,30,50,40]
```

한번 더

```jsx
const cities = [
  {name : 'daegu' , count : 2},
  {name : 'seoul' , count : 1},
  {name : 'busan' , count : 20}
]

// const num = cities.map((x) => {
//   return x.count * 10
// });

const num = cities.map((x) => x.count * 10) // 위와 같은 방법임

console.log(num);
```

실행 결과

```jsx
[20, 10, 200]
```

### filter

```jsx
const numbers = [1,2,3,5,4]

const num = numbers.filter((x) => x < 4)

console.log(num);
```

실행 결과

```jsx
[1,2,3]
```

한번 더

```jsx
const cities = [
  {name : 'daegu' , count : 2},
  {name : 'seoul' , count : 1},
  {name : 'busan' , count : 20}
]

const num = cities.filter((n) => n.name == 'seoul')
const num2 = cities.filter((c) => c.count < 10 )

console.log(num)
console.log(num2)
```

실행 결과

```jsx
{name : 'seoul' , count : 1}

{name : 'daegu' , count : 2}
{name : 'seoul' , count : 1}
```

### sort

```jsx
const numbers = [1,2,3,5,4]

console.log(numbers.sort());
```

실행 결과

```jsx
[1,2,3,4,5]
```

한번 더

```jsx
const numbers = [1,2,3,5,4]

const num = numbers.sort((x, y) => {
  console.log(`x는 ${x}`)
  console.log(`y는 ${y}`)
  console.log(`---------------`)

  if(x > y) {
    return 1;
  } else {
    return -1;
  }
});
```

실행 결과

```jsx
x는 2
y는 1
---------------
x는 3
y는 2
---------------
x는 5
y는 3
---------------
x는 4
y는 5
---------------
x는 4
y는 3
---------------
x는 4
y는 5
---------------
[1,2,3,4,5]
```

위의 코드를 한줄로 줄일 수 있다.

```jsx
const num = numbers.sort((x, y) => x-y)
```

한번 더

```jsx
const city = cities.sort((x,y) => x.count - y.count);
console.log(city)
```

실행 결과

```jsx
{name : 'seoul' , count : 1}
{name : 'daegu' , count : 2}
{name : 'busan' , count : 20}
```

### reduce

```jsx
const numbers = [1,2,3,5,4]

let acc = 0;
for (let i = 0; i < numbers.length; i++) {
  acc += numbers[i];
}
console.log(acc);
```

실행 결과

```jsx
15
```

저게 reduce로 바꾸면

```jsx
const numbers = [1,2,3,5,4]
const num = numbers.reduce( (acc, current) => {
  // acc 는 누적되는 값
  console.log(`acc는 ${acc}`)
  // current 는 현재 값
  console.log(`current는 ${current}`)
  console.log(`---------------------`)
  return acc + current;
});
console.log(num);
```

실행 결과

```jsx
acc는 1
current는 2
---------------------
acc는 3
current는 3
---------------------
acc는 6
current는 5
---------------------
acc는 11
current는 4
---------------------
15
```

위의 코드를 한줄로 줄일 수 있다.

