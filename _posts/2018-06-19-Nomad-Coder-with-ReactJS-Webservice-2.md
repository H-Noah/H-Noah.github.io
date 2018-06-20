---
title: "[실전] ReactJS로 웹 서비스 만들기 with 노마드코더 - 리뷰(2)"
permalink: /docs/Nomad-Coder-with-ReactJS-Webservice(2)/
last_modified_at: 2018-06-20T15:58:49-04:00
toc: true
classes: wide
author_profile: false
sidebar:
  title: "Order List"
  nav: sidebar-sample
---


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

>Render life cycle: componentWillMount() -> render0 -> componentDidMount()

>Update life cycle: compnentWillReceiveProps() -> shouldComponentUpdate0 -> componentWillUpdate() ->  render() -> component
