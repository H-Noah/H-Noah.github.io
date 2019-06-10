---
title: "[풀이]swacademy 풀이(III/1208 등)"
permalink: docs/swacademy(III)
last_modified_at: 2019-04-10T17:58:49-04:00
excerpt: "SW ACADEMY 1208 등 다수의 잡 문제 풀이"
toc: true
classes: wide
author_profile: false
sidebar:
  title: "Order List"
  nav: sidebar-sample
tags:
  - algorithm
  - coding

---


## 문제풀이

### Flatten(1208)

- 2차원 배열로 생각하자.
- 박스가 다른 높이로 세워져있다.
- 높게 쌓인 것을 낮은 곳으로 옮긴다.
- 최대점과 최저점의 차이가 최대1인 경우 평탄화 작업이 완료되었다고 한다.
- 작업횟수에 제한이 있을 경우, 제한된 횟수만큼만 진행해서 최고점과 최저점의 차이를 출력하라.


- 덤프: 가장 높은 곳에 있는 상자를 가장 낮은 곳으로 옮기는 작업
- 가로 길이는 항상 100
- 상자높이는 1~100
- 덤프횟수는 1~1000
- 평탄화가 완료되면 최고점 최저점 차이 반환


