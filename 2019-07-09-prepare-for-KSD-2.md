---
title: "[TO-DO-LIST]PREPARE-FOR-KSD-2"
permalink: docs/to-do-list-KSD-2
last_modified_at: 2019-07-09T17:56:49-04:00
excerpt: "나머지과목인 자료구조와 소프트웨어공학에 대해 다룹니다."
toc: true
classes: wide
author_profile: false
sidebar:
  title: "Order List"
  nav: sidebar-sample
tags:
  - data structure
  - software engineering

---

완료 후, ~~취소선~~으로 표시하며 하나씩 제거합니다.



## 자료구조

![자료구조](https://wayhome25.github.io/assets/post-img/cs/data-structure.png)

### 1장 자료구조와 알고리즘

* 최선, 평균, 최악의 경우
  * 최선의 경우: 의미없는 경우가 많다
  * 평균적인 경우: 계산하기 상당히 어려움
  * 최악의 경우: 널리 사용되며 경우에 따라 중요한 의미를 가짐

    ![problem](/assets/images/prepare-for-KSD-1.PNG)


### 2장 재귀(recursion)

### 3장 배열, 구조체, 포인터

* 구조체
  * 타입이 다른 데이터를 하나로 묶는 방법
  * 배열은 같은 타입의 데이터를 하나로 묶는다. 

* 포인터
  * 다른 변수의 주소를 가지고 있는 변수
  * 포인터가 가리키는 내용의 변경은 `*` 연산자를 이용한다.
  * 변수의 주소를 추출할 때는 `&` 연산자를 이용한다.

  ```c

    p;    	// 포인터
    *p;    	// 포인터가 가리키는 값
    *p++;  	// 포인터가 가리키는 값을 가져온 다음, 포인터를 한칸 증가한다.
    *p--;  	// 포인터가 가리키는 값을 가져온 다음, 포인터를 한칸 감소한다.

    void swap(int *px, int *py)
    { 
      int tmp;
      tmp = *px;
      *px = *py;
      *py = tmp;
    }
    int main()
    {
      int a=1,b=2;
      printf("swap을 호출하기 전: a=%d, b=%d\n", a,b);
      swap(&a, &b);
      printf("swap을 호출한 다음: a=%d, b=%d\n", a,b);
    }
  ```

### 3장 배열, 구조체, 포인터

### 4장 리스트

### 5장 스택


* 수식의 계산
  * prefix
    * +2*3 4, +5*ab, +7+1 2
  * infix 
    * 2+3*4, a+b*5, (1+2)+7
  * postfix
    * 234*+, ab*5+,  12+7+

> 컴퓨터에서는 스택을 사용하며 중위표기 -> 후위표기 -> 계산 순으로 작업이 진행된다.

> postfix와 infix의 피연산자 순서는 같으므로 스택에 연산자만 저장했다가 꺼내면 된다.


### 6장 큐


### 7장 트리


* 이진트리(binary tree)
  * 모든 노드가 2개의 서브 트리를 가지고 있는 트리
  * 이진 트리의 종류   

  ![problem](/assets/images/prepare-for-KSD-2.PNG)   
    * full binary tree
      * 말 그대로 트리의 각 레벨에 노드가 꽉 차있는 이진트리
    * complete binary tree
      * 마지막 Level에만 노드가 덜 채워져 있는 트리 
      * 단, 마지막 레벨의 트리는 왼쪽부터 순서대로 노드가 채워져야 한다.   
      ![problem](/assets/images/prepare-for-KSD-3.PNG)


* B-Tree
  * 이진트리를 확장하여 더 많은 수의 자식을 가질 수 있게 일반화한 트리
  * 하나의 노드에 여러자료가 배치되는 트리구조이다.
    * 규칙
      * Root 노드는 적어도 2개 이상의 자식을 가져야 한다.
      * 노드의 자료수가 N이라면 자식의 수는 N+1이어야 한다,
    * 특징
      * 순회작업이 상당히 어렵다.
      * 특정 key값이 하나의 노드에서만 존재할 수 있다.

* B+Tree
  * B트리의 변형구조로 Leaf노드가 순차적으로 Linked list를 구성하고 있어 순차적 처리가 가능하다.
    * 특징
      * 삽입작업이 b트리와 거의 동일하다

* B트리 VS B+트리
  * 공통점
    * 모든 Leaf의 depth가 같다
    * search가 비슷하다
    * 삽입 시 overflow가 발생하면 split한다.
  * 차이점
    * B-Tree의 각 node에는 key뿐만 아니라 data도 들어갈 수 있다.
    * B+Tree의 각 node에는 key만이 들어갈 수 있다. 즉, data는 leaf에만 존재한다.
    * B+트리의 leaft들은 linked list로 연결되어 있으므로 range query가 가능하다.

  따라서, 장점이 단점을 충분히 커버하므로 B+Tree는 file system과 DBMS에 널리 사용된다.



* 스패닝 트리(Spanning Tree) 프로토콜
  * 스위치나 브릿지에서 발생하는 `루핑`을 막아주기 위한 프로토콜
