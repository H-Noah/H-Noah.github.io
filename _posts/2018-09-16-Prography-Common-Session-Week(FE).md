---
title: "[강의요약]프로그라피 공통세션 -FE"
permalink: /docs/Prography-Front-End-Session
last_modified_at: 2018-09-16T15:58:49-04:00
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

## HTML

### homework1-common
---

+ 마진이나 패딩이 디스플레이나 해상도에 따라 변하지 않는게 좋다. (고정값으로 써라) 코드를 읽어보시기 바랍니다.

+ 참고: 핀터레스트(디자인 레퍼런스 서치사이트)
+ 목적: 내가 그릴 수 있는 도화지의 범위가 어디인가 (해상도와 그리드에서 답을 찾았었다.)
+ 해상도: 해상도의 개념 설명, 해상도가 중요한 이유
container의 div 사이즈를 물어본이유
+ 그리드: 단의 너비 단의 개수 사이 너비(GUTTER) 가 필요하다.
(보통 12개 그리드 BUT 기획에따라 달라질 수 있다.)



### homework2-common
---


### homework2(private)
:   페이스북 클론코딩을 찾아 분석해본다!
---


#### Dashboard
:   대시보드형태를 먼저 분석한다. 클론할 페이지는 아래와 같다.

![dashboard](/assets/images/18-09-16-facebook-clone-dashboard.PNG)  

> 처음에 나오는 meta 태그부터 분석해보자.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

**viewport는 모바일 브라우저가 파일을 렌더링하는 가상 'window'이다.** 모바일 웹이 데스크탑 환경처럼 웹화면 전체를 자연스럽게 브라우징하는 `풀브라우징`을 지원하는 특징을 가져 뷰포트가 중요하게 여겨지기 시작했다. 즉, 작은화면의 모바일 단말기에 웹페이지를 모두 표시하려다보니 가독성이 상당히 떨어지는 것이다. 모바일 브라우저의 설정 - 데스크탑모드로 보기 를 누르면 알 수 있듯이 배율축소로 글자 및 이미지의 가독성이 현저하게 떨어져 뷰포트 메타태그를 이용하여 모바일웹에 최적화된 상태로 화면이 표시되게 하기 위함이다.


![viewport 적용 전/후](/assets/images/18-09-16-viewport-yes.PNG)


> 그래서 저 코드가 무슨 의미인데?  

```html
<meta name="viewport" content="width=device-width">
```

뒷 부분을 자르고 보면 위 태그의 내용은 뷰포트의 가로폭을 기본 값(페이지마다 다를 수 있다.)인 1024px이 아닌 모바일 단말기 장치의 가로폭으로 설정한다는 의미이다.(아이폰은 320px).


> 그럼 initial-scale=1.0은?

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

메타태크 속성표의 원문을 보면 아래와 같다.

```
initial-scale

The initial scale of the viewport as a multiplier. The default is calculated to fit the webpage in the visible area. The range is determined by the minimum-scale and maximum-scale properties.

You can set only the initial scale of the viewport—the scale of the viewport the first time the webpage is displayed. Thereafter, the user can zoom in and out unless you set user-scalable to no. Zooming by the user is also limited by the minimum-scale and maximum-scale properties.

Available on iPhone OS 1.0 and later.
```
즉, 초기 스케일은 1.0 즉 확대/축소 없는, 본 크기 그대로를 지정한다는 의미이다.


