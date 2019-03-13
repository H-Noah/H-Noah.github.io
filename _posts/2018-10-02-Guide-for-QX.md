---
title: "Qooxdoo 사용 가이드"
permalink: /docs/Guide-For-QX/
last_modified_at: 2018-10-02T15:58:49-04:00
excerpt: "Qooxdoo 공식문서를 번역한 것입니다."
toc: true
classes: wide
author_profile: false
sidebar:
  title: "Order List"
  nav: sidebar-sample
---



## Getting Started

### Getting Started

이 섹션에서는 코드 작성을 시작하기 위한 개발환경 설정 방법과 사용자의 Needs에 따른 qooxdoo 패키지 선택에 도움을 줄 자료를 제공한다.

>qx.Website  

[qx.Website](https://www.qooxdoo.org/current/pages/website.html)는 다른 자바스크립트 라이브러리와 비슷하게 HTML page에서 하나 또는 그이상의 `.js`파일을 포함하여 deploy하는 low-level package이다. 이 내용은 DOM과 BOM 추상화, 크로스 브라우징 이벤트핸들링, 셀렉터 엔진, qooxdoo class system의 stripped down version 등을 포괄한다.


## Core

## Desktop

### Overview

> Widget

위젯은 qooxdoo의 그래픽 사용자 인터페이스 (GUI)의 기본 구성 요소입니다. 버튼, 레이블 또는 창과 같은 각 GUI 구성 요소는 위젯이며 기존 사용자 인터페이스 내에 배치 될 수 있습니다. 각각의 특정 유형의 위젯은 그 자체로 [LayoutItem](http://www.qooxdoo.org/5.0.2/api/#qx.ui.core.LayoutItem)의 서브 클래스인 [위젯](http://www.qooxdoo.org/5.0.2/api/#qx.ui.core.Widget)의 해당 서브 클래스에 의해 제공됩니다.

위젯은 쉽게 하위 클래스로 만들어 Custom 위젯을 만들 수 있습니다. 이 클래스의 전체 레이아웃 처리 및 자식 처리는 "protected"로만 사용할 수 있습니다. 필요한 경우 일부 공개 API를 추가 할 수 있습니다.

LayoutItem을 확장하는 또 다른 프레임 워크 클래스는 [Spacer](http://www.qooxdoo.org/5.0.2/api/#qx.ui.core.Spacer)입니다. 스페이서는 빈 영역으로 나중에 대체되거나 특정 동적 UI 설계에서 유연한 부분으로 명시적으로 대체되는 temporary placeholder로 사용될 수 있습니다.

인터페이스를 구성하려면 위젯을 서로 삽입하는 것이 일반적입니다. 각 하위 항목은 상위 항목이 차지하는 화면 영역 내에 표시됩니다. 계층적 구조는 특정 영역을 숨기거나 표시하는 데에도 사용됩니다. 예를 들어, 부모를 숨기는 것이 자녀를 숨기는 것을 의미합니다. 또 다른 예는 위젯이 삭제 될 때 해당 위젯에 포함 된 모든 하위 위젯이 자동으로 삭제된다는 것입니다.

> Composite

언급한 바와 같이 일반적인 위젯 위에 몇 문장은 Children을 관리하는 public Method가 없습니다. 이는 일반적인 위젯을 상속에 사용할 수있게합니다. 응용 프로그램에서 구조 작성을 허용하기 위해 Composite이 작성되었습니다.

[Composite](http://www.qooxdoo.org/5.0.2/api/#qx.ui.container.Composite)은 위젯을 확장하고 위젯의 전체 child 및 레이아웃 관리를 공개합니다. 일반적으로 다른 위젯의 컨테이너로 사용됩니다. 자식은 add (), remove () 등의 메서드를 통해 관리 할 수 있습니다. 응용 프로그램 코드에서는 복합체를 사용하여 인터페이스를 구조화합니다.

> Roots

위젯의 특별한 카테고리는 루트 위젯입니다. 이것들은 기본적으로 고전적인 DOM과 qooxdoo 위젯 시스템 사이를 연결합니다. 각 사례의 요구 사항에 대해 개별적으로 조정할 다양한 유형의 방법이 있습니다.(?)

우선, 모든 응용 프로그램 개발자는 응용 프로그램을 독립실행형으로 설정해야하는지 결정해야합니다.(e.g 최소한의 HTML 세트로 작업하거나 기존 웹 페이지에 통합되거나) 독립형 애플리케이션 개발자는 일반적으로 UI 툴킷에 페이지 레이아웃을 제어하는 ​​데 문제가 없지만 qooxdoo를 기존 웹 페이지 레이아웃에 통합하는 데는 효과가 없습니다.

독립실행 형 응용 프로그램은 일반적으로 실제로는 슬림화 된 HTML 집합을 사용합니다 (사실 관례적인 index.html 파일은 응용 프로그램 코드를 로드하는 wrapper로만 사용됩니다). 일반적으로 CSS 파일을 포함하지 않으며 빈 본문 요소가있는 경우가 많습니다. 실제로 머리글, 바닥 글 등의 간단한 요소도 위젯을 사용하여 만들 수 있습니다 (국제화, 테마 등의 일반적인 qooxdoo 기능을 활용하여).

## Mobile

## Website

## Server



## Tooling

### SDK Requirements

qooxdoo는 SDK의 형태로 유저 친화적이며 플랫폼 독립적인 tool-chain을 제공한다. [qx.Desktop](http://www.qooxdoo.org/current/pages/desktop.html)과 [qx.Mobile](http://www.qooxdoo.org/current/pages/mobile.html) 다운로드 함께 진행한다. 이 컴포넌트들은 qooxdoo 응용프로그램들을 작성하고 개발하는데 필요한 컴포넌트들이다. [qx.Desktop](http://www.qooxdoo.org/current/pages/desktop.html)과 [qx.Mobile](http://www.qooxdoo.org/current/pages/mobile.html)는 pre-build libraries이므로 SDK가 필요하지 않다.

> qx.Desktop tutorial의 download script 링크 만료....

### Python

tool chain은 Python(2.x) 설치만을 요구합니다. 하지만 따로 Python 지식을 필요로하지는 않으며 내부적으로 사용될 뿐입니다. 아래 절차에 따라 매우 쉽게 설치할 수 있습니다.

> Windows  

[Active python](https://www.activestate.com/activepython/downloads)을 이용하여 쉽게 설치할 수 있습니다. (따로 설정을 할 필요도 없습니다.) 만약, 파이썬 공식홈페이지에서 설치할 경우 수동설정이 필요할 수 있습니다.

> Windows Shells Interop

 Windows에서 사용할 수 있는 다양한 셸 관련 단어 및 상호 운영방법에 대한 설명입니다. 우리는 CMD창과 Powershell에서 SDK를 테스트할 수 있습니다. 등등 크게 쓸모없는 이야기.

### Hello World

이번 튜토리얼의 목적은 빠르게 작업하며 높은 수준의 정보를 제공하여 SDK 작업에 익숙해지는 것입니다. 이를 위해 최소한의 데스크톱 응용프로그램을 만들 것입니다.

> Setup the Framework

위의 설정을 모두 따랐다면 완료입니다.

> Create your Application

SDK `tool/bin`경로의 플랫폼 독립적인 `create-application.py`스크립트 실행을 통해 애플리케이션을 쉽게 세팅할 수 있습니다. 명시한 폴더에 스켈레톤 애플리케이션을 만들어주며 qooxdoo 버전에 따라 자동으로 Configuration 됩니다.

 개발의 나머지 부분이 플랫폼과 독립적이라도 `create-application.py`스크립트를 이용하여 새로운 스켈레톤을 만들기 위해 초기 플랫폼 종속단계를 따라야합니다.

 > Windows Setting

`cmd` 혹은 `powershell`을 열어 현재디렉토리에 `custom`이라는 이름을 가진 어플리케이션을 제작합니다. 아래 경로에서 명령어를 입력합니다.    

```cmd
qooxdoo-5.0.2-sdk\tool\bin\create-application.py --name=custom
```

> Run Your Application

이제 애플리케이션 셋업이 완료되었습니다. 브라우저에서 열 수 있는 버전을 생성해봅시다. 새로 생성된 디렉토리로 이동하여 아래 명령어를 통해 자동빌드 프로세스를 시작합니다.

```cmd
cd custom
generate.py source-all
```    

**팁:** Windows 이외의 운영체제인 경우 `./generate.py source-all` 명령어를 입력하면 됩니다.


이제 index.html 파일을 실행하면 생성된 버튼을 볼 수 있습니다.

응용 프로그램을 개발할 때 웹 서버를 통해 응용 프로그램을 실행하는 것이 좋습니다. 따라서 브라우저에서 직접 source / index.html을 여는 대신 쉘에서 다음 명령을 실행하여 로컬 미니 웹 서버를 시작할 수 있습니다.    

```cmd
generate.py source-server
```   

명령 출력을 보면 웹 서버에서 원본 응용 프로그램을 사용할 수있는 URL을 알 수 있습니다 (웹 브라우저의 위치 필드에 복사하여 붙여넣기만 하면됩니다). 완료되면 셸 창에서 Ctrl-C를 눌러 서버 프로세스를 종료합니다.

> Write Application Code

`source/class` 경로에는 application의 모든 class가 포함되어있습니다. 새롭게 생성된 application을 시작할 때, application logic을 위한 단일파일(application.js)만이 존재합니다. 이것을 원하는 IDE로 열어봅니다.    

`main()`함수는 스켈레톤 앱의 전체 코드를 포함합니다. 이전에 qooxdoo 프로그래밍을 하지 않았더라도 코드가 무엇을 의미하는지 이해할 수 있을겁니다. 코드와 친숙해지고 변경해보세요.   

변경사항을 보기위해서는 브라우저를 새로고침하면 됩니다. 개방 중에는 `Source`버전의 앱을 다시 생성할 필요가 없습니다. 나중에 새 클래스를 생성하거나 클래스간의 종속성이 변경되는 경우에만 새로 빌드하면 됩니다. 이렇게 하기위해서는 브라우저를 새로고침 하기 전에 `generate.py source-all` 명령어를 실행하면 됩니다.

> debugging

  새롭게 만들어진 `application.js`에서 아래 코드를 볼 수 있습니다.

  ```javascript
  if (qx.core.Environment.get("qx.debug"))
  {
    qx.log.appender.Native;
    qx.log.appender.Console;
  }
  ```

  이 코드는 응용 프로그램의 작업에 대한 정보를 캡처하고 인쇄하는 두 가지 "로깅"방법을 제공합니다.

  `qx.log.appender.Native`는 가능한 경우 클라이언트의 기본 로깅기능을 사용합니다.(ex. 크롬의 경우 f12로 개발자도구를 사용한다) 만약, 브라우저에서 도구를 제공하지 않는 경우 F7키를 눌러 디버깅할 수 있는 창을 제공합니다.

  소위 "디버그"변형에 두 로깅 클래스를 포함하는 이유는 다음 섹션에서 자세히 설명합니다. 앱의 개발 버전 (예 : '소스'버전)에서만 로깅을 사용하도록 설정합니다. 배포 할 앱의 최종 버전에서 자동으로 사용 중지됩니다.

 > Deployment

qooxdoo 앱의 개발버전을 `source`버전이라고 부르며 앱의 배포 버전을 `build`버전이라고 합니다. 후자는 아래 명령어를 통해 생성됩니다.     

```cmd
generate.py build
```

성공적으로 빌드가 완료된 후 브라우저가 새로 생성된 빌드폴더에서 `index.html`을 열도록 하면 됩니다. 이 배포버전의 앱과 이전의 `source`버전 사이에는 차이가 없을지라도 **it should have started up faster.(WHAT MEANS?)**.   

"소스"버전과 달리 수많은 수정되지 않은 JavaScript 파일과 함께 "빌드"버전은 최적화 된 단일 JavaScript 파일만 로드하면 됩니다.   

Application class에서 이러한 `custom build`를 수동으로 만드는 것은 매우 지루하고 복잡한 작업이었습니다. 실제로 대부분의 다른 JS 라이브러리는 이 작업을 자동화하는 작업을 내장으로 지원합니다. 앱을 빌드하면 불필요한 공백 및 주석을 제거하고, 코드를 최적화 및 재구성하며 JS링커를 이용하여 애플리케이션에 필요한 클래스만 포함하고 더 많은 개선 및 최적화도 수행합니다.   

개발할 때만 유용한(e.g printing out informative warnings or coding hints) 많은 디버깅 코드들은 `Build`가 생성되며 제거됩니다. (해석불필요) Just like the logging code in the section above, you can put arbitrary code into such "variants", which may then be automatically removed during "conditional compilation" of the build process. This lets you receive information on your app when you're developing it, but removes this for your final code, so your end users don't see it.

> API Reference

qooxdoo는 Javadoc 또는 JSDoc 주석과 유사한 인라인 주석을 지원합니다. 그들은 자바스크립트와 qooxdoo 특정 기능을 허용하고 / ** 당신의 코멘트 * /처럼 보입니다.

이러한 명령어에서 완전한 대화식 API 참조를 생성 할 수 있습니다.
```cmd
generate.py api
```

[API 뷰어 응용 프로그램](http://www.qooxdoo.org/current/pages/application/apiviewer.html)을 시작하려면 브라우저에서 새로 만든 api 폴더에서 index.html을 엽니다. 여기에는 응용 프로그램 클래스와 프레임 워크 클래스에 대한 완벽하게 상호 링크되고 검색 가능한 문서가 포함됩니다.


> Unit Testing


응용 프로그램의 `source / class` 폴더에있는 `test / DemoTest.js` 파일을 보셨을 것입니다. 이 클래스는 응용 프로그램에 대한 "단위 테스트"를 정의하는 방법을 보여줍니다. qooxdoo는 자체 유닛 테스트 프레임 워크와 함께 제공되며, 추가 소프트웨어 설치가 필요하지 않습니다. 다음 명령을 실행하기 만하면됩니다.

```cmd
generate.py test
```

브라우저에서 새로 생성 된 최상위 테스트 폴더에서 index.html을 엽니 다. [Testrunner 응용 프로그램](http://www.qooxdoo.org/current/pages/application/testrunner.html)을 사용하면 응용 프로그램 네임 스페이스 아래에서 테스트를 선택하고 실행할 수 있습니다.

![testrunner](http://www.qooxdoo.org/current/_images/testrunner1.png)

사용자 정의 응용 프로그램 코드를 계속 확장하면서 오히려 고급 단위 테스트 항목을 건너 뛸 수 있습니다. 테스트 주도 개발과 고유 한 단위 테스트에 관심이있는 경우 해당 [단위 테스트 설명서](http://www.qooxdoo.org/current/pages/development/unit_testing.html)를 참조하십시오.

    ....  http://www.qooxdoo.org/current/pages/tool/getting_started.html 이어가기..
