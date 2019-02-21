---
title: "[실전] ReactJS로 웹 서비스 만들기 with 노마드코더 - 리뷰(3)"
permalink: /docs/Nomad-Coder-with-ReactJS-Webservice(3)/
last_modified_at: 2018-06-25T15:58:49-04:00
toc: true
classes: wide
author_profile: false
sidebar:
  title: "Order List"
  nav: sidebar-sample
tags:
  - react
---


**주의:** 수강 후 필요하다고 생각되는 부분만 발췌한 것입니다. **설치 방법과 필자가 알고있는 내용은 포함하지 않으니** 디테일함을 원하시는 분들은 꼭 수강하시길 바랍니다.
{: .notice--info}

> [1편]( /docs/Nomad-Coder-with-ReactJS-Webservice(1))과 [2편](https://H-Noah.github.io//docs/Nomad-Coder-with-ReactJS-Webservice(2)/) 을 참조하세요.. 몇편까지 가려나

## 5-1. Dataflow with Props

모든 컴포넌트가 State가 있지는 않다. Stateless Functional Component도 존재하며 이녀석은 Props만 가지고 있다. Smart Component, Dumb Component(Stateless Functional Component)로 구분한다.

> 결론: Dumb Function은 HTML을 RETURN하는 기능만을 가진다!

Stateless Functional Component를 만드는 방법을 아래 코드로 보자

```javascript

class MoviePoster extends Component{

  static propTypes = {
    poster: PropTypes.string.isRequired
  }

  render(){
    return  (   <img src = {this.props.poster} />  );
  }
}

///////////////////////////////////////////////////////////////
function MoviePoster({poster}){
  return (
    <img src = {this.poster} alt="Movie Poster" />
  )
}


```

_////////////////////_ 를 기준으로 위 아래 Class와 Function은 같다. 둘 다 img와 props를 return한다.

> 그래서 왜 dumb component를 쓰냐?

어떤 Component들은 단지 return만을 위해 존재한다. 그런 컴포넌트들은 componentWillMount, componentDidMount.. update state.. 다 필요 없고 단지 하나의 props만 필요하므로 불필요한 행위를 하지 않기 위해서! 쓴다.
(dumb component는 state, function renter, 라이프사이클 모두 없다는 것을 기억!)

+Dumb func에서 Proptypes를 확인하는 방법!

```javascript

MoviePoster.propTypes  = {
  poster: PropTypes.string.isRequired
  //string을 number or int로 바꾸면 오류가 발생할 것!
}

```

보다시피 필요한 경우 dumb Func를 사용하면 훨씬 짧은 양으로 같은 기능을 구현할 수 있다! 아래는 원래 있던 Movie에서 불필요한 Class를 삭제하고 Dumb Function으로 변경한 코드이다. 기능은 똑같다.

```javascript
import React from 'react';
//더이상 컴포넌트를 사용하지 않으므로 {component} 삭제!
import PropTypes from  'prop-types'
import './Movie.css';


//Movie도 Dumb function으로 변경한다!
function Movie({title, poster}) {
  return (
    //더이상 클래스가 아니기 때문에 this.props를 삭제한다.
    <div>
      <MoviePoster poster = {poster}/>
      <h1>{title}</h1>
    </div>
  )
}

function MoviePoster({poster}){
  return (
    <img src = {poster} alt="Movie Poster" />
  )
}

Movie.propTypes   ={
  title: PropTypes.string.isRequired,
  poster: PropTypes.string.isRequired,
}


export default Movie;



```




## 6-1. Ajax in React

ajax(에이잭스, 아-작스 등.. 으로 읽힌다.)는 Asynchronous  Javascript ans XML의 약자로 요즘은 XML 보다는 JSON에 신경을 쓰면 된다.
JSON은 javascript object notation의 약자 오브젝트를 자바스크립트로 작성하는 기법이다.   

Fetch 덕분에 ajax를 react에 적용하기는 쉽다. 여기에 관련해서 HTTP request에 대해서도 다루어야 하지만... 시간관계상 인스타그램 풀스택 교육에서 다룬다고한다.
우선 전송방식은 GET 방식이며 **우리는 이번 시간에 FETCH를 이용해서 URL에서 뭔가를 GET하는 방법을 배운다!**
(URL은 API에서 가져올 것이다.)

componentDidMount()의 내용만 바꿀 것이다.  


```javascript

class App extends Component {

state = {}
  componentDidMount(){
    //이제 진짜 영화를 담는다!    
    fetch('https://yts.am/api/v2/list_movies.json?sort_by=download_count');
  }
}  
```

그래서 ajax를 왜 쓰는데?
:   뭔가를 불러올 때마다 새로고침 하기 싫으니까!(api 호출, 평점가져오기 등등) 또, 보이지 않는 곳에서 데이터를 다룰 수 있으니까 cool하다.

원래 ajax는 url에서 불러와서 다소 복잡한 면이 있었는데 최신 자바스크립트에서 promise를 지원하며 조금 쉬워졌다. promise는 다음 강의에서 설명한다.


## 6-2.Promises

Promise is Asynchronous! 앞의 명령어가 끝나든 말든 다음 명령어가 시작한다는 뜻이다. 다른작업이 끝나길 기다리지 않고 계속 다른 작업을 예약할 수 있다는 장점이 있다. 또한,

API 주소가 없어졌다고 생각해서.. 한참 찾다가. [VELOPERT.LOG](https://velopert.com/2597) 내용 중 [가짜 API](https://jsonplaceholder.typicode.com/) 가 있다는 것을 알게되었다~

>그렇지만 쓸 필요 없어졌다... 멀쩡한 소스를 GIT에서 CLONE했기 때문이다.


## 6-2.Async Await in React

 promises도 배웠으니 Await, Async를 배울 차례다. Await, Async는 fecth().then().catch()를 더 분명하게 작성할 수 있게 도와주는 도구이다.

애플리케이션이 크면 then()안에 then이 계속 되어 **CALLBACK HELL**(콜백지옥)을 만든다.

>여담이지만 이걸 듣고나니 삼성 멀티캠퍼스에서 들었던 교육이 REACT 기반이었다는거.. 부끄러워라 열심히 공부하자.

아무튼 그래서 Await, Async를 쓸거야.


```javascript
import React, { Component } from 'react';
import './App.css';
import Movie from './Movie'


class App extends Component {

state = {}

//componentDidMount후에 movies라는 변수를 가진 비동기함수 _getMovies를 실행한다.
//movies는 await모드에서 _callApi를 실행한 리턴값이다.
  componentDidMount(){
    this._getMovies();
  }


  _renderMovies = () => {
    const movies = this.state.movies.map((movie, index) => {
      return <Movie title={movies.title} poster={movies.title} key={index} />
    })
    return movies
  }

  _callApi = () => {

    //fetch()는
    //var oReq = new XMLHttpRequest();
    //oReq.addEventListener("load", reqListener);
    //oReq.open("GET", "http://www.example.org/example.txt");
    //oReq.send() 를 한줄로 만들었다고 생각해라!

      fetch('https://jsonplaceholder.typicode.com/posts/1')
      .then(response => response.json())
      .then(json => {
        movies: json.title
      })
      .catch(err => console.log(err));
      }


       _getMovies = async () => {
        //await:  _callApi가 성공하든 실패하든 끝나서 리턴값을 가져오길 기다리는 것!
        const movies = await this._callApi();
        //여기에 작성되는 코드는 윗라인이 끝나기 전에 실행되지 않는다!
      }




  //RENDER - 이 컴포넌트가  나에게 보여주는 것이 무엇인가 를 담고있다.
  render() {
    //State - 모든 컴포넌트에 속한 객체로 바뀔 때 마다 Render를 재실행한다.
    return (
      <div className="App">
            {this.state.movies ? this._renderMovies() : 'Loading..'}
      </div>
    );
  }
}

export default App;

```