자세한 내용은 애플에서 제공하는 문서를 참조하기 바란다.[Configuring the Viewport](https://developer.apple.com/safari/resources/#//apple_ref/doc/uid/TP40006509-SW1)

> 스타일 지정

```html
<link rel="stylesheet" href="assets/css/style.css"/>
<link rel="stylesheet" href="assets/css/admin.css"/>
<style>
    .box{
        background: rgba(255,255,255,1);
        padding: 10px 20px;
        border-radius: 2px;
        box-shadow: 0px 0px 15px 5px rgba(0,0,0,0.4);
    }
</style>
```
이 부분은 `style.css`와 `admin.css`를 스타일로 지정하고 `.box`를 id로 쓰는 녀석은 저렇게 스타일하자는 의미이다.

```html
<script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<script>
(adsbygoogle = window.adsbygoogle || []).push({
google_ad_client: "ca-pub-8894073675575663",
enable_page_level_ads: true
});
</script>
```

이 부분은 링크를 따라들어가면 자바스크립트 파일을 다운받게 되는데 구글광고를 넣는 코드이다... 필요하면 읽어보시길 ^^...

> 진짜 분석시작

바디코드만,,, 약 300줄에 달하는 꽤나 복잡한 구조이다.
큰 div하나 씩 붙잡고 세부 내용을 파헤치도록 해보자.

```html
    <div class="header no-shadow">
        <div class="container-fluid">
            <div class="row">
                <div class="col-sm-4">
                    <div class="logo">
                        <h1>Facebook</h1>
                    </div>
                </div>
                <div class="col-sm-8">
                    <ul class="header-menu pull-right">
                        <li><a href="#" class="">Requests</a></li>
                        <li><a href="#" class="">Messages</a></li>
                        <li><a href="#" class="">Notifications</a></li>
                    </ul>
                </div>
            </div>
        </div>
    </div>
```

먼저 `<div class="header no-shadow">`의 세부내용을 펼쳐보자. 총 5단계의 div로 이루어져 있으며 아래 사진 부분이다. 즉, 최상단 컴포넌트를 구성한다.
![viewport 적용 전/후](/assets/images/18-09-16-facebook-clone-dashboard-header-no-shadow.PNG)   

css는 `style.css`의 `.header`과 `admin.css`의 `.no-shadow`를 적용했다.
+ div의 너비는 최대
+ 색깔은 `#2d9a40`
+ 위치는 고정이며
+ `top`, `left` 속성을 이용해 문서로부터 태그의 거리를 지정했다 [참조](http://mainia.tistory.com/3218).
+ `z-index`란 쉽게 이해하면 그림의 순서로 수치가 높을수록 앞에 위치하게 된다. (3차원 좌표로 이해하면 쉽다.)
+ `box-shadow`는 말 그대로 그림자를 의미하며 no-shadow 속성을 이용하여 그림자를 제외했다. 자세한 내용은 [MSDN](https://developer.mozilla.org/ko/docs/Web/CSS/box-shadow)을 참조하자.

```css
/* style.css */
.header {
    width: 100%;
    background: #2d9a40;
    position: fixed;
    top: 0px;
    left: 0px;
    z-index:999;
    box-shadow: 0px 5px 5px 0px rgba(0, 0, 0, 0.45);
}
/* admin.css */
.no-shadow{
    box-shadow:none;
}

```


```html

        <div class="main">
            <div class="container-fluid">
                <div class="col-sm-3 left-sidebar">
                    <ul>
                        <li><a href="./dashboard.html" class="active">News Feed</a></li>
                        <li><a href="./settings.html" class="active">Settings</a></li>
                        <li><a href="./index.html">Logout</a></li>
                    </ul>
                </div>
                <div class="col-sm-6">
                    <div class="post col-sm-12" id="post_1">
                        <div class="row post-heading">
                            <div class="col-sm-12">
                                <a href="profile.html">
                                    <img src="assets/imgs/2.jpg" class="profile-picture pull-left"/>
                                    &nbsp;
                                    <span class="post-user-name">Maninder Kaur</span><br/>
                                    &nbsp;
                                    <small class="post-date text-mute">31th March, 2017 2:49PM</small>
                                </a>
                            </div>
                        </div>
                        <div class="row post-body">
                            <div class="col-sm-12">
This is the post body. Lorem Ipsum Doler sit. Lorem Ipsum Doler sit. Lorem Ipsum Doler sit. Lorem Ipsum Doler sit.
                            </div>
                        </div>
                        <div class="row post-action">
                            <ul class="post-action-menu">
                                <li><a href="javascript:void(0);" class="text-mute" onclick="like(1);">Like</a></li>
                                <li><a href="javascript:void(0);" class="text-mute" onclick="share(1);">Share</a></li>
                                <li><a href="javascript:void(0);" class="text-mute" onclick="comment(1);">Comment</a></li>
                                <li class="pull-right"><a href="#" class="text-mute"><span id="post_like_count_1">2142</span> Likes</a></li>
                                <li class="pull-right"><a href="#" class="text-mute"><span id="post_comment_count_1">2172</span> Comments</a></li>
                                <li class="pull-right"><a href="#" class="text-mute"><span id="post_share_count_1">200</span> Shares</a></li>
                            </ul>
                        </div>
                    </div>
                    <div class="post col-sm-12" id="advertisement_1" style="min-height:250px">
                    <script async src="//pagead2.googlesyndication.com/pagead/js/adsbygoogle.js"></script>
<!-- Github Facebook -->
<ins class="adsbygoogle"
     style="display:block"
     data-ad-client="ca-pub-8894073675575663"
     data-ad-slot="3929924245"
     data-ad-format="auto"></ins>
<script>
(adsbygoogle = window.adsbygoogle || []).push({});
</script>
                    </div>
                    <div class="post col-sm-12" id="post_2">
                        <div class="row post-heading">
                            <div class="col-sm-12">
                                <a href="profile.html">
                                    <img src="assets/imgs/3.jpg" class="profile-picture pull-left"/>
                                    &nbsp;
                                    <span class="post-user-name">Divyanshu Gupta</span><br/>
                                    &nbsp;
                                    <small class="post-date text-mute">31th March, 2017 2:49PM</small>
                                </a>
                            </div>
                        </div>
                        <div class="row post-body">
                            <div class="col-sm-12">
This is the post body. Lorem Ipsum Doler sit. Lorem Ipsum Doler sit. Lorem Ipsum Doler sit. Lorem Ipsum Doler sit.

This is the post body. Lorem Ipsum Doler sit. Lorem Ipsum Doler sit. Lorem Ipsum Doler sit. Lorem Ipsum Doler sit.

This is the post body. Lorem Ipsum Doler sit. Lorem Ipsum Doler sit. Lorem Ipsum Doler sit. Lorem Ipsum Doler sit.
                            </div>
                        </div>
                        <div class="row post-action">
                            <ul class="post-action-menu">
                                <li><a href="javascript:void(0);" class="text-mute" onclick="like(2);">Like</a></li>
                                <li><a href="javascript:void(0);" class="text-mute" onclick="share(2);">Share</a></li>
                                <li><a href="javascript:void(0);" class="text-mute" onclick="comment(2);">Comment</a></li>
                                <li class="pull-right"><a href="#" class="text-mute"><span id="post_like_count_2">2142</span> Likes</a></li>
                                <li class="pull-right"><a href="#" class="text-mute"><span id="post_comment_count_2">2172</span> Comments</a></li>
                                <li class="pull-right"><a href="#" class="text-mute"><span id="post_share_count_2">200</span> Shares</a></li>
                            </ul>
                        </div>
                    </div>
                    <div class="post col-sm-12" id="post_3">
                        <div class="row post-heading">
                            <div class="col-sm-12">
                                <a href="profile.html">
                                    <img src="assets/imgs/5.jpg" class="profile-picture pull-left"/>
                                    &nbsp;
                                    <span class="post-user-name">Sourabh Thakur</span><br/>
                                    &nbsp;
                                    <small class="post-date text-mute">31th March, 2017 2:49PM</small>
                                </a>
                            </div>
                        </div>
                        <div class="row post-body">
                            <div class="col-sm-12">
This is the post body. Lorem Ipsum Doler sit. Lorem Ipsum Doler sit. Lorem Ipsum Doler sit. Lorem Ipsum Doler sit.
                            </div>
                        </div>
                        <div class="row post-action">
                            <ul class="post-action-menu">
                                <li><a href="javascript:void(0);" class="text-mute" onclick="like(3);">Like</a></li>
                                <li><a href="javascript:void(0);" class="text-mute" onclick="share(3);">Share</a></li>
                                <li><a href="javascript:void(0);" class="text-mute" onclick="comment(3);">Comment</a></li>
                                <li class="pull-right"><a href="#" class="text-mute"><span id="post_like_count_3">2142</span> Likes</a></li>
                                <li class="pull-right"><a href="#" class="text-mute"><span id="post_comment_count_3">2172</span> Comments</a></li>
                                <li class="pull-right"><a href="#" class="text-mute"><span id="post_share_count_3">200</span> Shares</a></li>
                            </ul>
                        </div>
                    </div>
                    <div class="post col-sm-12" id="post_4">
                        <div class="row post-heading">
                            <div class="col-sm-12">
                                <a href="profile.html">
                                    <img src="assets/imgs/4.jpg" class="profile-picture pull-left"/>
                                    &nbsp;
                                    <span class="post-user-name">Akshima</span><br/>
                                    &nbsp;
                                    <small class="post-date text-mute">31th March, 2017 2:49PM</small>
                                </a>
                            </div>
                        </div>
                        <div class="row post-body">
                            <div class="col-sm-12">
This is the post body. Lorem Ipsum Doler sit. Lorem Ipsum Doler sit. Lorem Ipsum Doler sit. Lorem Ipsum Doler sit.
                            </div>
                        </div>
                        <div class="row post-action">
                            <ul class="post-action-menu">
                                <li><a href="javascript:void(0);" class="text-mute" onclick="like(4);">Like</a></li>
                                <li><a href="javascript:void(0);" class="text-mute" onclick="share(4);">Share</a></li>
                                <li><a href="javascript:void(0);" class="text-mute" onclick="comment(4);">Comment</a></li>
                                <li class="pull-right"><a href="#" class="text-mute"><span id="post_like_count_4">2142</span> Likes</a></li>
                                <li class="pull-right"><a href="#" class="text-mute"><span id="post_comment_count_4">2172</span> Comments</a></li>
                                <li class="pull-right"><a href="#" class="text-mute"><span id="post_share_count_4">200</span> Shares</a></li>
                            </ul>
                        </div>
                    </div>
                    <div class="post col-sm-12" id="post_5">
                        <div class="row post-heading">
                            <div class="col-sm-12">
                                <a href="profile.html">
                                    <img src="assets/imgs/1.jpg" class="profile-picture pull-left"/>
                                    &nbsp;
                                    <span class="post-user-name">Shubham Kumar</span><br/>
                                    &nbsp;
                                    <small class="post-date text-mute">31th March, 2017 2:49PM</small>
                                </a>
                            </div>
                        </div>
                        <div class="row post-body">
                            <div class="col-sm-12">
This is the post body. Lorem Ipsum Doler sit. Lorem Ipsum Doler sit. Lorem Ipsum Doler sit. Lorem Ipsum Doler sit.
                            </div>
                        </div>
                        <div class="row post-action">
                            <ul class="post-action-menu">
                                <li><a href="javascript:void(0);" class="text-mute" onclick="like(5);">Like</a></li>
                                <li><a href="javascript:void(0);" class="text-mute" onclick="share(5);">Share</a></li>
                                <li><a href="javascript:void(0);" class="text-mute" onclick="comment(5);">Comment</a></li>
                                <li class="pull-right"><a href="#" class="text-mute"><span id="post_like_count_5">2142</span> Likes</a></li>
                                <li class="pull-right"><a href="#" class="text-mute"><span id="post_comment_count_5">2172</span> Comments</a></li>
                                <li class="pull-right"><a href="#" class="text-mute"><span id="post_share_count_5">200</span> Shares</a></li>
                            </ul>
                        </div>
                    </div>
                </div>
                <div class="col-sm-3 chat-users">
                    <div class="row">
                        <h3>Chat</h3>
                    </div>
                    <div class="row">
                        <div class="col-sm-12 chat-user online">
                            <a href="#">
                                <img src="assets/imgs/1.jpg" class="pull-left"/>
                                &nbsp;
                                Shubham Kumar
                            </a>
                        </div>
                        <div class="col-sm-12 chat-user online">
                            <a href="#">
                                <img src="assets/imgs/2.jpg" class="pull-left"/>
                                &nbsp;
                                Maninder Kaur
                            </a>
                        </div>
                        <div class="col-sm-12 chat-user online">
                            <a href="#">
                                <img src="assets/imgs/3.jpg" class="pull-left"/>
                                &nbsp;
                                Divyanshu Gupta
                            </a>
                        </div>
                        <div class="col-sm-12 chat-user">
                            <a href="#">
                                <img src="assets/imgs/4.jpg" class="pull-left"/>
                                &nbsp;
                                Akshima
                            </a>
                        </div>
                        <div class="col-sm-12 chat-user online">
                            <a href="#">
                                <img src="assets/imgs/5.jpg" class="pull-left"/>
                                &nbsp;
                                Sourabh Thakur
                            </a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="footer no-shadow">
            <div class="container-fluid">
                <div class="row">
                    <div class="col-sm-12">
                        &copy; Facebook 2017.
                    </div>
                </div>
            </div>
        </div>
        <script>
            function like(id){
                var elem = document.getElementById("post_like_count_"+id);
                var count = parseInt(elem.innerHTML);
                elem.innerHTML = count+1;
                highlight(elem);
            }
            function share(id){
                var elem = document.getElementById("post_share_count_"+id);
                var count = parseInt(elem.innerHTML);
                elem.innerHTML = count+1;
                highlight(elem);
            }
            function comment(id){
                var elem = document.getElementById("post_comment_count_"+id);
                var count = parseInt(elem.innerHTML);
                elem.innerHTML = count+1;
                highlight(elem);
            }
            function highlight(elem){
                elem.style.color = "red";
                elem.parentElement.parentElement.style.transform="scale(1.5)";
                setTimeout(function(){
                    elem.style.color="";
                    elem.parentElement.parentElement.style.transform="scale(1)";
                },300);
            }
        </script>
    </body>
```



최상단(녹색) DIV를 분석한 결과 생각보다 구조가 복잡하게 되어있다.





## vue

### directive
:  VUE에서 제공하는 특수속성으로 `v-` 라는 접두어가 붙어있으며 렌더링된 DOM에 특수한 반응형 동작을 한다. if문, for문, eventListener, 데이터 최신화 등 예제를 볼 수 있다.

### component
:  컴포넌트란 본질적으로 미리 정의된 옵션을 가진 Vue 인스턴스. 컴포넌트를 정의 후 인스턴스를 생성하여 사용한다.





**문제:**   
근거리 통신망의 프로토콜에서 매체 액세스 제어계층(MAC: Media Access Control Layer)의 역할을 설명하시오.
{: .notice--info}   

**정답**     
여러 개의 스테이션이 공통의 전송로로 데이터를 송출할 때의 경쟁을 제어하고,  또한 전송로의 이상 유무를 검출한다.
{: .notice--warning}   
