---
title: "[숙제]VueJS-get-started(FE)"
permalink: docs/VueJS-get-started(FE)
last_modified_at: 2018-12-12T17:58:49-04:00
excerpt: "Vue.js 책을 참조하며 겪은 경험"
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




vue-cli로 시작해본다.


## 선언적 렌더링

1. Build commits in your github repository(Recommend TIL).
 - TIL: Today I Learned
2. Make a Branch(Never use master), and PR from Working Branch to master.
 - PR: Pull Reaquest
3. Tell me PR URL, I will review your codes.
4. Finish.



## index.html에 있는 Form을 제거 및 순수 JS로 FORM 제작(TO-DO 1,2)


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



## app.js, index.js도 순수 JS만사용? (TO-DO 3)

원래 다 순수js아니었던가.... 아무튼 그래서 babel로 변환되지 않으면 브라우저가 읽지못하는 import와 export만 변경해주었다. 아래사진처럼 짜잔.

![result](/assets/images/18-11-02-capture-2.PNG);

+ 소스도 조금 수정하고 css도 import시켜서 처리했다.
