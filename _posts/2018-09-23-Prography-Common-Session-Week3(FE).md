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

180924 오후 7시 37분 새로운 자료 전달완료

1801004 오전 11시 37분 제작완료

![mine1](/assets/images/18-10-04-TO-DO-1-mine.PNG)
![mine2](/assets/images/18-10-04-TO-DO-1-mine2.PNG)

반응형,,,,으로(600px기준) 버튼이라도 변하게 제작해보았다. 자료는 [GIT](https://github.com/emperorright/prography-FE-homework/tree/master/week3/homework/TO-DO-1)에 있다.




### html 원본 분석하기

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

> `<html lang="en" dir="ltr">`

dir 속성은 열거형 속성으로 요소의 텍스트에 대한 방향성을 나타낸다.
   - ltr, 왼쪽에서 오른쪽 방향을 의미하며, 영어와 같이 왼쪽에서 오른쪽으로 기술되는 언어에 사용됩니다
   - rtl, 오른쪽에서 왼쪽 방향을 의미하며, 아랍어와 같이 오른쪽에서 왼쪽으로 기술되는 언어에 사용됩니다
   - auto, 사용자 에이전트가 결정하도록 합니다. 이 방식은 요소의 내부에 있는 문자를 강한 방향성(strong directionality)을 갖는 문자를 찾을 때까지 파싱을 계속해 나가며, 찾은 방향성을 요소 전체에 적용하는 기본적인 알고리즘을 사용합니다.

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

    ```

  > ` <div class="container">`  

  div css에 대한 설명
     - 을 합니다.

 > ` <label for="psw-repeat"><b>Repeat Password</b></label>`  


 for 속성은 label 요소에서 Form 컨트롤을 나타내는 요소의 id 속성과 명시적으로 연결하는데 사용됩니다.
 - for 속성을 사용해서 폼 컨트롤을 캡션과 연결할 수 있습니다. 속성의 값은 레이블을 붙일 수 있는 폼 관련 요소의 ID여야 하고, label 요소와 같은 Document에 속해야 합니다.
 - 이 속성은 label 요소 안에 폼 컨트롤을 나타내는 input 요소 등을 넣지 않을 때에 사용합니다.



```html
    <div class="container signin">
      <p>계정이 있으신가요? 그렇다면 <a href="#">로그인하기</a></p>
    </div>
  </form>
</body>
```


> `<html lang="en" dir="ltr">`

dir 속성은 열거형 속성으로 요소의 텍스트에 대한 방향성을 나타낸다.
   - ltr, 왼쪽에서 오른쪽 방향을 의미하며, 영어와 같이 왼쪽에서 오른쪽으로 기술되는 언어에 사용됩니다

------
위 내용말고는 크게 공부할 것이 없었다.


### TO-DO-1 반응형으로 제작



## homework-private(TO-DO-2)

180923 제작한 페이스북 마크업을 반응형으로 바꿔라!
(디테일은 원하는 만큼)

> 확인 결과 원래 클론하려던 페이스북레이아웃이 반응형으로



## Previous(TO-DO-3)


* {
  box-sizing: border-box;
}
-----

html{
  padding: 10%;
  margin: 10%;
}
body{
  max-width: 1024px;
  margin: 10px auto;
}
이거날아가면 왜 다저렇게 돼!
