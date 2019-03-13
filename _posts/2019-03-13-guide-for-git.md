---
title: "[번역]PRO GIT, GIT사용가이드"
permalink: docs/pro-git
last_modified_at: 2019-03-13T18:58:49-04:00
toc: true
excerpt: "PRO GIT 책의 내용을 번역/요약한 포스트"
classes: wide
thumbnail: "/assets/images/github-logo.png"
author_profile: false
sidebar:
  title: "Order List"
  nav: sidebar-sample
tags:
  - "guide"  
  - "documentation"  
  - "GIT"  
---



## 시작하기


Git의 핵심은 뭘까? 이 질문은 Git을 이해하는데 굉장히 중요하다. Git이 무엇 이고 어떻게 동작하는지 이해한다면 쉽게 Git을 효과적으로 사용할 수 있다. Git을 배우려면 Subversion이나 Perforce 같은 다른 VCS를 사용하던 경험을 버려야 한다. `Git은` 미묘하게 달라서 다른 VCS에서 쓰던 개념으로는 헷갈린다. 사용자 인터페이스는 매우 비슷하지만, `정보를 취급하는 방식이 다르다.` 이런 차이점을 이해하면 Git을 사용하는 것이 어렵지 않다.

<!--more-->



### GIT의 목표
 - 빠른 속도
 - 단순한 구조
 - 비선형적 개발(수천개의 동시브랜치)
 - Linux 같은 대형프로젝트에서 사용가능

### 스냅샷

<mark>SVN과 GIT의 가장 큰 차이점은 데이터를 다루는 방법</mark>이다. 

![SVN](/assets/images/git1.PNG)
> SVN은 각 파일의 변화를 시간순으로 관리하며 파일들의 집합을 관리한다.

![GIT](/assets/images/git2.PNG)
> 반면 GIT은 데이터를 아주 작은 파일 시스템 스냅샷으로 취급하며 데이터를 `스냅샷의 스트림`처럼 취급한다.


### 로컬의 장점

대부분의 명령을 로컬에서 실행하며 로컬파일과 데이터만 사용하므로 빠른 속도를 보여준다.

### 세 가지 상태

`이 부분은 중요하므로 집중해서 읽어야한다` GIT은 파일을 Commited, Modified, Staged 이렇게 세 가지 상태로 관리한다. 

![GIT3](/assets/images/git3.PNG)


<ul>
    <li>상태
        <ol>
            <li>Committed: 데이터가 로컬 데이터베이스에 안전하게 저장됨</li>
            <li>Modified: 수정한 파일을 로컬데이터베이스에 아직 커밋하지 않음</li>
            <li>Staged: 현재 수정한 파일을  커밋할 것이라고 표기한 것</li>
        </ol>
    </li>
    <li>폴더
        <ol>
            <li>.git directory: repository, 프로젝트의 메타데이터와 객체데이터베이스를 저장하는 곳</li>
            <li>Working directory: 프로젝트의 특정 버전을 checkout한 것</li>
            <li>Staging Area: GIT 디렉토리에 존재하는, 곧 커밋할 파일에 대한 정보를 저장하는 파일</li>
        </ol>
    </li>
    <li>하는 일
        <ol>
            <li>워킹 디렉토리에서 파일을 수정한다. </li>
            <li>Staging Area에 있는 파일을 Stage해서 커밋하리 스냅샷을 만든다. <mark>git add .</mark> </li>
            <li>Staging Area에 있는 파일을 커밋해서 스냅샷을 만든다. <mark>git commit -m "message"</mark></li>
        </ol>
    </li>
</ul>

## GIT의 기초

GIT 저장소를 만드는 방법은 크게 두 가지이다. 첫 째는 기존 프로젝트를 GIT 저장소로 만드는 것이고 둘 째는 다른 서버에 있는 저장소를 Clone하는 것이다.

### 기존 디렉토리를 Git 저장소로 만들기

기존 프로젝트를 git으로 관리하고 싶은 경우 cmd 혹은 git bash를 이용하여 해당 경로로 이동한 뒤 아래 명령어를 입력한다.

```
git init
```

위 명령어는 `.git`이라는 하위 디렉토리를 생성하며 저장소를 유지하기 위한 기본 파일들이 들어간다.
이제 기존 파일들을 관리하기 위해 staging 한 뒤, 커밋한다.

```
git add .
git commit -m "first commit"
```

### 기존 저장소를 clone하기

다른 프로젝트에 참여하거나 Git 저장소를 복사하고 싶은 경우 사용한다

```
git clone "URL"
```

### 수정하고 저장소에 저장하기

이제 하나의 repository가 생겼다고 가정하자. 워킹디렉토리의 모든 파일은 크게 Tracked(관리대상)와 Untracked(관리제외)로 나뉜다. Untracked 파일은 워킹 디렉토리에 있는 파일 중 스냅샷에도 Staging Area에도 포함되지 않은 파일이다. 처음 저장소를 Clone한 경우 모든 파일은 Tracked이면서 Unmodified상태이다. 

<ul>
    <li>워킹디렉토리
        <ol><font color="red">Tracked(관리대상) files</font>
            <li>Modified: 수정함</li>
            <li>Unmodified: 수정하지 않음</li>
            <li>Staged: 커밋으로 저장소에 기록할 것</li>
        </ol>
    </li>    
</ul>

![GIT4](/assets/images/git4.PNG)


<mark>이 이상의 커밋관련 정보는 불필요하다고 판단하여 생략합니다.</mark>

### 파일 무시하기

보통 로그파일이나 빌드시스템이 자동으로 생성한 파일은 Git으로 관리할 필요가 없다. 이런 파일들을 무시하려면 `.gitignore`파일을 만들고 그 안에 무시할 패턴을 적는다.

```
$cat .gitignore
*.[oa]
*~
```
`*.[oa]`는 확장자가 `.o`나 `.a`인 파일을 git이 무시하라는 의미이고 `*~`는 ~로 끝나는 모든 파일을 무시하라는 것이다.

> .gitignore파일은 보통 처음에 만들어 두는 것이 편하다.

