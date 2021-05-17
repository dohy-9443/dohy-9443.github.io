---


layout: post
title: 2021-05-17 cloneCoding(1주차)
category: cloneCoding
permalink: /log/:year/:month/:day/:title/
tags: [클론코딩]
comments: true




---



# 밑바닥부터 배포까지 클론코딩

## 1주차(5/17)

## Javascript 란

브라우저를 제어하기 위해 넷스케이프에서 개발한 언어

사용자의 클릭, 계산기, 달력등의 이벤트 조작에 대응하기 위한 언어

자바스크립트의 확대

AJAX활용(구글맵) → Debug툴에 발전 → V8엔진의 개발 → Node.js등장 → Desktop, IoT, 사용법위 확대 → 여러 플랫폼 제작사에서 자바스크립트 개발자를 끌어안기 위한 환경 조성

- var로 선언 ( var a = 1; )

- 동적언어 이므로 자료형을 선언할 필요없음

  **예를 들어** 자바는 

  int i = 10;

  char c = "c";

  이렇게 쓰는데 이런거는 정적언어라고 한다.

- 기본자료형과 객체(Object) 두가지로 나뉜다.

| 기본 자료형 | 설명                                      |
| ----------- | ----------------------------------------- |
| Boolean     | 논리적인 요소를 나타내고, (true 와 false) |
| Null        | 객체 값이 존재하지 않는 다는 것을 의미    |
| Undefined   | 값을 할당하지 않음                        |
| Number      | 숫자형                                    |
| String      | 문자형                                    |
| Symbol      | ECMAScript 6 에서 추가, 유일하고 변경불가 |

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
  haha
  <script>
    var a = '123';
    console.log(a);
		var b = 'Node.js 수업입니다.';
    console.log(b);
    var c = false;
    console.log(c);
    var d;
    console.log(d);
  </script>
</body>
</html>
```

## 배열

- var a = ['안녕', 'Node.js', 55, 'Hello']

|  0   |    1    |  2   |   3   |
| :--: | :-----: | :--: | :---: |
| 안녕 | Node.js |  55  | Hello |

```jsx
<script>
  var a = ["hello", 22, "node.js", "333"];
  console.log(a[0]); // "hello"
  console.log(a[2]); // "node.js"
  a[4] = 4444;
  console.log(a[4]);
	a[0] = 'hi';
  console.log(a[0]);
	console.log(a.length); // 배열의 길이를 알고싶을 때
	console.log(a.indexOf("333")); // 333이 몇번째인지 알고싶을 때
</script>
```

실행 결과

```jsx
hello
node.js
4444
hi
5
3
```

### 배열(반복문)

```jsx
var a = ['hello', 22, 'node.js', 55];
for(var i = 0; i < a.length; i++) {
  console.log(a[i]);
}
```

실행 결과

```jsx
hello
22
node.js
55
```

배열을 출력함

## 반복문

1. for
2. while
3. do-while

```jsx
for(초기화 값; 제한조건; 증감식) {}
```

```jsx
<script>
  for(var i = 0; i < 5; i++) {
    document.write('화면에 찍어주세요.');
    document.write('<br/>');
  }
</script>
```

실행결과

```jsx
화면에 찍어주세요.
화면에 찍어주세요.
화면에 찍어주세요.
화면에 찍어주세요.
화면에 찍어주세요.
```

```jsx
while(제한조건){}
```

```jsx
<script>
  var i = 0;
  while(i < 5) {
    document.write('화면에 찍어주세요.');
    document.write('<br/>');

    i++;
  }
</script>
```

실행결과

```jsx
화면에 찍어주세요.
화면에 찍어주세요.
화면에 찍어주세요.
화면에 찍어주세요.
화면에 찍어주세요.
```

```jsx
do {
	// 무조건 실행되는 
} while(제한조건);
```

```jsx
<script>
  var i = 0;
  do {
    document.write('화면에 찍어주세요.');
    document.write('<br/>');
    i++;
  } while (i < 5);
</script>
```

실행결과

```jsx
화면에 찍어주세요.
화면에 찍어주세요.
화면에 찍어주세요.
화면에 찍어주세요.
화면에 찍어주세요.
```

### while 과 do while의 차이

```jsx
<script>
  var i = 0;
  while(i < 0) {
    document.write('화면에 찍어주세요.');
    document.write('<br/>');
    i++;
  }
  document.write('<br/>');
  document.write('<br/>');

  i = 0;
  do {
    document.write('화면에 찍어주세요.');
    document.write('<br/>');
    i++;
  } while (i < 0);
</script>
```

실행 결과

```jsx
화면에 찍어주세요.
```

do while문은 do {  } 안에 내용이 먼저 실행되고 조건을 비교하는데 while문은 조건을 먼저 비교한다.

그래서 실행 결과를 보면 while문에 내용은 실행이 안된반면 do while 문은 내용이 한번 출력이 된다.

### 구구단

```jsx
<script>
  for(var i = 2; i <= 9; i++) { // 2단~9단
    for(var j = 1; j <= 9; j++) {
      document.write(i + " * " + j + " = " + i*j);
      document.write("<br/>");
    }
    document.write("<br/>");
  }
</script>
```

실행 결과

```jsx
2 * 1 = 2
2 * 2 = 4
2 * 3 = 6
2 * 4 = 8
2 * 5 = 10
2 * 6 = 12
2 * 7 = 14
2 * 8 = 16
2 * 9 = 18

3 * 1 = 3
3 * 2 = 6
3 * 3 = 9
3 * 4 = 12
3 * 5 = 15
3 * 6 = 18
3 * 7 = 21
3 * 8 = 24
3 * 9 = 27

4 * 1 = 4
4 * 2 = 8
4 * 3 = 12
4 * 4 = 16
4 * 5 = 20
4 * 6 = 24
4 * 7 = 28
4 * 8 = 32
4 * 9 = 36

5 * 1 = 5
5 * 2 = 10
5 * 3 = 15
5 * 4 = 20
5 * 5 = 25
5 * 6 = 30
5 * 7 = 35
5 * 8 = 40
5 * 9 = 45

6 * 1 = 6
6 * 2 = 12
6 * 3 = 18
6 * 4 = 24
6 * 5 = 30
6 * 6 = 36
6 * 7 = 42
6 * 8 = 48
6 * 9 = 54

7 * 1 = 7
7 * 2 = 14
7 * 3 = 21
7 * 4 = 28
7 * 5 = 35
7 * 6 = 42
7 * 7 = 49
7 * 8 = 56
7 * 9 = 63

8 * 1 = 8
8 * 2 = 16
8 * 3 = 24
8 * 4 = 32
8 * 5 = 40
8 * 6 = 48
8 * 7 = 56
8 * 8 = 64
8 * 9 = 72

9 * 1 = 9
9 * 2 = 18
9 * 3 = 27
9 * 4 = 36
9 * 5 = 45
9 * 6 = 54
9 * 7 = 63
9 * 8 = 72
9 * 9 = 81
```