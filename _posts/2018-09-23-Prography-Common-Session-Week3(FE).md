---
title: "[강의요약]프로그라피 공통세션 -FE(3주차)"
permalink: /docs/Prography-Front-End-Session(3)
last_modified_at: 2018-09-23T15:58:49-04:00
toc: true
classes: wide
author_profile: false
sidebar:
  title: "Order List"
  nav: sidebar-sample
tags:
  - frontend
  - html
  - css

---

```
TO-DO List (~10/6)

1. 민정멘토님 숙제(FE 공통)
2. 성환멘토님 숙제(FE 멘토)
3. 학습자료 공부 및 지난 주 숙제 복습, 마무리(https://www.w3schools.com/html/html_responsive.asp) + 성환멘토님 소스분석 자료 읽기 + 민정멘토님 html, css 자료 확인하기
```


## homework-common(TO-DO-1)

180923 오후 3시 50분 아래 사진과 같은 레이아웃을 제작한다.

![homework](/assets/images/18-09-23-prograpy-common-homework-layout.png)

180924 오후 7시 37분 새로운 자 전달완료



###html head부분 분석하기

```html
<!DOCTYPE html>
<html lang="en" dir="ltr">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <link rel="stylesheet" href="form.css">
    <title>Form task</title>
  </head>
</html>
```


+ 크게 볼건없고 `<html lang="en" dir="ltr">`

+ 참고: 핀터레스트(디자인 레퍼런스 서치사이트)
+ 목적: 내가 그릴 수 있는 도화지의 범위가 어디인가 (해상도와 그리드에서 답을 찾았었다.)
+ 해상도: 해상도의 개념 설명, 해상도가 중요한 이유
container의 div 사이즈를 물어본이유


```html
<body>

  <form action="/action_page.php">
    <div class="container">
      <h1>새 계정 만들기</h1>
      <p>계정을 만들려면, 양식을 작성하십시오</p>
      <hr>

      <input type="text" placeholder="Enter Email" name="email" required>
      <label for="email"><b>Password</b></label>
      <input type="password" placeholder="Enter Password" name="psw" required>

      <label for="psw-repeat"><b>Repeat Password</b></label>
      <input type="password" placeholder="Repeat Password" name="psw-repeat" required>
      <hr>
      <p>계정을 생성하면 <a href="#">이용 약관 및 개인 정보 보호 정책</a>에 동의하게됩니다.</p>

      <button type="submit" class="registerbtn">등록하기</button>
    </div>

    <div class="container signin">
      <p>계정이 있으신가요? 그렇다면 <a href="#">로그인하기</a></p>
    </div>
  </form>
</body>
```

## homework-private(TO-DO-2)

180923 제작한 페이스북 마크업을 반응형으로 바꿔라!
(디테일은 원하는 만큼)

> 확인 결과 원래 클론하려던 페이스북레이아웃이 반응형으로



## Previous(TO-DO-3)