그래야 git 저장소에 커밋하고 싶지 않은 파일을 실수로 커밋하는 일을 방지할 수 있다.
.gitignore파일에 입력하는 패턴은 아래 규칙을 따른다.

<ul>
    <li>gitignore 규칙
        <ol>
            <li> 아무것도 없는 라인이나, #로 시작하는 라인은 무시한다. 
</li>
            <li>표준 Glob 패턴을 사용한다. </li>
            <li>슬래시(/)로 시작하면 하위 디렉토리에 적용되지(Recursivity) 않는다. </li>
            <li>디렉토리는 슬래시(/)를 끝에 사용하는 것으로 표현한다.  </li>
            <li>느낌표(!)로 시작하는 패턴의 파일은 무시하지 않는다. </li>
        </ol>
    </li>    
</ul>

> GitHub은 다양한 프로젝트에서 자주 사용하는 .gitignore 예제를 관리하고 있다.  https://github.com/github/gitignore 를 참조하면 적당한 예제를 찾을 수 있다.


### Staged와 Unstaged 상태의 변경 내용 비교

단순히 파일이 변경됨이 아니라 어떤 내용이 변경되었는지 확인하기 위해서는 아래 명령어를 이용한다.
```
git diff
```

<mark>하지만 CMD보다는 tool을 이용하는 것이 낫다.</mark>

### [중요]파일 삭제하기 

 Git에서 파일을 제거하려면 `git rm`명령으로 Tracked된 파일을 삭제한 후에(정확히는 Staging Aread에서 삭제하는 것) 커밋해야 한다. 이 명령은 워킹 디렉토리에 있는 파일도 실제로 삭제하는 것이다.

만약 Git 없이 그냥 파일을 삭제하고 `git status` 명령으로 상태를 확인하면 `Changed for commit` 즉, Unstaged에 속한다는 것을 확인할 수 있다.

> Git 없이 파일삭제 후, git status 명령으로 상태를 확인

```
$ rm grit.gemspec
$ git status

On branch master
Changes not staged for commit:
(use "git add/rm <file>..." to update what will be committed)
(use "git checkout -- <file>..." to discard changes in working directory)
    
deleted:    grit.gemspec

no changes added to commit (use "git add" and/or "git commit -a")
```

> git rm 명령어로 삭제 후, git status 명령으로 상태를 확인

```
$ git rm grit.gemspec
rm 'grit.gemspec' 
$ git status 
On branch master
Changes to be committed:
(use "git reset HEAD <file>..." to unstage)

    deleted:    grit.gemspec
```

이제 커밋하면 <mark>파일은 삭제되고 더이상 추적하지 않는다</mark>. 이미 파일을 수정했거나 Index에 추가했다면 -f 옵션을주어 강제로 삭제해야 한다. 

또, Staging Area에서만 제거하고 워킹 디렉토리에 있는 파일은 지우지 않을 수도 있다. 즉, 하드디스크에 있는 파일은 그대로 두고 Git만 추적하지 않게한다.

```
git rm --cached README
```

### 커밋 히스토리 조회하기

> TOOL을 사용하도록 하자


### 되돌리기(중요, git commit --amend)



> Git을 사용하면 우리가 한 실수를 복구하지 못할 것은 거의 없지만 __되돌린 것은 복구할 수 없다.__ <mark>주의하세요</mark>

완료한 커밋을 수정해야 할 필요가 있을 때, `--amend` 옵션을 사용한다.

```
git commit --amend
```
이 명령은 Staging Area를 사용하여 커밋한다. 아래처럼 사용하며 아래의 경우 두 번째 커밋은 첫 번쨰 커밋을 덮어쓰기때문에 하나의 커밋만 올라간다.

```
$git commit -m "initial commit"
$git add forgotten_file
$git commit --amend
```

### 파일 상태를 Unstage로 변경하기 (git reset HEAD~)

다음은 Staging Area와 워킹 디렉토리 사이를 넘나드는 방법을 설명한다. 예를 들어, 파일을 두 개 수정하고서 따로따로 커밋하려고 했으나 `git add .`를 실행해버렸다고 가정하자. 이제 둘 중 하나를 꺼내보겠다. 현재 상태는 아래와 같다.

```
$ git add . 
$ git status 
On branch master 
Changes to be committed:  
(use "git reset HEAD <file>..." to unstage)
    renamed:        README.md -> README    
    modified:       benchmarks.rb
```

`git reset HEAD <file>...` 메시지를 보면 알 수 있듯이 저 명령어로 Unstaged 상태로 변경할 수 있다.

```
$ git reset HEAD benchmarks.rb 
Unstaged changes after reset:
M benchmarks.rb 
$ git status
On branch master 
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

    renamed:    README.md -> README

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
  
    modified:   benchmarks.rb
```

낯설지만 잘 동작한다. benchmark.rb파일은 Unstaged상태가 되었다.

> git reset 명령을 --hard 옵션과 함께 사용하면 워킹 디렉토리의 파일이 수정돼서 을 조심해야 한다. --hard 옵션만 사용하지 않는다면 git reset 명령은 Staging Area의 파일만 조작하기 때문에 위험하지 않다.

더욱 자세한 정보는 7장에서 설명한다.

### [비추천]Modified 파일 되돌리기. (git checkout)

benchmark.rb 파일을 수정하고나서 다시 되돌리고 싶은 경우, 즉, 최근 커밋된 버전으로 되돌리는 방법을 소개한다. 현재상태는 아래와 같다

```
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)
    modified:   benchmarks.rb
```

복원시키기 위해 아래 명령어를 입력한다.

```
$ git checkout -- benchmarks.rb 
$ git status
 On branch master Changes to be committed:
   (use "git reset HEAD <file>..." to unstage)

    renamed:    README.md -> README
```

> git checkout -- [file] 명령은 꽤 위험한 명령이라는 것을 알아야 한다. 원래 파일로 덮어썼기 때문에 수정한 내용은 전부 사라진다. 수정한 내용이 진짜 마음에 들지 않을 때에만 
사용하자..

