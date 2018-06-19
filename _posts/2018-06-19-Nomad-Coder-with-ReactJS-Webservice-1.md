---
title: "[실전] ReactJS로 웹 서비스 만들기 with 노마드코더 - 리뷰(1)"
permalink: /docs/Nomad-Coder-with-ReactJS-Webservice(1)/
last_modified_at: 2018-06-19T15:58:49-04:00
toc: true
classes: wide
author_profile: false
sidebar:
  title: "Order List"
  nav: sidebar-sample
---


**주의:** 수강 후 필요하다고 생각되는 부분만 발췌한 것입니다. **설치 방법과 필자가 알고있는 내용은 포함하지 않으니** 디테일함을 원하시는 분들은 꼭 수강하시길 바랍니다.
{: .notice--info}

> 강의를 듣다가 수업내용 요약 겸 복습이 필요하다고 생각하여 작성하게 되었다.  강의자는 Nicolás Serrano Arévalo이며 참 **쿨하다**.

## 1-1. Introduction to React

### 리액트가 좋은 이유! (주관적)

<figure style="width: 250px" class="align-left">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/nomad-Composition250.png" alt="">
  <figcaption>출처: 노마드코더</figcaption>
</figure>

자바스크립트 기반이다.
:   Angular나 Vue.js처럼 다른 프레임워크를 배울 필요 없이 자바스크립트만 이해하면 된다. (Angular나 Vue를 제대로 다루어보지 않아서.. 공감이 잘 안간다. 추후 다른 프레임워크를 공부하여 따로 포스팅해야겠다.)

Composition, 구조가 Cool하다.
:   리액트 구조는 요소별, 컴포넌트 별로 나눠서 작업할 수 있다. 왼쪽 사진과 같이 각 요소(Composition)들을 따로 개발하여 합칠 수 있다. (모듈화가 잘 되어 있다는 얘기인 것 같다.)   

Unidirectional Data Flow(단방향 데이터 흐름)
:   데이터는 항상 일정한 장소에 위치해있고, 그 장소에서만 변경할 수 있다. (**Data is on the state**) 상태가 변했을 경우, 데이터는 그대로 있고 UI가 업데이트된다. 즉, 데이터가 UI를 변경시킬 뿐 UI는 데이터를 변경시킬 수 없다. (Data -> Change Data -> Update UI).

(ETC..)방대한 커뮤니티, 프레임워크가 아닌 UI 라이브러리
:   방대한 커뮤니티로 질답이 쉬우며 React는 MVC모델에서 View만을 다루기 때문에 다른 것들과 섞어쓸 수 있다.



## 1-2. What are we Building  

<figure style="width: 200px" class="align-right">
  <img src="{{ site.url }}{{ site.baseurl }}/assets/images/MovieApplication200.png" alt="">
  <figcaption>출처: dribbble.com</figcaption>
</figure>  

  오른쪽 그림과 같은 대시보드를 클론코딩 할 예정이다.  

 > API는 yps를 사용한다. (영화에 관련된 정보를 긁어오는 API  영화리스트, 추천, 별점 등의 정보를 JSON 형태로 제공한다.)  

  **주의:** 설치 및 Hello world 출력,  Webpack 관련 설명영상은 생략하고 바로 2장으로 넘어갑니다.
  {: .notice--warning}

## 2-1. Creating React Components with JSX

아래의 세 컴포넌트와 JSX를 이용하여 무비앱을 생성해 볼 것이다.

  <figure style="width: 200px" class="align-left">
    <img src="{{ site.url }}{{ site.baseurl }}/assets/images/MovieAppComponent(200).png" alt="">
    <figcaption>출처: 노마드코더</figcaption>
  </figure>  

  빨간 컴포넌트 (무비리스트 컴포넌트)
  :   영화 전체 리스트를 출력한다. 크고 기본에 해당하므로 app 컴포넌트로 지정한다.

  파란 컴포넌트 (무비 컴포넌트)
  :  영화에 대한 자세한 정보를 가지고 있다.

  초록 컴포넌트 (이미지 컴포넌트)
  :    이름 그대로 이미지를 담고있는 컴포넌트이다.

  JSX
:    리액트 컴포넌트를 만들 때 사용하는 언어로 javascript안에서 사용하는 HTML

---




### 무비리스트 컴포넌트 - APP.js, Index.js 분석하기.

