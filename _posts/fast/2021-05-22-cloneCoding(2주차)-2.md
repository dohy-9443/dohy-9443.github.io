---
layout: post
title: 2021-05-22 cloneCoding(2주차)
category: cloneCoding
permalink: /log/:year/:month/:day/:title/
tags: [클론코딩]
comments: true







---



# 밑바닥부터 배포까지 클론코딩

# 1주차(5/22)

## 정적파일

express 에서 url을 만들때 admin.js에 admin/products를 url로 작성을 했다. 근데 이미지를 올리거나 css , js를 올리는 경우 한폴더에 다 있는데 uploads에 1.jpg같이 하나하나 올리는게 아니라 해당 폴더 자체에 있는 것은 url에서 접근되면 전체가 보이게 하는 것을 정적파일로 세팅을 한다라고 한다.

우선 template과 같은 선상에 폴더를 만든다.

uploads라는 폴더를 만든 후

app.js에 작성한다.

```jsx
app.use('/uploads', express.static('uploads'));
```

앞에는 url 뒤에는 express에서 static(정적파일/폴더(uploads))를 추적해달라 라는 의미 이다.

그리고 uploads 폴더 안에 이미지 하나 넣는다.

실행해보면

![2%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1(5%2025)%20702a0fc585b94dcaaf57e18f176a226e/2021-05-22-25.png](2%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1(5%2025)%20702a0fc585b94dcaaf57e18f176a226e/2021-05-22-25.png)

이런식으로 나온다.

## Global View Variable

로그인한 사람한테는 로그아웃버튼을 활성화 시켜주고싶고, 로그인 안한 사람한테는 로그인 버튼을 활성화 해주고 싶다. 그럴 때 사용함

app.js

```jsx
app.use((req, res, next) => {
  app.locals.isLogin = true;
  next();
});
```

작성을 하고 

모든 곳에서 보고싶으니

base.html

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

    {% if isLogin %}
      로그인 중
    {% else %}
      로그인이 안되어있습니다.
    {% endif %}

    {% block content %}{% endblock %}
  </div>
</body>
</html>
```

이부분은 nunjucks의 문법이다.

```html
{% if isLogin %}
  로그인 중
{% else %}
  로그인이 안되어있습니다.
{% endif %}
```

실행을 해보면

![2%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1(5%2025)%20702a0fc585b94dcaaf57e18f176a226e/2021-05-22-26.png](2%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1(5%2025)%20702a0fc585b94dcaaf57e18f176a226e/2021-05-22-26.png)

![2%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1(5%2025)%20702a0fc585b94dcaaf57e18f176a226e/2021-05-22-27.png](2%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1(5%2025)%20702a0fc585b94dcaaf57e18f176a226e/2021-05-22-27.png)

이런식으로 볼 수 있다.

```jsx
// Global View Variable
app.use((req, res, next) => {
  app.locals.isLogin = false;
  next();
});
```

이부분을 true → false로 변경해보면

![2%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1(5%2025)%20702a0fc585b94dcaaf57e18f176a226e/2021-05-22-28.png](2%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1(5%2025)%20702a0fc585b94dcaaf57e18f176a226e/2021-05-22-28.png)

![2%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1(5%2025)%20702a0fc585b94dcaaf57e18f176a226e/2021-05-22-29.png](2%E1%84%8C%E1%85%AE%E1%84%8E%E1%85%A1(5%2025)%20702a0fc585b94dcaaf57e18f176a226e/2021-05-22-29.png)

이런식으로 볼 수 있다.

## 404, 500 error handing