변경한 내용을 쉽게 버릴수는 없고 하지만 당장은 되돌려야만 하는 상황이라면 Stash와 Branch를 사용하자. Chapter 3 에서 다루는 이 방법들이 훨씬 낫다. Git으로 커밋한 모든 것은 언제나 복구할 수 있다. 삭제한 브랜치에 있었던 것도, --amend 옵션으로 다시 커밋한 것도 복구할 수 있다(자세한 것은 “데이터복구” 에서 다룬다). 하지만 커밋하지 않고 잃어버린 것은 절로 되돌릴 수 없다.


### 리모트 저장소

리모트 저장소는 인터넷이나 네트워크 어딘가에 있는 저장소를 말한다. 즉, 다른 사람들과 함께 일한다는 것은 리모트 저장소를 관리하면서 데이터를 거기에 Push 하고 Pull 하는 것이다

### 리모트 저장소를 Pull하거나 fetch 하기

리모트 저장소에서 데이터를 가져오려면 아래와 같이 실행한다.

```
$git fetch [remote-name]
```
위 명령은 로컬에는 없지만, 리모트 저장소에는 있는 데이터를 모두 가져온다. 그러면 리모트 저장소의 모든 브랜치를 로컬에서 접근할 수 있어서 언제든지 Merge 하거나 내용을 살펴볼 수 있다.


## GIT BRANCH

모든 버전 관리 시스템은 브랜치를 지원한다. 개발을 하다 보면 코드를 여러 개로 복사해야 하는 일이 자주 생긴다. <mark>코드를 통째로 복사하고 나서 원래 코드와는 상관없이 독립적으로 개발을 진행할 수 있는데, 이렇게 독립적으로 개발하는 것이 브랜치</mark>다. 사람들은 브랜치 모델이 Git의 최고의 장점이라고, Git이 다른 것들과 구분 되는 특징이라고 말한다. 당최 어떤 점이 그렇게 특별한 것일까. Git의 브랜치는 매우 가볍다. 순식간에 브랜치를 새로 만들고 브랜치 사이를 이동할 수 있다. <mark>다른 버전 관리 시스템과는 달리 Git은 브랜치를 만들어 작업하고 나중에 Merge 하는 방법을 권장</mark>한다. 심지어 하루에 수십 번씩해도 괜찮다. Git 브랜 치에 능숙해지면 개발 방식이 완전히 바뀌고 다른 도구를 사용할 수 없게 된 다.

### 브랜치란?

Git이 브랜치를 다루는 과정에 앞서 git이 데이터를 저장하는 방법에 대해 알아보자. Git은 데이터를 일련의 스냅샷으로 기록한다고 앞서 말한 바 있다. 즉, `커밋을 할 경우 Git은` 현 Staging Area에 있는 데이터와 스냅샷에 대한 포인터, 커밋 메시지 같은 메타데이터, 이전 커밋에 대한 포인터 등을 포함하는 `커밋 object를 저장한다`. 이전 커밋포인터가 있으므로 현재 커밋이 무엇을 기준으로 바뀌었는지를 알 수 있다. 최초 커밋을 제외한 모든 커밋은 이전 커밋포인터가 `적어도 하나`씩 있다. (브랜치를 합친 Merge 커밋은 포인터가 여러개이다.) 

파일이 3개있는 디렉토리가 하나 있고 이 파일을 Staging Area에 저장하고 커밋하는 예제를 살펴보자. 파일을 Stage 하면 Git 저장소에 파일을 저장하고 (Git은 이것을 Blob이라고 부른다) Staging Area에 해당 파일의 체크섬을 저장 한다(Chapter 1 에서 살펴본 SHA-1을 사용한다).

```
$ git add README test.rb LICENSE 
$ git commit -m 'initial commit of my project'
```

git commit으로 커밋하면 먼저 루트 디렉토리와 각 하위 디렉토리의 트리 개체를 체크섬과 함께 저장소에 저장한다. 그다음에 커밋 개체를 만들고 메타데이터와 루트 디렉토리 트리 개체를 가리키는 포인터 정보를 커밋 개체에 넣어 저장한다. 그래서 필요하면 언제든지 스냅샷을 다시 만들 수 있다. 이 작업을 마치고 나면 Git 저장소에는 다섯 개의 데이터 개체가 생긴다. 각 파일에 한 Blob 세 개, 파일과 디렉토리 구조가 들어 있는 트리 개체 하나, 메타데이터와 루트 트리를 가리키는 포인터가 담긴 커밋 개체 하나이다.

![GIT5](/assets/images/git5.PNG)

다시 파일을 수정하고 커밋하면 이전 커밋이 무엇인지도 저장한다.

![GIT6](/assets/images/git6.PNG)

<mark>Git의 브랜치는 커밋 사이를 가볍게 이동할 수 있는 포인터 같은 개념이다.</mark> 최초 커밋 시, 기본적으로 Git은 master 브랜치를 만든다. 커밋을 만들 때 마다 브랜치가 자동으로 가장 마지막 커밋을 가리키게 한다.

![GIT7](/assets/images/git7.PNG)

### 새 브랜치 생성하기

 `$git branch branch-name(testing)` 명령어를 통해 브랜치를 만들 수 있다. 아래 그림처럼 새로 만든 브랜치도 가장 최근의 커밋을 가리키고 있다.

![GIT8](/assets/images/git8.PNG)

Git은 현재 작업하는 로컬브랜치를 가리키는 `HEAD`라는 특수한 포인터를 가진다. 따라서 브랜치를 생성했다 하더라도 `checkout`을 하지 않을 경우 아래 사진과 같은 형태이다.

![GIT9](/assets/images/git9.PNG)


### [중요]브랜치 이동하기

`git checkout` 명령어를 통해 `HEAD`를 옮길 수 있다.(브랜치를 변경할 수 있다.)

```
git checkout testing
```

![GIT10](/assets/images/git10.PNG)

현재상태에서 파일에 변화를 준 뒤 커밋한다면 아래와 같이 새 커밋점이 생기고 헤드도 같이 이동한다.

![GIT11](/assets/images/git11.PNG)