_index.html 코드 분석_

> 이번 강의에서는 <div>안의 내용만 참조하면 될 것 강다.

 ```html
 <!DOCTYPE html>
 <html lang="en">
   <head>
     <meta charset="utf-8">
     <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
     <meta name="theme-color" content="#000000">

     <link rel="manifest" href="%PUBLIC_URL%/manifest.json">
     <link rel="shortcut icon" href="%PUBLIC_URL%/favicon.ico">

     <title>Movie App</title>
   </head>
   <body>
     <noscript>
       You need to enable JavaScript to run this app.
     </noscript>

     <div id="root">
 <!-- 여기 index.js에서 renderer함수를 호출하여 view를 보여줌 -->
     </div>

   </body>
 </html>

 ```


 _index.js코드 분석_

 >  직접 요소검사를 보면 알 수 있겠지만 실제로 우리가 만드는 컴포넌트들은 index.js에서 불러와진다.

 ```javascript
 import React from 'react';
 import ReactDOM from 'react-dom';
 import './index.css';
 import App from './App';
 import registerServiceWorker from './registerServiceWorker';

//바로 여기!에서 ReactDOM이 APP 컴포넌트를 ID가 root인 녀석에 render()한다.
 ReactDOM.render(<App />, document.getElementById('root'));
 //reactDOM은 하나의 컴포넌트를 RENDER한다고만 기억하면 된다.
 registerServiceWorker();
 ```


 **React VS ReactDOM** React는 UI라이브러리이다. 하지만 ReactDOM은 리액트(라이브러리)를 웹사이트에 출력(render)하는 것을 도와주는 모델이다. 즉, 리액트를 사용해서 무언가를 웹사이트에 올리고 싶은 경우 ReactDOM을 사용한다. 모바일의 경우 ReactNative라는 것이 존재함.
 {: .notice--info}
>  (잘 이해가 안된다면 UI, 라이브러리, DOM에 대한 정보를 찾아보길 바람..)


 _아래 코드는 app 컴포넌트 코드의 일부로 모든 Component는 render()함수를 포함해야 한다._

```javascript
class App extends Component {
  //RENDER - 이 컴포넌트가  나에게 보여주는 것이 무엇인가 를 담고있다.
  render() {
    //State - 모든 컴포넌트에 속한 객체로 바뀔 때 마다 Render를 재실행한다.
    return (
      <div className="App">
        {this.state.greeting}
        {movies.map((movies, index) =>{
          return <Movie title={movies.title}  poster={movies.poster} key={index} />
        })}
      </div>
    );
  }
}
```
![no-alignment](/assets/images/update_data_flow.png)





### 무비 컴포넌트 - Movie.js, Movie.css 만들기

APP.js와 같은 구조로 import, export를 진행하고 Movie.css또한 불러온다. 마지막으로 Movie Class를 만들어주고 Render를 진행한다.

_Props는 다음 강의에서 살펴보도록 하자._   

```javascript
import React, { Component } from 'react';
import PropTypes from  'prop-types'
import './Movie.css';


class Movie extends Component {
  //RENDER - 이 컴포넌트가  나에게 보여주는 것이 무엇인가 를 담고있다.
  render() {
    return (
      <h1>Hello~</h1>
    );
  }
}
export default Movie;
```

### 무비 컴포넌트 - MovieMovieposter 클래스 만들기

MoviePoster 클래스 > Render > Return > 이미지 소스(URL)

```javascript

class Movie extends Component {
  //RENDER - 이 컴포넌트가  나에게 보여주는 것이 무엇인가 를 담고있다.
  render() {
    return (
      <div>
      // Movie라는 컴포넌트를 불러오는 JSX!
       return <MoviePoster />
      </div>
    );
  }
}

//Movie.js 안에  Movie Poster 클래스를 추가한다.
class MoviePoster extends Component{
  render(){    
    return  (   <img src = " 내가 원하는 이미지의 url"  />  );
  }
}
```



App.js(대왕 컴포넌트) 안에 우리의 컴포넌트를 불러오고 실제 그 데이터는 각 컴포넌트(Movie.js)에 저장되어 있다.  

이렇게 컴포넌트 단위로 개발하고 조립하여 원하는 것을 만들어 낼 수 있는 것이 React의 가장 큰 힘이라고 한다.







기초흐름도:

index.js
