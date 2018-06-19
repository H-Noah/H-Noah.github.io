---
title: "[실전] ReactJS로 웹 서비스 만들기 with 노마드코더 - 리뷰"
permalink: /docs/Nomad-Coder-with-ReactJS-Webservice/
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