당연히 `master`브랜치는 제자리에 있다. 이제 마스터 브랜치로 돌아가면 (`git checkout master`) HEAD가 다시 마스터로 돌아감을 볼 수 있다.

![GIT12](/assets/images/git12.PNG)

파일 수정 후 다시 커밋을 할 경우 아래 그림처럼 브랜치가 분기된다. 아래 그림처럼 독립적으로 작업하다가 어느 순간 두 브랜치를 Merge할 수 있다.

![GIT13](/assets/images/git13.PNG)

### [중요]브랜치와 Merge의 기초

<mark>이제 왜 브랜치를 수시로 만들고 사용해야 하는지 알아보자</mark>

실제 개발과정에서 겪을 만한 예제를 하나 살펴보자. 브랜치와 Merge는 보통 이런 식으로 진행한다. 

1. 작업 중인 웹사이트가 있다. 
2. 새로운 이슈를 처리할 새 Branch를 하나 생성한다. 
3. 새로 만든 Branch에서 작업을 진행한다. 

이때 중요한 문제가 생겨서 그것을 해결하는 Hotfix를 먼저 만들어야 한다. 그러면 아래와 같이 할 수 있다.

1. 새로운 이슈를 처리하기 이전의 운영(Production) 브랜치로 이동한다. 
2. Hotfix 브랜치를 새로 하나 생성한다. 
3. 수정한 Hotfix 테스트를 마치고 운영 브랜치로 Merge 한다. 
4. 다시 작업하던 브랜치로 옮겨가서 하던 일 진행한다.

> 상황1. 이슈 발생

 먼저 작업하는 프로젝트에서 이전에 커밋을 몇 번 했다고 가정하자.

 ![GIT14](/assets/images/git14.PNG)

53번 이슈를 처리하려고 한다고 가정하면 이 이슈를 처리하기 위한 브랜치를 생성한다

```
git checkout -b iss53
```

iss53 브랜치로 `checkout`했기 때문에 `HEAD`는 iss53브랜치를 가리키고 있다.

![GIT15](/assets/images/git15.PNG)

> 상황2. 이슈 발생 후 새로운 Hotfix(즉시해결이슈) 발생

먼저 버그를 해결한 `Hotfix`에 `iss53`이 섞이는 것을 방지하기 위해 iss53과 관련된 코드를 어딘가에 저장해두고 원래의 운영소스로 복구해야한다. 현재 작업중인 것을 커밋하고(checkout할 브랜치와 충돌이 날 수도 있으므로) `master 브랜치로 checkout`한다. 이런 문제는 추후 Stash나 Cleaning에서 다루도록 한다.

```
$git checkout master
```

이제 53번 이슈를 다루기 전으로 돌아갔으므로 Hotfix를 해결하도록 하자.

```
$git checkout -b hotfix
```

![GIT16](/assets/images/git16.PNG)

정상적으로 버그를 수정했다면 master 브랜치와 merge를 시도한다.

``` 
$ git checkout master 
$ git merge hotfix
 Updating f42c576..3a0874c
  Fast-forward
   index.html | 2 ++
   1 file changed, 2 insertions(+)
```

일반적인 경우 merge할 브랜치가 가리키는 커밋이 현 브랜치의 Upstream 브랜치이기 때문에 master 브랜치의 포인터는 최신 커밋으로 이동한다.(fast forward 방식, 사진 참조)

![GIT17](/assets/images/git17.PNG)

이제 `hotfix` 브랜치의 변경내역을 모두 병합하였기에 브랜치를 삭제한 뒤, 다시 issue53으로 돌아간다.

```
$git branch -d hotfix
$git checkout iss53
```

현재 브랜치 상황은 아래 사진과 같으며 `hotfix`브랜치의 작업이 `iss53`브랜치의 작업에 영향을 끼치지 않는다는 것을 알 수 있다. 만약 `iss53`을 해결해여 `master`에 병합하면 그때서야 `hotfix`의 내용이 적용될 것이다.

![GIT18](/assets/images/git18.PNG)


> 상황3. hotfix 병합 후 iss53 병합

53번 이슈를 모두 해결하여 `master`브랜치에 병합하는 과정을 살펴보자. 이전에 `hotfix`를 병합할 때와 마찬가지로 `master`로 checkout한 뒤 아래 명령어를 입력한다.

```
$ git checkout master 
Switched to branch 'master' 
$ git merge iss53 
Merge made by the 'recursive' strategy. 
README |    1 +
 1 file changed, 1 insertion(+)
```

`hotfix`병합 때와 조금 다른 메세지가 출력된다. 왜냐하면 이 경우 현재 브랜치가 가리키는 커밋이 Merge할 브랜치의 조상이 아니므로 Git은 각 브랜치가 가리키는 커밋 두 개와 공통조상 하나를 사용하여 3-way Merge를 한다.

![GIT19](/assets/images/git19.PNG)

`fast forward`와 달리 단순히 브랜치 포인터를 최신 커밋으로 옮기는 것이 아니라 `3-way Merge`의 결과를 별도의 커밋으로 만들고 해당 브랜치가 그 커밋을 가리키도록 이동시킨다. 해당 커밋은 부모가 여러개이며 `Merge commit`이라고 부른다.

![GIT20](/assets/images/git20.PNG)


### [중요]충돌의 기초

 병합하는 두 브랜치에서 같은 부분을 동시에 수정하는 경우 3-way Merge가 실패할 것이다.
 
 ```
$ git merge iss53 
Auto-merging index.html 
CONFLICT (content): Merge conflict in index.html 
Automatic merge failed; fix conflicts and then commit the result
 ```

 <mark>git은 자동으로 Merge 하지 못해서 새 커밋이 생기지 않는다</mark> 변경사항의 충돌을 개발자가 해결하지 않는 한 Merge 과정을 진행할 수 없다. Merge 충돌 이 일어났을 때 Git이 어떤 파일을 Merge 할 수 없었는지 살펴보려면 git status 명령을 이용한다.

> 이왕이면 툴을 사용하도록 한다.

### [중요]브랜치 Workflow

