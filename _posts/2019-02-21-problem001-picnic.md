---
title: "[풀이,회고]종만북001 picnic"
permalink: docs/problem001-picnic
last_modified_at: 2019-02-21T17:58:49-04:00
excerpt: "종만북 1번문제 Picnic 회고"
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

**Note:** 전체목차를 다룰 수 없어 필요하다고 생각하는 부분만 발췌하여 요약합니다.
{: .notice--warning}




## 최초 생각

```javascript
#include <iostream>
#include <vector>

//`boolean`형태의 1차원 배열 human[N]을 생성한다.
//이는 1~N까지의 사람을 나타내며 True, False 값은 짝을 맺었는지 아닌지의 여부이다.

boolean human[N];
int findFirstStudent(human[N]){
 int firstStudent = -1;
 for(int i=0; i<N; i++){
   if(!human[N])
   {
     firstStudent = i;
     break;
   }   
 }
 return firstStudent;
}

int matching(boolean human[N]){

  기능1. 남은 친구 중 가장 번호가 빠른 친구를 찾는다.
  int firstStudent;
  firstStudent = findFirstStudent(human[N]);

  ....짝을 찾는다..
}

int main() {

  matching(human[N]);

  return ;
}

```



## 검색 후 생각

```javascript
#include <iostream>
#include <vector>

//`boolean`형태의 1차원 배열 human[N]을 생성한다.
//이는 1~N까지의 사람을 나타내며 True, False 값은 짝을 맺었는지 아닌지의 여부이다.

int N; (학생 수)
boolean human[N];
bool areFriends[N][N];

int findFirstStudent(human[N]){
 int firstStudent = -1;
 for(int i=0; i<N; i++){
   if(!human[N])
   {
     firstStudent = i;
     break;
   }   
 }
 return firstStudent;
}

int matching(boolean human[N]){

  //기능1. 남은 친구 중 가장 번호가 빠른 친구를 찾는다.
  int firstStudent;
  firstStudent = findFirstStudent(human[N]);

  //기저사례: 모든 학생이 짝을 찾았으면 한 가지 방법을 찾았으니 종료한다.
  if(first Student == -1)   return 1;

  int result = 0;
  //이 학생과 짝지을 학생 결정
  for(int i= firstStudent+1; i<N; i++;){
    if(!human[i] && areFriends[firstStudent][i])
    {
      human[firstStudent] = human[i] = true; //짝이 정해져 있는 상태
      result += matching(human); //재귀
      human[firstStudent] = human[i] = false; // 다른 경우의 수를 찾기 위해 짝 해제
    }
  }
  return result;
}

int main() {

 //데이터 쭉받아서

 memset(areFriends, false, sizeof(areFriends));
 memset(human, false, sizeof(human));

 // 받은 친구들 값만큼 true 넣어주고


cout<<  matching(human[N]);

  return ;
}

```
