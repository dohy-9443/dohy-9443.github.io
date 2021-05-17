# 1주차(5/18)

## 함수

\images\2021-05-17.PNG)

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