브랜치를 만들고 Merge 하는 것을 어디에 써먹어야 할까. 이 절에서는 Git 브랜치가 유용한 몇 가지 Workflow를 살펴본다. 여기서 설명하는 Workflow를 개발에 적용하면 도움이 될 것이다.

> Long-Running 브랜치

 배포했거나 배포할 코드만 master 브랜치에 Merge해서 안정버전의 코드만 master 브랜치에 둔다. 개발을 진행하고 안정화하는 브랜치는 develop이나 next라는 이름으로 추가로 만들어 사용한다. 이 브랜치는 언젠가 안정상태가 되겠지만, 항상 안정상태를 유지해야 하는 것이 아니다. 테스트를 거쳐서 안정적이라고 판단되면 master 브랜치에 Merge 한다. 토픽 브랜치(앞서 살펴 본 iss53 브랜치 같은 짧은 브랜치)에도 적용할 수 있는데, 해당 토픽을 처리하고 테스트해서 버그도 없고 안정적이면 그때 Merge 한다.

 ![GIT21](/assets/images/git21.PNG)
 ![GIT22](/assets/images/git22.PNG)

 위처럼 코드를 여러단계로 나누어 안정성을 높일 수 있다. `but, 규모가 크고 복잡한 프로젝트 일수록 좋다..`

> 토픽 브랜치

 <mark>토픽 브랜치는 프로젝트 크기에 상관없이 유용하다</mark>. 토픽 브랜치는 어떤 한 가지 주제나 작업을 위해 만든 짧은 호흡의 브랜치다. 다른 버전관리시스템에서는 브랜치를 만드는 코스트가 커서 잘 사용하지 않는 방식이다. 묶음별로 나눠서 일할 경우 검토하기도, 테스트하기도 편하다.

 > 상황1. 여러 토픽브랜치

 master 브랜치를 checkout 한 상태에서 어떤 작업을 한다고 해보자. 한 이슈를 처리하기 위해서 iss91 브랜치를 만들고 해당 작업을 한다. 같은 이슈를 다른 방법으로 해결해보고 싶을 때도 있다. iss91v2 브랜치를 만들고 다른 방법을 시도해 본다. 확신할 수 없는 아이디어를 적용해보기 위해 다시 master 브랜치로 되돌아가서 dumbidea 브랜치를 하나 더 만든다. 지금까지 말했던 커밋 히스토리는 아래 그림이다.

![GIT23](/assets/images/git23.PNG)

> 상황2. 토픽브랜치 선택 후 merge

이슈를 처리했던 방법 중 두 번째 방법인 iss91v2 브랜치가 괜찮아서 적용 하기로 결정했다. 그리고 아이디어를 확신할 수 없었던 dumbidea 브랜치를 같이 일하는 다른 개발자에게 보여줬더니 썩 괜찮다는 반응을 얻었다. iss91 브랜치는 (C5, C6 커밋도 함께) 버리고 다른 두 브랜치를 Merge 하면 아래 그림 과 같이 된다.

![GIT24](/assets/images/git24.PNG)


### ~~[RE...]리모트 브랜치~~

리모트 Refs는 리모트 저장소에 있는 포인터인 레퍼런스다. 리모트 저장소에 있는 브랜치, 태그, 등등을 의미한다. git ls-remote (remote) 명령으로 모든 리모트 Refs를 조회할 수 있다. git remote show (remote) 명령은 모든 리모트 브랜치와 그 정보를 보여준다. 리모트 Refs가 있지만 보통은 리모트 트래킹 브랜치를 사용한다.    
    
리모트 트래킹 브랜치는 리모트 브랜치를 추적하는 브랜치다. 이 브랜치는 로컬에 있지만 움직일 수 없다. 리모트 서버에 연결할 때마다 리모트 브랜치에 따라서 자동으로 움직일 뿐이다. 리모트 트래킹 브랜치는 일종의 북마크라고 할 수 있다. 리모트 저장소에 마지막으로 연결했던 순간에 브랜치가 무슨 커밋을 가리키고 있었는지를 나타낸다.     
    
<mark>리모트 브랜치의 이름은 (remote name)/(branch) 형식으로 되어있다.</mark> 예를 들어 리모트 저장소 origin의 master 브랜치를 보고 싶다면 origin/master 라는 이름으로 브랜치를 확인하면 된다. 다른 팀원과 함께 어떤 이슈를 구현 할 때 그 팀원이 iss53 브랜치를 서버로 Push 했고 당신도 로컬에 iss53 브랜치가 있다고 가정하자. 이때 서버의 iss53 브랜치가 가리키는 커밋은 로컬에 서 origin/iss53이 가리키는 커밋이다.         
     
다소 헷갈릴 수 있으니 예제를 좀 더 살펴보자. git.ourcompany.com이라 는 Git 서버가 있고 이 서버의 저장소를 하나 Clone 하면 Git은 자동으로 origin이라는 이름을 붙인다. origin으로부터 저장소 데이터를 모두 내려받고 master 브랜치를 가리키는 포인터를 만든다. 이 포인터는 origin/master라 고 부르고 멋대로 조종할 수 없다. 그리고 Git은 로컬의 master 브랜치가 origin/master를 가리키게 한다. 이제 이 master 브랜치에서 작업을 시작할 수 있다.     

![GIT25](/assets/images/git25.PNG)

로컬 저장소에서 어떤 작업을 하고 있는데 동시에 다른 팀원이 git.ourcompany.com 서버에 Push 하고 master 브랜치를 업데이트한다. 그러면 이제 팀원 간의 히스토리는 서로 달라진다. 서버 저장소로부터 어떤 데이터도 주고 받지 않아서 origin/master 포인터는 그로다.

![GIT26](/assets/images/git26.PNG)

리모트 서버로부터 저장소 정보를 동기화하려면 `git fetch origin` 명령 을 사용한다. 명령을 실행하면 우선 “origin” 서버의 주소 정보(이 예에서는 git.ourcompany.com)를 찾아서, 현재 로컬의 저장소가 갖고 있지 않은 새로 운 정보가 있으면 모두 내려받고, 받은 데이터를 로컬 저장소에 업데이트하고 나서, origin/master 포인터의 위치를 최신 커밋으로 이동시킨다.

 ![GIT27](/assets/images/git27.PNG)

