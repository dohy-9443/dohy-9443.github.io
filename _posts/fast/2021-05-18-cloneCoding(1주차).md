---
layout: post
title: 2021-05-18 cloneCoding(1주차)
category: cloneCoding
permalink: /log/:year/:month/:day/:title/
tags: [클론코딩]
comments: true





---



# 밑바닥부터 배포까지 클론코딩

# 1주차(5/18)

## 함수

![2021-05-17](\images\2021-05-17.PNG)

```jsx
<script>
  function test(a) {
    console.log(a);
  }
  test(10);
</script>
```

실행결과

```jsx
10
```

두 개일 경우

```jsx
<script>
  function test(a, b) {
    console.log(a);
    console.log(b);
  }
  test(10, "haha");
</script>
```

```jsx
10
haha
```

더하기

```jsx
<script>
  function sum(a, b) {
    return a + b;
  }
  var c = sum(10, 20);
  console.log(c);
</script>
```

실행 결과

```jsx
30
```

위에 함수를 더 짧게 선언하는 방법

```jsx
<script>
  var sum = function() {
    console.log('sum 함수를 호출했나요?');
  }
  var sum2 = function(a,b) {
    return a+b;
  }
  var c = sum();
  var d = sum2(1,2);
  console.log(d);
</script>
```

실행 결과

```jsx
sum 함수를 호출했나요?
3
```

### 객체

자바스크립트는 기본 자료형과 객체형으로 이루어져있다.

객체는 '**일정 틀을 만들고 찍어낸다.**' 라고 생각하면 된다.

```jsx
<script>
  function Car(a, b) {
    this.name = a;
    this.color = b;
  }
  var a = new Car("현대", "검은색");
  console.log(a.name);
  console.log(a.color);

  var b = new Car("기아", "흰색");
  console.log(b.name);
  console.log(b.color);
</script>
```

실행 결과

```jsx
현대
검은색
기아
흰색
```

**public 변수 , private 변수**

```jsx
<script>
  function Car(a, b, c) {
    this.name = a; // (this)는 public 변수
    this.color = b;
    var move = c; // 이 함수 내부에서의 move는 private 변수이다.
  }
  var a = new Car("현대", "검은색", "전진");
  console.log(a.name);
  console.log(a.color);
  console.log(a.move);
</script>
```

실행 결과

```jsx
현대
겸은색
undefined
```

## 프로토타입

자바스크립트는 **프로토타입기반 언어**이다.

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

실행 결과

```jsx
현대차이고 검은색입니다.
```

또 다른 예제 (배열)

```jsx
var a = [1,2,3,4,10];
Array.prototype.print = function() {
  for(var i = 0; i < this.length; i++) {
    console.log(i);
  }
}
a.print();
```

실행 결과

```jsx
1
2
3
4
10
```

## 리터럴객체

배열과 다르게 중괄호{} 로 사용하고 

```jsx
var a = {}
```

이런 식으로 생성 한다.

예제

```jsx
// 리터럴객체 선언
var a = {
  'a' : 110,
  'b' : 'hello',
  'c' : function() {
    console.log('ccc');
  }
}
a.c();
console.log(a.a);
console.log(a.b);
```

실행 결과

```jsx
ccc
110
hello
```

## 조건문

특정 조건일 때 실행되는 부분을 작동해라 

### if문

```jsx
if(특정 조건) {
  특정조건에 해당하면 실행되는 문;
}
```

간단 예제

```jsx
var a = 5;
if(a < 10) {
  console.log('10보다 작다.');
}
```

실행 결과

```jsx
10보다 작다.
```

### == , === , ! == 차이

```jsx
var a = 5;
if(a == '5') { // 숫자형 5와 문자형 5는 같다.
  console.log('5와 \'5\'는 같습니다.');
}
if(a === '5') { // === 이거는 형태까지 같아야 된다.
  console.log('5와 \'5\'는 같습니다.');
} else {
  console.log('숫자형5와 문자형5는 형태가 달라 다르다.');
}
if(a !== 5) { // !== 다른지 비교
  console.log('a와 5는 다르다.');
} else if (a !== 6) {
  console.log('a와 6은 다르다.');
}
```

실행 결과

```jsx
5와 '5'는 같습니다.
숫자형5와 문자형5는 형태가 달라 다르다.
a와 6은 다르다.
```

### if - esle if - else

```jsx
var a = 15;
if(a < 10) {
  console.log('a는 10보다 작다.');
} else if (a < 20) {
  console.log('a는 20보다 작다.');
} else if (a < 30) {
  console.log('a는 30보다 작다.');
} else {
  console.log('a는 30보다 크다.');
}
```

실행 결과

```jsx
a는 20보다 작다.
```

### switch 문

```jsx
var color = 'red';
switch(color) {
  case 'orange':
    console.log('orange 입니다.');
    break;
  case 'red':
    console.log('red 입니다.');
    break;
  case 'yellow':
    console.log('yellow 입니다.');
    break;
  default :
    console.log('벗어나는 조건');
}
```

실행 결과

```jsx
red 입니다.
```

### 함수에서의 조건문

```jsx
function myNum(num) {
  if(num < 10) {
    console.log(num + '은(는) 10보다 작습니다.');
  } else {
    console.log(num + '은(는) 10이상입니다.');
  }
}

var test = myNum(5);
console.log(test);
```

실행 결과

```jsx
5은(는) 10보다 작습니다.
```
