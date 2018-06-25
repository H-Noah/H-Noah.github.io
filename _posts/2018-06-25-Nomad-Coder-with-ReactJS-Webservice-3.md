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
---


**주의:** 수강 후 필요하다고 생각되는 부분만 발췌한 것입니다. **설치 방법과 필자가 알고있는 내용은 포함하지 않으니** 디테일함을 원하시는 분들은 꼭 수강하시길 바랍니다.
{: .notice--info}

> [1편]( /docs/Nomad-Coder-with-ReactJS-Webservice(1))과 [2편](https://emperorright.github.io//docs/Nomad-Coder-with-ReactJS-Webservice(2)/) 을 참조하세요.. 몇편까지 가려나

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