리모트 저장소를 여러 개 운영하는 상황을 이해할 수 있도록 개발용으로 사용할 Git 저장소를 팀 내부에 하나 추가해 보자. 이 저장소의 주소가 git.team1.ourcompany.com 이며 Chapter 2에서 살펴본 git remote add 명령으로 현재 작업 중인 프로젝트에 팀의 저장소를 추가한다. 이름을 teamone으로 짓고 긴 서버 주소 대신 사용한다.

### ~~[RE...]PUSH 하기~~

로컬의 브랜치를 서버로 전송하려면 쓰기 권한이 있는 리모트 저장소에 Push 해야 한다
 
> 상황1. `serverfix`라는 브랜치를 다른사람과 공유한다.

serverfix라는 브랜치를 다른 사람과 공유할 때에도 브랜치를 처음 Push 하는 것과 같은 방법으로 Push 한다. 아래와 같이 git push (remote) (branch) 명령을 사용한다.

```
$ git push origin serverfix 
Counting objects: 24, done. 
Delta compression using up to 8 threads. 
Compressing objects: 100% (15/15), done. 
Writing objects: 100% (24/24), 1.91 KiB | 0 bytes/s, done. 
Total 24 (delta 2), reused 0 (delta 0) 
To https://github.com/schacon/simplegit
 * [new branch]      serverfix -> serverfix
```

### ~~[RE...]브랜치 추적~~


### [중요]PULL 하기

git fetch 명령을 실행하면 서버에는 존재하지만, 로컬에는 아직 없는 데이터를 받아와서 저장한다. 이 때 워킹 디렉토리의 파일 내용은 변경되지 않고 그대로 남는다. 서버로부터 데이터를 가져와서 저장해두고 사용자가 Merge 하도록 준비만 해둔다. 간단히 말하면 git pull 명령은 git fetch 명령을 실행하고나서 자동으로 git merge 명령을 수행하는 것이다. 바로 앞에서 살펴본대로 clone이나 checkout 명령을 실행하여 추적 브랜치가 설정되면 git pull 명령은 서버로부터 데이터를 가져와서 현재 로컬 브랜치와 서버의 추적 브랜치를 Merge 한다. 일반적으로 fetch와 merge 명령을 명시적으로 사용하는 것이 pull 명령 으로 한번에 두 작업을 하는 것보다 낫다.


### ~~[RE...]Rebase하기(Rebase의 기초)~~

Git에서 한 브랜치에서 다른브랜치로 합치는 방법은 `merge`와 `rebase` 2가지가 있다. 

![GIT28](/assets/images/git28.PNG)

위의 두 브랜치를 합치는 가장 쉬운 방법은 `merge`명령어이다. 마지막 커밋 두 개(C3, C4)의 공통조상(C2)를 사용하는 3-way merge로 새 커밋(C5)을 만들것이다.

![GIT29](/assets/images/git29.PNG)

rebase란 위와 비슷한 방식으로 `C3`에서 변경된 사항을 Patch로 만들고 이를 다시 `C4`에 적용시키는 것이다.

```
$ git checkout experiment 
$ git rebase master 
First, rewinding head to replay your work on top of it... 
Applying: added staged command
```

위 명령어를 입력하면 두 브랜치가 나뉘기 전인 공통커밋으로 이동하고 그 커밋부터 Checkout한 브랜치가 가리키는 커밋까지 diff를 차례로 만들어 temp에 저장한다. `Rebase할 브랜치(expreiment)`가 `합칠 브랜치(master)`가 가리키는 커밋을 가리키게 하고 아까 저장해 놓았던 변경사항을 차례대로 적용한다.

### ~~Rebase 활용~~

### ~~Rebase의 위험성~~

### ~~Rebase VS Merge~~

일반적인 해답을 굳이 드리자면 로컬 브랜치에서 작업할 때는 히스토리를 정리하기 위해서 Rebase할 수도 있지만, Push로 리모트에든 밖으로 내보낸 커밋에 해서는 절대 Rebase하지 말아야 한다

## ~~Git 서버~~


## 분산환경에서의 Workflow

 중앙집중형 버전 관리 시스템에서 각 개발자는 중앙 저장소를 중심 으로 하는 하나의 노드일 뿐이다. 하지만, Git에서는 각 개발자의 저장소가 하 나의 노드이기도 하고 중앙 저장소 같은 역할도 할 수 있다. 즉, <mark>모든 개발자는 다른 개발자의 저장소에 일한 내용을 전송하거나, 다른 개발자들이 참여할 수 있도록 자신이 운영하는 저장소 위치를 공개할 수도 있다.</mark> 이런 특징은 프로 젝트나 팀이 코드를 운영할 때 다양한 Workflow을 만들 수 있도록 해준다.


### 중앙집중식 workflow

![GIT30](/assets/images/git30.PNG)

팀이 작거나 이미 중앙집중식에 적응한 상황이라면 이 Workflow에 따라 Git을 도입하여 사용할 수 있다. 중앙 저장소를 하나 만들고 개발자 모두에게 Push 권한을 부여한다. 모두에게 Push 권한을 부여해도 Git은 한 개발자가 다른 개발자의 작업 내용을 덮어쓰도록 허용하지 않는다. 

<mark>충돌 발생 시, Fetch로 받아서 Merge한 뒤 Push한다!</mark>


### ~~Integration-Manager Workflow~~

이 방식은 GitHub나 GitLab 같은 Hub 사이트를 통해 주로 사용하는 방식이 다. 프로젝트를 Fork 하고 수정사항을 반영하여 다시 모두에게 공개하기 좋은 구조로 돼 있다. 

### ~~Dictator and Lieutenant Workflow~~

보통 수백 명의 개발자가 참여하는 아주 큰 프로젝트를 운영할 때 이 방식을 사용한다. Linux 커널 프로젝트가 표적이다. 

### ~~프로젝트에 기여하기~~

