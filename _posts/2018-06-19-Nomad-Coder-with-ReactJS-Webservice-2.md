---
title: "[실전] ReactJS로 웹 서비스 만들기 with 노마드코더 - 리뷰(2)"
permalink: docs/Nomad-Coder-with-ReactJS-Webservice(2)/
last_modified_at: 2018-06-20T15:58:49-04:00
toc: true
classes: wide
author_profile: false
sidebar:
  title: "Order List"
  nav: sidebar-sample
tags:
  - react
---


[실전] ReactJS로 웹 서비스 만들기 with 노마드코더 - 리뷰(2) - [1편]( /docs/Nomad-Coder-with-ReactJS-Webservice(1))이 너무 길어서 2편... 아니 3편까지 만들어 질 것 같다.
<!--more-->

**주의:** 수강 후 필요하다고 생각되는 부분만 발췌한 것입니다. **설치 방법과 필자가 알고있는 내용은 포함하지 않으니** 디테일함을 원하시는 분들은 꼭 수강하시길 바랍니다.
{: .notice--info}

> [1편]( /docs/Nomad-Coder-with-ReactJS-Webservice(1))이 너무 길어서 2편... 아니 3편까지 만들어 질 것 같다.

## 2-2. Dataflow with Props

리액트에는 2개의 주요 컨셉이 있다. **State** 와 **Props** 이다. 이 강의에서는 Props에 대해서 다룬다.

메인 컴포넌트는 영화정보를 담아와서 출력할 것이다. 이 말인 즉슨, _리스트(영화정보를 담을 그릇!)_ 가 존재한다는 뜻이다.  props는 부모컴포넌트가 자식컴포넌트에게 데이터를 보내는 것을 돕는 역할을 한다. 코드로 확인하자.

> App.js 중 일부

```javascript
const movies = [
  {
      title: "Maxtrix"
  }
]

class App extends Component {  
  render() {    
    return (
      <div className="App">
      //부모(app)컴포넌트에서 정의된 title을 자식 컴포넌트(movie)에 전달한다.
        <Movie title={movies.title}/>
      </div>
    );
  }
}
```


> Movie.js 중 일부

```javascript
import React, { Component } from 'react';
import PropTypes from  'prop-types'
import './Movie.css';


class Movie extends Component {
  render() {
    return (
      <div>
        <MoviePoster />      
        //props로 전달받은 부모 데이터를 출력한다.
        <h1>{this.props.title}</h1>
      </div>
    );
  }
}
```

위 코드와 같이 부모 컴포넌트에서 전달하고 싶은 데이터를JSX 문법으로 넘겨주면 자식 컴포넌트(movie.js)에서 props로 불러올 수 있다. **위와 같이 메인컴포넌트에서 데이터를 다 가지고 있고 자식 컴포넌트에게 넘겨주어 props로 받기만 하면 된다!**

> 실제 강의에서는 영화 제목, 포스터를 배열로 만들어서 Movie 컴포넌트에 여러개 넘겨줬다.. 굳이 할 필요 없는 작업으로 패스.

**TIP:** JSX문법의 경우 명령을 실행시키려면 괄호를 반드시 쳐야한다. (중괄호)
{: .notice--info}



## 2-3. Lists with .map

2-2 에서 배운 내용의 경우 모든 데이터를 직접 입력해야 하기 때문에 API로 대용량을 데이터를 긁어와서 출력하는 경우에는 적합하지 않다. 따라서 아래와 같이 배열 데이터를 모두 담아둔다.

```javascript
const movies = [
  {
      id: 1,
      title: "Maxtrix",
      poster: "https://m.media-amazon.com/images/M/MV5BNzc2ZThkOGItZGY5YS00MDYwLTkyOTAtNDRmZWIwMGRhYTc0L2ltYWdlXkEyXkFqcGdeQXVyNjU0OTQ0OTY@._V1_UX182_CR0,0,182,268_AL_.jpg"
  },
  {
    id: 2,
    title: "Full Metal Jacket",
    poster: "https://realorfake4k.com/wp-content/uploads/2018/02/matrix-4k-uhd-main.jpg"
  },
  {
    id: 3,
    title:   "Old Boy",
    poster: "https://upload.wikimedia.org/wikipedia/en/6/67/Oldboykoreanposter.jpg"
  },
  {
    id: 4,
    title:   "Star Wars",
    poster: "https://upload.wikimedia.org/wikipedia/commons/thumb/6/6c/Star_Wars_Logo.svg/375px-Star_Wars_Logo.svg.png"
  }
]
```

