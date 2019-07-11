---
title: "[예상문제]최종예상문제"
permalink: docs/final-ready
last_modified_at: 2019-07-10T18:56:49-04:00
excerpt: "최종예상문제입니다."
toc: true
classes: wide
author_profile: false
sidebar:
  title: "Order List"
  nav: sidebar-sample
tags:  
  - computer science

---


### ~~2014년 1번~~

* bitonic sort
  * quick sort정도면 단일스레드를 빠르게 처리하는데는 문제가 없다.
  * 이제는 병렬적으로 빠르게 처리하는 것이 문제가되어 나타난 알고리즘
  * 공간복잡도가 높지만 병렬처리할 때 O(logN * logN)으로 빠르게 처리가능하다.


### 2014년 2번

* topological sort(위상정렬)
  * 어떤 일을 하는 순서를 찾는 알고리즘
  * 방향 그래프에 존재하는 각 정점들의 순서를 위배하지 않으며 모든 정점을 나열하는 것..
  

### 2014년 3번

* Go-back-N ARQ와 Selective Repeat ARQ는 `Transport layer의 프로토콜`이며 두 가지를 혼합/개선한 것이 `TCP`이다.

* 파이프라인: ACK를 받기 전 보낼 수 있는 프레임의 갯수
* Sliding window: 파이프라인의 크기

* ARQ(Automatic Repeat reQuest)
  * 에러가 발생한 경우 재전송을 요구하는 방식

* Stop And Wait ARQ
  * **대원칙**: 프레임을 제대로 받은 경우에만 ACK를 보내 응답한다.
  * 송신측은 사본을 가지고 있다가 타이머가 만료되면 다시 프레임을 보낸다.(ACK가 오지않으면 손실, 중복 등이 발생된 것으로 판단)

* Go-back-N ARQ
  * 패킷전송 시 수신측에서 데이터를 잘못받거나 못받을 때, `못 받은 패킷번호부터 재전송`하는 기법

  * **따라서, Stop-and-Wait ARQ는 송신측 sliding window의 크기가 1인 Go-back-N ARQ라고 볼 수 있다.**

* Selective Reapeat
  * 패킷전송 시, 수신측에서 데이터를 잘못받거나 못받을 때, `못 받은 패킷만 재전송`하는 기법

### (중요)2014년 4번

* tracert(trace route)
  * 지정된 호스트에 도달할 때 까지 통과하는 경로의 정보와 지연시간을 추적하는 명령어. 쉽게 경로 추적 툴이라고 볼 수 있다. 어떤 곳에서 병목이 발생했는지 알아낼 수 있어 매우 유용하다.
  * `tracert 목적지 IP` 형태로 사용
  * tracert -d 목적지 = 이름해석 X, IP주소만 출력(빠르다)
  * tracert -h 숫자 목적지 = 숫자만큼의 경로만 출력

* 추가
  * ICMP(Internet Control Message Protocol)
    * 통신 중 발생하는 오류처리/메세지 등을 취급하는 프로토콜
  * `ping`
    * 도메인주소로 ICMP 메세지를 전송한다.
    * ping -r 숫자 = 숫자만큼 라우팅 경로 출력
    * ping -s 숫자 = 숫자만큼 타임스탬프 출력
    * ping -l 숫자 = 숫자 크기만큼 ICMP 사이즈 조절
    * PING -n 숫자 = 숫자만큼 ICMP 메세지 전송
    * ex) ping 123.456.7.8 -l 500 -n 3 -r 3
      * 123.456.7.8로 500사이즈의 패킷을 3회 전송하고 전송경로 3개를 출력한다.

  * `netstat`
    * 라우팅 테이블을 확인하거나 열려져있는 포트/서비스의 상태, 네트워크 연결상태를 알아보기 위해 사용한다.
    * netstat -a = 모든 연결 및 포트를 표시
    * netstat -t = tcp로 연결된 모든 포트 표시
    * netstat -u = udp로 연결된 모든 포트 표시
    * netstat -r = 라우팅 테이블 표시
    * netstat -p `프로토콜` = 해당 토콜과 연결된 정보 표시
  * `nslookup`
    * 도메인의 IP주소를 확인할 수 있는 명령어
    * EX) nslookup www.naver.com


### 2014년 5번

* Naive Bayes Classifier(스팸 필터 알고리즘)
  * Baye's theorem에 근거한 분류법과 naive Bayes 알고리즘을 이용하여 스팸을 구분하는 것.
  * naive란 예전 스팸문서에 a, b, c가 있었다고 가정할 때, b가 나타날 확률은 a,c와 무관하다고 가정하는 것이다.
  
* 예제
  * 총 메일: 74개
  * 스팸메일: 30개
  * 조건1. 74개 중 51개의 메일은 `test`라는 단어를 포함하고 있다.
  * 조건2. `test` 라는 단어가 들어간 20개의 이메일을 스팸으로 분류했다.

  * 따라서, 최근 수신한 메일에 test가 들어간 경우 스팸일 확률은 다음과 같다.
  * P(A) = 스팸일 확률
  * P(B) = `test`가 들어간 메일일 확률
  * P(A|B) = `test`가 들어간 메일인 경우 스팸일 확률
  * 즉, P(A|B) = 스팸&TEST / TEST = 20 / 51 = 0.39..? 어쩌라구요

