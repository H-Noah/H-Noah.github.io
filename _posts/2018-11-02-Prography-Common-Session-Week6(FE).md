---
title: "[숙제]프로그라피 공통세션 -FE(7주차)"
permalink: /docs/Prography-Front-End-Session(7)
last_modified_at: 2018-11-02T17:58:49-04:00
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

```javascript
previous (~10/6)

1. src/elements/index.js 코드 분석하기.
2. src/elements/index.js에 있는 코드를 개선해보기, 혹은 자신이 더 고민해서 구현해보기.
3. app.js에 getUserList 함수 구현
    - fetch를 이용하여 localhost:3000/users 데이터 가져오기.
    - details에 렌더링되는 함수를 참고하여, 가져온 데이터를 사용하여 렌더링 시킬 Elements 구현하기.
    - index.html를 참고하여, <section id='user-list'></section> 안에 list 렌더링 하기.
    - style은 src/assets/form.css에 정의하기.
4. 모르면 아래 참고사항 꼼꼼히 읽어보기, 그래도 모르면 검색하고 StackOverFlow 글 읽어보기, 또 모르면 검색/정리해서 질문하기.


this.week(~11/03)

1. CreateElement부터 Rendering까지 직접구현
    1. index.html에 있는 Form을 제거
    2. Form과 1번 과제의 페이지의 기능을 순수 JS로 만들기
     

```




## How to submit report

1. Build commits in your github repository(Recommend TIL).
 - TIL: Today I Learned
2. Make a Branch(Never use master), and PR from Working Branch to master.
 - PR: Pull Reaquest
3. Tell me PR URL, I will review your codes.
4. Finish.



## index.html에 있는 Form을 제거(TO-DO 1)


```javascript
  //1차 뻘짓! 만들어야 할 것 
      
  //  1. <form action="/users" method="POST" id='myForm'>

  var myForm = document.createElement('form');
  myForm.method = 'post';
  myForm.action = '/user';
  myForm.target = '_blank';
  myForm.className = 'container';

  //  1-1. <fieldset>
  var myFieldset = document.createElement('fieldset');
  //  1-1-1. <legend> 
  var myLegend = document.createElement('legend');
  myLegend.setAttribute("value", "새 계정 만들기");
  //  1-1-2. <p>
  var myParagraph = document.createElement('p');
  myParagraph.setAttribute("value", "계정을 만들려면, 양식을 작성하십시오");
  //  1-1-3. <input type="text" placeholder="Enter Email" name="email">
  var myInput = document.createElement('input');
  myInput.setAttribute("type", "text");
  myInput.setAttribute("name", "email");    
  myInput.setAttribute("placeholder", "Enter Email");
  //  1-1-4. <label for="email">
  var myLabel = document.createElement('label');
  myLabel.setAttribute("for", "email");
  //  1-1-4-1 <b>
  //  1-1-4-1 <input>

  myForm.appendChild(myFieldset);
  myForm.appendChild(myLegend);
  myForm.appendChild(myParagraph);
  myForm.appendChild(myInput);
  myForm.appendChild(myLabel);    
    
```

> 1차 뻘짓

바보같이 위의 소스처럼 노가다로 만들었다가 아래코드로 수정했다.

```javascript

   var myForm = document.createElement('form');
    myForm.method = 'post';
    myForm.action = '/user';
    myForm.target = '_blank';
    myForm.className = 'container';

    myForm.innerHTML = [
      "<fieldset>",
      "<legend>새 계정 만들기</legend>",
      "<p>계정을 만들려면, 양식을 작성하십시오</p>",
      "<input type='text' placeholder='Enter Email' name='email'>",
      "<label for='email'>",
      "<b>Password</b>",
      "<input type='password' placeholder='Enter Password' name='password'>",
      "</label>",
      "<label for='psw-repeat'>",
      "<b>Repeat Password</b>",
      "<input type='password' placeholder='Repeat Password' name='password-repeat'>",
      "</label>",
      "<hr>",
      "<p>계정을 생성하면 <a href='#'>이용 약관 및 개인 정보 보호 정책</a>에 동의하게됩니다.</p>",
      "<button type='button' class='registerbtn' id='submitButton'>Button</button>",
      "<button type='button' class='registerbtn' id='getdataButton'>GetData</button>",
      "<div class='container signin'>",
      "<p>계정이 있으신가요? 그렇다면 <a href='#'>로그인하기</a></p>",
      "</div>",
      "</fieldset>"
    ].join("");

    document.body.appendChild(myForm);
```

결과는 아래 사진과 같다.
![result](/assets/images/18-11-02 capture-1.png);


+ CSS가 안먹어서 위쪽에 소스 다 때려박은건 안함정..
+ 시간이 정말 너무너무 없다... 이제 `app.js`에 구현되어있던 post기능과 validation기능, 데이터를 가져와서 render하는 기능을 만들어야 한다!