array에는 map()이라는 함수가 있다. map에 대한 내용은 [map()](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/map)을 참조하시기 바람. (다른 array의 엘리먼트를 포함한 새로운 array를 리턴한다.).  

아무튼, map 함수를 이용하여 **'movies' 배열을 가져다가 그 안의 element를 활용** 해서 새로운 array를 생성한다.

```javascript
class App extends Component {  
  render() {    
    return (
      <div className="App">      
      //여기서 쓰는게 map 함수. (arrow func에 대한 설명은 생략한다.)
      {movies.map(movie => {
      //(배열 하나를 잡고 그 배열을 토대로 컴포넌트를 만든다고 생각하면 될 것 같음)
        <Movie title={movies.title} poster={movies.poster} />
      })}        
      </div>
    );
  }
}
```




## 3-1. Lifecycle Events on React

컴포넌트 Lifecycle에 대해 알아보자. 컴포넌트는 여러 기능을 정해진 순서대로 실행한다. Render()와 Update의 라이프사이클은 차이가 있으며 자세한 내용은 아래와 같다.  

### Render() Life Cycle

>Render life cycle: componentWillMount() -> render0 -> componentDidMount()

Render life cycle
:    컴포넌트가 '존재'하는 경우 라이프사이클은 componentWillMount() -> render0 -> componentDidMount() 순서대로 진행되며 내가 원하든 말든 자동으로 발생한다. 무슨소리인지 아래 코드를 보고 이해해보자.  

```javascript
//APP.js
componentWillMount(){
  console.log("will mount");
}

componentDidMount() {
  console.log("Did mount");
}

render() {
  console.log("render()");
  return ;
}
```

위 코드를 실행하면 줄 순서대로 실행되는 것이 아니라 라이프사이클을 따라  componentWillMount() -> render0 -> componentDidMount() 순서로 실행된다.
만들고 있는 영화앱을 기준으로한다면 Willmount에서는 API에 작업요청을 한다. 완료 후, render()에서 데이터 관련 작업을 할 것이다.  


### Update Life Cycle

>Update life cycle: compnentWillReceiveProps() -> shouldComponentUpdate0 -> componentWillUpdate() ->  render() -> component  

Update life cycle
:    업데이트가 '발생'하는 경우 라이프사이클은 compnentWillReceiveProps() -> shouldComponentUpdate0 -> componentWillUpdate() ->  render() -> component   순서대로 진행된다.

compnentWillReceiveProps()
:   컴포넌트가 새로운 props를 받았다.

shouldComponentUpdate0
:   old, new props를 살펴서 그 둘이 다른 경우 update==true로 판정한다. 즉, 업데이트를 해야하는지 판정하는 라이프사이클

componentWillUpdate()
:   업데이트 할거야!

render()
:   업데이트!

> 그래서 어쩌라고? 쓸데가 있나?

넵. willmount를 보면 사이클 시작, render를 보면 컴포넌트 생성중, didmount를 보면 컴포넌트 생성 완료라는 정보를 캐치할 수 있다. 이러한 정보를 통해 **componentWillUpdate()를 수행중일 때 업데이트임을 알리기 위해 Loading 이미지를 띄워준던가..**  하는 방식으로 사용할 수 있다.


## 4-1. Creating React Components with JSX

State에 대해 배워보자.
 - State는 리액트 컴포넌트 안에 있는 오브젝트이다,
 - state가 바뀔 때 마다 render가 발생한다.(again)

State를 만드는 방법