### ~~커밋 가이드라인~~

### [매우중요]비공개 소규모 팀

모든 개발자는 공유하는 저장소에 쓰기 권한이 있어야 한다. <mark>이런 환경에서는 보통 SVN 같은 시스템에서 사용하던 방식을 사용</mark>한다. 물론, Git이 가진 오프라인 커밋기능이나 브랜치 Merge 기능을 이용하지만 크게 다르지 않다. 가장 큰 차이점은 서버가 아닌 클라이언트 쪽에서 Merge한다는 것이다.

> 상황 1. 개발자 재우는 저장소를 Clone하고 파일을 `수정`하고 로컬에 커밋한다.

```
# Jaewoo's Machine 
$ git clone john@githost:simplegit.git 
Initialized empty Git repository in /home/john/simplegit/.git/ ... 
$ cd simplegit/ 
$ vim lib/simplegit.rb 
$ git commit -am 'removed invalid default value'
 [master 738ee87] removed invalid default value
1 files changed, 1 insertions(+), 1 deletions(-)
```

> 상황 2. 개발자 지훈은 저장소를 Clone하고 파일을 `추가`하고 로컬에 커밋/푸쉬한다.

```
# ji Hoons Machine 
$ git clone jessica@githost:simplegit.git
Initialized empty Git repository in /home/jessica/simplegit/.git/ ... 
$ cd simplegit/ 
$ vim TODO 
$ git commit -am 'add reset task' 
[master fbff5bc] add reset task 
1 files changed, 1 insertions(+), 0 deletions(-)

$ git push origin master 
... 
To jessica@githost:simplegit.git   
1edee6b..fbff5bc  master -> master

```

> 상황 3. 개발자 재우도 변경사항을 `푸쉬`한다.

```
# jaewoo's Machine 
$ git push origin master 
To john@githost:simplegit.git
! [rejected]        master -> master (non-fast forward) 
error: failed to push some refs to 'john@githost:simplegit.git'
```

`SVN과 다르게 지훈의 Push는 성공`했지만 `재우의 Push는 서버에서 거절`된다. 같은 파일을 수정하지 않았는데도 말이다. SVN은 서로 다른파일을 수정하는 Merge 작업은 자동으로 서버가 처리하지만 Git은 로컬에서 먼저 Merge 해야한다. 즉, <mark>재우는 Push하기 전에 지훈이 수정한 커밋을 Fetch하고 Merge해야한다</mark>

```
$git fetch origin
```

fetch하고난 뒤, 재우의 `로컬저장소`는 아래와 같다.

![GIT31](/assets/images/git31.PNG)

지훈이 원격저장소(`origin`)으로 push한 코드를 로컬로 가져왔다. 이제 `재우의 변경사항`을 push하기 전에 Fetch한 브랜치를 `Merge`해야한다.

```
$git merge origin/master
Merge made by recursive.
TODO | 1+
1 files changed, i insetions(+), 0 deleteions(-)
```

아래는 `merge 후` 재우의 로컬저장소 상태이다. 동시에 지훈은 `토픽브랜치`를 하나 만든다. `issue54`브랜치를 만들고 세번에 걸쳐서 커밋하며 push한 재우의 커밋을 fetch하지 않은 상황이기 때문에 아래와 같은 상황이 된다.

![GIT32](/assets/images/git32.PNG)

지훈은 재우의 작업을 적용하기 위해 `Fetch`한다.

```
$ git fetch origin 
... 
From jessica@githost:simplegit
   fbff5bc..72bbc59  master     -> origin/maste
```

위 명령으로 재우가 Push 한 커밋을 모두 내려받는다. 그러면 지훈의 저장소는 아래와 같은 상태가 된다.

![GIT33](/assets/images/git33.PNG)

이제 `origin/master`(재우가 Push한 커밋)와 merge한다. 우선 Merge할 내용을 확인하고 합치기 전에 우선 `master`브랜치로 checkout 한다.

```
$git checkout master
Switched to branch 'master' 
Your branch is behind 'origin/master' 
```

`origin/master`, `issue54` 모두 Upstream 브랜치이므로 둘 중에 어느것을 먼저 Merge하던 상관이 없다. 물론 히스토리는 달라지지만 최종결과는 같다.


> 1. `issue`브랜치 병합

```
$ git merge issue54 
Updating fbff5bc..4af4298 
Fast forward
 README           |    1 +
 lib/simplegit.rb |    6 +++++ 
 2 files changed, 6 insertions(+), 1 deletions(-)
```
Fast-forward Merge이므로 문제 없이 실행된다. 다음으로 재우의 커밋 `Origin/master`를 병합한다.

> 2. `origin/master`병합

```
$ git merge origin/master 
Auto-merging lib/simplegit.rb 
Merge made by recursive.
 lib/simplegit.rb |    2 + 
 1 files changed, 1 insertions(+), 1 deletions(-)
```

> 3. 마지막 push

```
$ git push origin master 
... To jessica@githost:simplegit.git
   72bbc59..8059c15  master -> master
```

최종 결과는 아래와 같다.

![GIT34](/assets/images/git34.PNG)

토픽 브랜치에서 수정하고 로컬의 master 브랜치에 Merge 한다. 작업한 내용을 프로젝트의 공유 저장소에 Push 하고자 할 때에는 우선 origin/master 브랜치를 Fetch 하고 Merge 한다. 그리 고 나서 Merge 한 결과를 다시 서버로 Push 한다. 이런 Workflow가 일반적이며 아래와 같이 나타낼 수 있다.


![GIT35](/assets/images/git35.PNG)


## GITHUB

### GitHub Flow

GitHub은 Pull Request가 중심인 협업 Workflow를 위주로 설계됐다. 이 Workflow는 Fork 해서 프로젝트에 기여하는 것인데 단일 저장소를 사용하는 긴한 팀에서도 유용하고 전 세계에서 흩어져서 일하는 회사나 한 번도 본 적 없는 사람들 사이에서도 유용하다. Chapter 3 에서 설명했던 “토픽 브랜 치” 중심으로 일하는 방식이다. 보통은 아래와 같이 일한다. 

 1. master에서 토픽 브랜치를 만든다. 
 2. 뭔가 수정해서 커밋한다. 
 3. 자신의 GitHub 프로젝트에 브랜치를 Push 한다. 
 4. GitHub에 Pull Request를 연다. 
 5. 토론하면서 그에 따라 계속 커밋한다. 
 6. 프로젝트 소유자는 Pull Request를 Merge 하고 닫는다. 