* 예제2
  1. 메일함에 들어오는 스팸메일의 비율(0.8)
  2. 메일함에 들어오는 정상메일의 비율(0.2)
  3. 정상메일에 `money`가 들어있을 확률(0.1)
  4. 스팸메일에 `money`가 들어있을 확률(0.6)
  * 위 조건을 기준으로 베이즈의 공식을 풀이하면 아래와 같다
  [baye's](http://image.dongascience.com/Photo/2016/10/14775424793897.JPG)

  따라서, 1X4 > 2X3 인 경우, `money`가 들어있는 메일이 스펨메일이 확률이 높다.


### 2014년 6번 스케쥴링

* inturrupt
  * 예상치 못한 일이 발생하여 이를 최우선적으로 해결하는 기능
  * 인터럽트 발생 시, context switching이 발생한다.
  * I/O, time slice expired 등

* Throughtput: 단위시간 당 처리하는 작업의 수
* Waiting time: 프로세스가 연산되기 위해 Ready queue에서 대기하는 시간

* context switching
  * 인터럽트 발생 시, PCB에 있는 데이터(프로세스 정보)를 교환하는 절차

* RR(Rount Robin) 방식
  * FCFS + 선점 + time slice 
  * Time slice만큼 각 프로세스는 CPU를 할당받는다.
  * 만약, Time Slice가 끝나기 전에 프로세스가 종료되면 Context Switching은 발생하지 않는다.
  * 평균 context switching time은 10마이크로초 정도 이므로 적절한 time Slice분배가 필요하다.

* Priority Scheduling
  * 우선순위를 매겨 연산을 실행한다.
  * 단, starvation이 발생할 수 있으므로 `aging`기법을 통해 시간이 지나면 우선순위를 높일 수 있따.
  
* 예제) RR방식일 때, 평균 처리시간을 구하시오

