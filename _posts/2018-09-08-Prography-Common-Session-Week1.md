---
title: "[강의요약]프로그라피 공통세션 - GIT"
permalink: /docs/Prography-Common-Session/
last_modified_at: 2018-09-08T15:58:49-04:00
toc: true
classes: wide
author_profile: false
sidebar:
  title: "Order List"
  nav: sidebar-sample
tags:
  - git
---


[강의요약]프로그라피 공통세션 - GIT, 별 내용 없음

## git

### GIT Merge  
:     같은 파일의 같은 라인을 수정할 경우 Conflict가 발생한다.
master branch와 dev branch를 생성하여 각 branch에서 merge를 진행한다.

### GIT branch
:     (실제 리모트저장소에 올리지 않음) 임의의 폴더에서 `git init`명령어를 사용한 뒤 `git branch XXX`를 통해 임의의 브랜치를 생성했다.
그리고 브랜치 명과 같은 TXT 파일을 생성(ex. master.txt)했다. 그 후, 생성한 브랜치로 `git checkout XXX` 명령어를 통해 이동하여 마찬가지로 다른 파일을
생성한다. 이렇게 시작된 지점은 같지만 가지가 퍼지는 것을 확인하고 `git merge XXX` 명령어를 통해 원하는 브랜치를 합칠 수 있다.