### [꿀팁]PULL REQUEST 만들기

> 상황1. Tony는 자신의 Arduino 장치에서 실행해볼 만한 코드를 찾고 있었고 GitHub에 있는 https://github.com/schacon/blink에서 매우 흡족한 프로그램을 찾았다.

다 좋은데 너무 빠르게 깜빡이는 게 마음에 안 들었다. 매초 깜빡이는 것보 다 3초에 한 번 깜빡이는 게 더 좋을 것 같았다. 그래서 프로그램을 수정하고 원 프로젝트에 다시 보내기로 했다. 앞서 설명했던 것처럼 Fork 버튼을 클릭해서 프로젝트를 복사한다. 사용자 이름이 “tonychacon”이라면 https://github.com/tonychacon/blink에 프 로젝트가 복사된다. 이 프로젝트는 본인 프로젝트이고 수정할 수 있다. 이 프 로젝트를 로컬에 Clone 해서 토픽 브랜치를 만들고 코드를 수정하고 나서 GitHub에 다시 Push 한다.


```

$ git clone https://github.com/tonychacon/blink Cloning into 'blink'...
$ cd blink $ git checkout -b slow-blink Switched to a new branch 'slow-blink'
$ sed -i '' 's/1000/3000/' blink.ino 
$ git diff --word-diff 
diff --git a/blink.ino b/blink.ino 
index 15b9911..a6cc5a5 100644 
--- a/blink.ino 
+++ b/blink.ino 
@@ -18,7 +18,7 @@ void setup() { 
    // the loop routine runs over and over again forever: 
    void loop() {
          digitalWrite(led, HIGH);   // turn the LED on (HIGH is the voltage level)  [-delay(1000);-]{+delay(3000);+}               // wait for a second  
          digitalWrite(led, LOW);    // turn the LED off by making the voltage LOW  
          [-delay(1000);-]{+delay(3000);+
          }               // wait for a second 
    }

$ git commit -a -m 'three seconds is better' 
[master 5ca509d] three seconds is better 
1 file changed, 2 insertions(+), 2 deletions(-)

$ git push origin slow-blink 
Username for 'https://github.com': tonychacon 
Password for 'https://tonychacon@github.com': 
Counting objects: 5, done. 
Delta compression using up to 8 threads. 
Compressing objects: 100% (3/3), done. 
Writing objects: 100% (3/3), 340 bytes | 0 bytes/s, done. 
Total 3 (delta 1), reused 0 (delta 0) To https://github.com/tonychacon/blink
 * [new branch]      slow-blink -> slow-blink

```

1. Fork 한 개인 저장소를 로컬에 Clone 한다.
2. 무슨 일인지 설명이 되는 이름의 토픽 브랜치를 만든다.
3. 코드를 수정한다.
4. 잘 고쳤는지 확인한다.
5. 토픽 브랜치에 커밋한다.
6. GitHub의 개인 저장소에 토픽 브랜치를 Push 한다



## GIT 도구

### ~~[RE][중요]Stashing과 Cleaning~~

> 상황1. 작업이 미완성상태일 때, 다른요청이 들어와서 잠시 브랜치를 변경해야 한다.

현재 작업이 완료되지 않았기 때문에 커밋하기 껄끄럽다... 이 상황에서 `git stash`를 사용한다. stash는 워킹디렉토리에서 수정한 파일들만 저장한다. 즉 Stash는 Modified이면서 Tracked인 파일과 Staging파일을 보관해두는 장소이다.

예제 프로젝트를 하나 살펴보자. 파일을 두 개 수정하고 그 중 하나는 Staging Area에 추가한다. 그리고 git status 명령을 실행하면 아래와 같은 결과를 볼 수 있다.

```
$ git status 
Changes to be committed: 
 (use "git reset HEAD <file>..." to unstage)

    modified:   index.html

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)  (use "git checkout -- <file>..." to discard changes in working directory)

    modified:   lib/simplegit.rb
```
 
이제 브랜치를 변경하고 상태를 살펴보자.

```
$ git stash
 Saved working directory and index state \
   "WIP on master: 049d078 added the index file"    
HEAD is now at 049d078 added the index file 
(To restore them type "git stash apply


$ git status 
# On branch master 
nothing to commit, working directory clean
```

이제 아무브랜치나 골라서 쉽게 바꿀 수 있다. 또, git stash list를 이용하여 저장한 stash를 확인한다.

```
$ git stash list 
stash@{0}: WIP on master: 049d078 added the index file 
4stash@{1}: WIP on master: c264051 Revert "added file_size" 
stash@{2}: WIP on master: 21d80a5 added number to lo
```

Stash 두 개는 원래 있었다. 그래서 현재 총 세 개의 Stash를 사용할 수 있다. 이제 git stash apply를 사용하여 Stash를 다시 적용할 수 있다. git stash 명령을 실행하면 Stash를 다시 적용하는 방법도 알려줘서 편리하다. git stash apply stash@{2}처럼 Stash 이름을 입력하면 골라서 적용할 수 있다. 

```
$ git stash apply 
# On branch master 
# Changed but not updated: 
#   (use "git add <file>..." to update what will be committed) # 
#      modified:   index.html 
#      modified:   lib/simplegit.rb 
#
```
이름이 없으면 Git은 가장 최근의 Stash를 적용한다. Git은 Stash에 저장할 때 수정했던 파일들을 복원한다.


### ~~[RE]..Reset 명확히 알고 가기~~

<mark>이 두 명령은 Git을 처음 사용하는 사람을 가장 헷갈리게 하는 부분이다.</mark>






## GIT 맞춤



## GIT MIGRATION

## GIT 내부

## TortoiseGIT