![RR](https://t1.daumcdn.net/cfile/tistory/99982E335A28F8BC0F)

* MultiLevel Queue Scheduling
  * 프로세스를 그룹화하는 방식, 은행 대출창구 예금업무 분할한 것과 비슷하게 생각하면 된다


### 2014년 7번 데드락

* 데드락 발생조건
    1. 상호 배제(mutual exclusion) = **자원 동시 접근불가**
      * 한 번에 한 프로세스만 공유 자원을 사용할 수 있다.
      * 좀 더 정확하게는, 공유 자원에 대한 접근 권한이 제한된다. 자원의 양이 제한되어 있더라도 교착상태는 발생할 수 있다.
  2. 들고 기다리기(hold and wait) = **점유대기**
      * 공유 자원에 대한 접근 권한을 갖고 있는 프로세스가, 그 접근 권한을 양보하지 않은 상태에서 다른 자원에 대한 접근 권한을 요구할 수 있다.
  3. 선취 불가능(Non Preemptive) = **비선점**
      * 한 프로세스가 다른 프로세스의 자원 접근 권한을 강제로 취소할 수 없다.
  4. 대기 상태의 사이클(circular wait)

* DeadLock Prevention

* DeadLock Avoidance

* Deadlock Detection, Recovery


### 2014년 8번 단편화

* page (내부단편화 발생)
  * 가상메모리를 `같은 크기의 블록으로 나눈 것`

* segment (외부단편화 발생)
  * 가상메모리를 `서로 크기가 다른 논리적 단위로 나눈 것`

* Internal Fragmentation
  * 프로세스가 필요한 양보다 더 큰 메모리가 할당되어 내부에 메모리가 남는 경우

* External Fragmentation
  * 메모리 할당/해제 반복 시 중간에 사용하지않는 남는 메모리가 생기는데 이게 쌓이는 경우
  * 중간중간 잘린 1MB짜리 메모리가 10개면 10MB이지만 실제 10MB짜리 프로세스를 할당할 수 없다.


### (질문)2014년 9번 

* 부울대수
  * x(y+z) = xy + xz
  * x+yz = (x+y)(x+z)
  * (x+y)' = x'y'
  * (xy)' = x' + y'

  * 예시)
    * A + AB
      * = A(1+B) = A
    * AB + AB'
      * = A(B+B') = A
    * (질문) A'BC + AC 
      * = (A'B + A)C = (A+A')(A+B)C = (A+B)C            
    * A'B+ ABC'+ ABC 
      * = A'B + AB(C'C) = A'B + AB = (A'+A)B = B
    * (질문) AB+A(CD+CD') = AB + A(C(D+D')) = AB + AC = A(B+C)
      * 정답 = A + AB = A(1+B) = A
    * (질문) (BC'+A'D)(AB'+CD') 
      * = BC'AB' + BC'CD' + A'DAB' + A'DCD' = AC' + BD' + DB' + A'C = AC' + A'C + BD' + DB' = 1 (정답은 0)
    
  * De Morgan 정리
    * 예시)
      * (A+B')'(A'+B')' = (A'B)(AB) = AA'BB 따라서 무조건 결과는 0
      * AA' = 0 인이유는 A AND A' = 0이기 때문이다.
      * A+A'B+A'B' = A+A'(B+B')= A+A'  = 1

    * F = x'y + xy'z 에 대하여
      * F' = (x'y + xy'z)' = (x'y)'(xyz')' = (x+y')((xy)' + z) = (x+y')(x'+y'+z) = xx'+ xy' + xz + y'x' + y'y' + y'z = 0 + xy' + xz + y'x' + y' = xz + (x+x'+1)y' = xz + y'
      * FF' = 0임을 증명하여라
        * (x'y+xyz')(y'+xz) = 0 풀기
      * F+F' = 1임을 증명하라
        * 풀면됨


### ~~2015년 1번~~

* demand paging
  * 연산 시, 가상메모리에 접근하여 실제 데이터를 가져올 수 없어 **페이징이 요구될 때만 가상메모리와 물리메모리의 주소를 변환하는 기술**  
  * 9/10 Rule에 따라 가상메모리를 활용하게 되며 이러한 논리/물리 메모리주소를 MMU를 통해 변환한다.
  * LRU = Least Recently Used, 가장 오래전에 쓰였던 페이지를 교체하면 된다.

### ~~2015년 2번~~

* sql 짜는 문제(금요일 빡공)

### ~~2015년 3번~~

* 정렬 별 시간복잡도

![time complexity](http://cfs6.tistory.com/upload_control/download.blog?fhandle=YmxvZzEzODYwNkBmczYudGlzdG9yeS5jb206L2F0dGFjaC8wLzA1MDAwMDAwMDA3Ny5qcGc%3D)

### ~~2015년 4번~~

* 무방향 그래프
  * 두 노드를 연결하는 간선에 방향이 없는 그래프

* 완전 그래프
  * n개의 정점을 가진 그래프 중 n(n-1)/2개의 간선을 갖는 그래프
  ![complete graph](https://upload.wikimedia.org/wikipedia/commons/thumb/b/b7/3-coloringEx.svg/250px-3-coloringEx.svg.png)

* 스패닝 트리 프로토콜
  * 네트워크에서 루핑을 막기위한 용도로 사용되는 트리 프로토콜
  
* MST(Minimum Spanning Tree)
  * 연결된 그래프에서 사이클이 생기지 않는 최단경로만을 찾은 트리
  * Prim's algorithm = O(N^2)
    * 각 노드를 기준으로 다른 노드로가는 최단경로테이블을 그려 갱신하는 방식
  * 크루스칼 알고리즘 = O(eloge + 정렬)
    * 각 엣지를 기준으로 greedy 하게 최소비용을 찾는다.

### 2015년 5번

* 인접행렬
  * 공간복잡도 = O(V*V)  
  * 그래프 간의 연결관계를 이차원 배열로 나타내는 방식, 무방향그래프에서는 대각선 기중 대칭이다.
* 인접리스트
  * 공간복잡도 = O(V+E)
  * 아래와 같이 노드별로 연결된 정보만을 벡터로 기록하는 방식   
  ![list](https://t1.daumcdn.net/cfile/tistory/265E074D584C26DD2B)   


### 2015년 10번

* 폭포수 모델 요구분석 후 4단계를 적으시오
  * 프로세스가 따로 없는 절차적 프로그래밍 기법이다.
  * 계획수립 -> 요구분석 -> **설계 -> 개발/구현 -> 테스트 -> 유지보수** 순으로 진행된다.

* (추가) 프로토타이핑모델
  * 사용자중심의 모델
  * 계획수립 -> 요구분석 -> 프로토타입 개발 -> 평가 -> 구현 -> 테스트 순으로 진행된다

* (추가) Spiral 모델
  * 위험 분석단계를 점진적으로 반복하여 개발한다.
  * 계획수립 -> 위험분석 -> 구현 및 테스트 -> 유지보수

### 2015년 11번

* 16진수 수를 3bit shifting 한 결과를 적으시오
  * 예시) 
    ![shift](https://dojang.io/pluginfile.php/237/mod_page/content/23/unit23-3.png)

```c
    #include <stdio.h> 
    int main()
    {
        unsigned char num1 = 3;     //  3: 0000 0011
        unsigned char num2 = 24;    // 24: 0001 1000
    
        printf("%u\n", num1 << 3);  // 24: 0001 1000: num1의 비트 값을 왼쪽으로 3번 이동
        printf("%u\n", num2 >> 2);  //  6: 0000 0110: num2의 비트 값을 오른쪽으로 2번 이동
        printf("%u\n", num1 << 7);  // 384: 1 1000 0000: num1의 비트 값을 왼쪽으로 7번 이동
        printf("%u\n", num2 >> 4);  //  1: 0000 0001: num2의 비트 값을 오른쪽으로 5번 이동      
        return 0;
    }
```

    
    
### 2016년 1번

* 트랜잭션과 ACID에 대해 설명하시오.
  * 프로세스가 따로