```javascript

class App extends Component {

//1. GREETING 이라는 STATE 생성
  state = {
    greeting: 'Hello!'
  }

  componentDidMount(){
    setTimeout( () => {
      //2. Component가 MOUNT되면 5초를 기다리고 Greeting을 업데이트한다.
      //+state는 직접건들면 안된다. (이유는 모르겠네..) -> setState 사용해야한다!.
       this.setState({
         greeting: 'Hello aAGIN'
       })
    }, 5000)
  }

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


## 4-2. Practicing this.setState()

[4-1-creating-react-components-with-jsx](http://localhost:4000/docs/Nomad-Coder-with-ReactJS-Webservice(2)/#4-1-creating-react-components-with-jsx) 에서 배운 내용을 좀 더 알아보자.

컴포넌트 외부에 있는 무비리스트를 State 안으로 옮길 예정!

> 어디에 써? - 추가컨텐츠를 아래에 계속 로딩하며 페이스북, 인스타그램의 infinite scroll같은 기능을 제작할 수 있다!.


```javascript

componentDidMount(){
  setTimeout( ( )=> {
    this.setState({
      movies: [
        //이전 영화리스트를 그대로 두고, 하나를 추가하라! 아래53라인이 없으면 1초 후 영화리스트가 대체된다.
        ...this.state.movies,
        {
          title: "Trainspotting",
          poster: "https://upload.wikimedia.org/wikipedia/en/6/67/Oldboykoreanposter.jpg"
        }
      ]
    })
  }, 1000)
}

```

## 4-3. Loading States

내가 필요한 데이터가 항상 존재하지는 않는다. 데이터 API가 데이터를 구해서 주면 State가 업데이트 되면서 데이터가 생기게 될 것이다. 따라서 데이터가 불러지기 전 로딩 state를 타임아웃기능으로 구현해 볼 것이다.


>이를 위해 먼저 state 안의 movies를 componentDidMount()로 이동시키자.

```javascript

class App extends Component {
  state = {
  }

  componentDidMount(){
    setTimeout( ( )=> {
      this.setState({
        movies: [
          {
              id: 1,
              title: "Maxtrix",
              poster: "https://m.media-amazon.com/images/M/MV5BNzc2ZThkOGItZGY5YS00MDYwLTkyOTAtNDRmZWIwMGRhYTc0L2ltYWdlXkEyXkFqcGdeQXVyNjU0OTQ0OTY@._V1_UX182_CR0,0,182,268_AL_.jpg"
          },
          {
            id: 2,
            title: "Full Metal Jacket",
            poster: "https://realorfake4k.com/wp-content/uploads/2018/02/matrix-4k-uhd-main.jpg"
          },
          {
            id: 3,
            title:   "Old Boy",
            poster: "https://upload.wikimedia.org/wikipedia/en/6/67/Oldboykoreanposter.jpg"
          },
          {
            id: 4,
            title:   "Star Wars",
            poster: "https://upload.wikimedia.org/wikipedia/commons/thumb/6/6c/Star_Wars_Logo.svg/375px-Star_Wars_Logo.svg.png"
          },
          {
            id: 5,
            title: "Trainspotting",
            poster: "https://upload.wikimedia.org/wikipedia/en/6/67/Oldboykoreanposter.jpg"
          }
        ]
      })
    }, 1000)
  }
}
```

>state 안에 있던 movie를 옮겼으므로 (존재하지 않으므로) 아래 코드에서 오류가 날것이다.

```javascript
render() {
  return (
    <div className ="App">
      {this.state.movies.map((movie, index)=> {
        return <Movie title={movie.title} poster= {movie.poster} key={index}/>
      })}
      </div>
  );
}
```

따라서 loading state를 만들어줘야 하며 이를 위해  _renderMovies()_ 함수를 만들어 줄 것이다. 설명은 코드 안에 포함되어 있으며 당연히 render()함수 안의 내용도 아래와 같이 바뀌었다.

코드를 실행해보면 Loading..이라고 출력되다가 setTimeout으로 설정한 시간 이후에 영화정보가 출력됨을 알 수 있다.

```javascript
//movie라는 변수 값을 저장,
  //데이터가 없을 때, 로딩을 띄우고 있으면 영화정보가 보이도록 한다.
  //언더바(_)를 쓰는이유: 리액트 자체함5이 많으므로  내가만든 함수과 구별하기 위해서.
  _renderMovies = () => {
    const movies = this.state.movies.map((movie, index) => {
      return <Movie title={movie.title} poster={movie.poster} key={index} />
    })
    return movies
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
```
