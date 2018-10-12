---
title: "[숙제]프로그라피 공통세션 -FE(3주차)"
permalink: /docs/Prography-Front-End-Session(4)
last_modified_at: 2018-10-11T17:58:49-04:00
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
TO-DO List (~10/6)

1. src/elements/index.js 코드 분석하기.
2. src/elements/index.js에 있는 코드를 개선해보기, 혹은 자신이 더 고민해서 구현해보기.
3. app.js에 getUserList 함수 구현
    - fetch를 이용하여 localhost:3000/users 데이터 가져오기.
    - details에 렌더링되는 함수를 참고하여, 가져온 데이터를 사용하여 렌더링 시킬 Elements 구현하기.
    - index.html를 참고하여, <section id='user-list'></section> 안에 list 렌더링 하기.
    - style은 src/assets/form.css에 정의하기.
4. 모르면 아래 참고사항 꼼꼼히 읽어보기, 그래도 모르면 검색하고 StackOverFlow 글 읽어보기, 또 모르면 검색/정리해서 질문하기.
```


## src/elements/index.js 코드 분석하기.(TO-DO 1)
`세부 내용을 채웁니다`

> const isEmpty

주석과 오브젝트 이름으로 알 수 있듯이 `isEmpty`는 오브젝트가 Empty인지 아닌지 판별하는 기능을 가진다.

```javascript
/*
 ** Check Object is Empty or not.
 */
const isEmpty = (obj) => {
  Object.keys(obj).forEach((key) => {
    if (Object.prototype.hasOwnProperty.call(obj, key)) {
      return false;
    }
    return true;
  });
};
```

[MSDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Object/hasOwnProperty)에 따르면 정의는 아래와 같다.

```
hasOwnProperty() 메소드는 객체가 특정 프로퍼티를 가지고 있는지를  나타내는 불리언 값을 반환한다.
```

선택한 오브젝트에 임의의 키값들을 넣어서 없는경우 false를 반환하는데..쓰는데가 없는듯?하다..


> createElement

마찬가지로 이름으로 알 수 있듯이 `createElement`는 attribute와 함께 target에 Element를 만들거나 Render한다..?


1. createElement 객체는 tag, attributes, content, chindren을 가진다.
2. 만약 tag가 없거나 `string`이 아닌경우 오류를 발생시키며 null을 리턴한다/
3. element 객체에는 **createElement()** 함수를 이용하여 **tag** 라는 이름을 가진 엘리먼트를 생성해 담는다.
4. 만약 attributes가 배열이거나 length가 있는 경우, element의 attribute에 name과 value를 나누어 집어넣는다. (아니더라도 작업은 동일하다)
5. content가 존재하거나 string type인 경우 element.innerHTML을 이용하여 element의 내부 HTML코드를 변경한다.
6. 

```javascript
/*
 ** Create and Render Element into target with attributes.
 */
const createElements = ({
  tag,
  attributes,
  content,
  children,
}) => {
  if (!tag || typeof tag !== 'string') {
    console.error('tag argement is required and string');
    return null;
  }
  const element = document.createElement(tag);
  if (Array.isArray(attributes) && attributes.length) {
    attributes.forEach(({
      name,
      value,
    }) => {
      element.setAttribute(name, value);
    });
  }
  if (content && typeof content === 'string') {
    element.innerHTML = content;
  }
  if (Array.isArray(children) && children.length) {
    children.forEach((child) => {
      // Reculsive methods
      const childEelement = createElements({
        tag: child.tag,
        attributes: child.attributes,
        content: child.content,
        children: child.children,
      });
      element.appendChild(childEelement);
    });
  }
  return element;
};
```


```javascript
const createAndRenderElement = ({
  tag,
  attributes,
  content,
  children,
}, target, isClean = false) => {
  const element = createElements({
    tag,
    attributes,
    content,
    children,
  });
  if (isClean) {
    while (target.hasChildNodes()) {
      target.removeChild(target.lastChild);
    }
  }
  target.appendChild(element);
};

export {
  isEmpty,
  createAndRenderElement,
};
```



## src/elements/index.js에 있는 코드를 개선해보기, 혹은 자신이 더 고민해서 구현해보기.(TO-DO 2)
[세부 내용을 채웁니다](세부 내용을 채웁니다)


## app.js에 getUserList 함수 구현(TO-DO 3)

```cmd
세부 내용을 채웁니다
```


### fetch를 이용하여 localhost:3000/users 데이터 가져오기.
```javascript
세부 내용을 채웁니다   
```

### details에 렌더링되는 함수를 참고하여, 가져온 데이터를 사용하여 렌더링 시킬 Elements 구현하기.
세부 내용을 채웁니다
{: .notice--info}


### index.html를 참고하여, <section id='user-list'></section> 안에 list 렌더링 하기.
세부 내용을 채웁니다   
{: .notice--warning}


### style은 src/assets/form.css에 정의하기.
세부 내용을 채웁니다
{: .notice--primary}


## 모르면 아래 참고사항 꼼꼼히 읽어보기, 그래도 모르면 검색하고 StackOverFlow 글 읽어보기, 또 모르면 검색/정리해서 질문하기.
세부 내용을 채웁니다
{: .notice--notice}
