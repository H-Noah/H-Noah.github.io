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

<<<<<<< HEAD
* demand paging, [참조](http://truemind5.blogspot.com/2017/05/15-1.html)
  * 여러 프로세스가 메모리를 효율적으로 공유할 수 있도록 하는 기술
=======
* demand paging
  * 연산 시, 가상메모리에 접근하여 실제 데이터를 가져올 수 없어 **페이징이 요구될 때만 가상메모리와 물리메모리의 주소를 변환하는 기술**  
>>>>>>> f70938e5734ff9b10e630b2757f0e827a7321829
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
  
  * 트랜잭션(Transaction) 이란
    * **데이터베이스의 상태를 변환시키는 논리적인 작업 단위(연산의 집합)**
        * 예를 들어, 계좌이체가 트랜잭션이라고 하자.
          1. A계좌의 잔액을 확인한다.
          2. A계좌의 금액에서 이체할 금액을 빼고 다시 저장한다.
          3. B계좌의 잔액을 확인한다.
          4. B계좌의 금액에서 이체할 금액을 더하고 다시 저장한다.
        * 위 네개의 연산이 합쳐져 하나의 트랜잭션을 이룬다.
    * 하나의 트랜잭션은 Commit 되거나 Rollback 된다.
        * Commit
            * 한개의 트랜잭션이 성공적으로 완료된 것을 트랜잭션 관리자에게 알려주는 연산이다.
        * Rollback 연산
            * 하나의 트랜잭션 처리가 비정상적으로 종료되었을 때, 트랜잭션이 행한 모든 연산을 취소(Undo)하는 연산이다.                
* 트랜잭션의 성질(ACID)
    * 원자성(Atomicity), All or nothing
        * 트랜잭션의 모든 연산이 완료되거나 아니면 전혀 수행되지 않아야한다.
    * 일관성(Consistency)
        * 트랜잭션 완료 후에도 일관된 상태
    * 독립성(Isolation)
        * 트랜잭션 실행 도중에 다른 트랜잭션이 참조하지 못한다.
    * 지속성(Durability)
        * 성공적으로 수행된 트랜잭션은 영원히 반영되어야 한다.
* 트랜잭션의 상태 
    ![problem](/assets/images/transaction-status.png)     
    * 활동(Active)
        * 트랜잭션이 실행 중에 있는 상태, 연산들이 정상적으로 실행 중인 상태
    * 장애(Failed)
        * 트랜잭션이 실행에 오류가 발생하여 중단된 상태
    * 철회(Aborted)
        * 트랜잭션이 비정상적으로 종료되어 Rollback 연산을 수행한 상태
    * 부분 완료(Partially Committed)
        * 트랜잭션이 마지막 연산까지 실행했지만, Commit 연산이 실행되기 직전의 상태
    * 완료(Committed)
        * 트랜잭션이 성공적으로 종료되어 Commit 연산을 실행한 후의 상태


* (추가)undo와 redo의 차이
  * undo는 무언가를 되돌리는 개념(했던 작업을 반대로 진행한다. 원상복구)
  * redo는 무언가를 다시하는 개념(하던 작업을 그대로 다시한다.)

### 2016년 2번

* SQL 작성문제

### 2016년 3번

* TCP SYN Flooding
  * Dos 공격의 일종으로 TCP `3-Way handshaking`의 약점을 공격하는 방식
  * 공격자는 SYN만 수행하고 SYN+ACK응답을 보내지 않는다. 이러면 SERVER는 메모리공간 QUEUE에 이정보를 담아두게 되는데 이러한 요청이 계속오면 메모리가 초과되어 서버가 다운된다.
  * netstat -na | grep SYN 명령어를 통해 QUEUE 내부를 볼 수 있다.

### 2016년 4번

* (다 외워야 함)모듈 간 결합도

* 모듈화의 정의
  * 시스템을 분해하고 추상화하여 소프트웨어의 성능을 향상시키거나 시스템의 디버깅, 시험, 통합이 용이하도록 하는 소프트웨어 설계기법.
  * 소프트웨어를 기능별로 분할하는 것을 의미하며 각 기능을 모듈이라고 한다.

* 모듈화의 목표
  * 모듈 간 결합도의 최소화
  * 모듈 내 요소들 간의 응집도 최대화

* 결합도(Coupling)
  * 모듈간에 상호 의존하는 정도
  * 모듈 상호간 결합도를 낮추어 서로 의존하는 모듈이 적어야 한다.
  * **내용결합도 - 공통결합도 - 제어결합도 - 스탬프결합도 - 자료결합도** 순으로 결합도가 강하다.
    (내 공재 쓰자)

* (중요) 자료 결합도(Data Coupling)
  * 한 모듈이 다른 모듈을 호출할 때, 필요한 자료만을 매개변수로 전달하여 참조하는 경우

  * **(불분명)** 예시) [감리사-2014-49] 다음과 같은 C 프로그램이 주어졌을 때, 모듈 abc와 모듈 def 간의 결합도와 모듈 def의 응집도를 가장 적절하게 나타낸 것은?
    
  ```c
  void abc(void) {     
        int a, b, in;     
        int res;     
        scanf("%d %d %d", &a, &b, &in);     
        res = def(a, b, in);
        printf("result = %d\n", res);
  }
  
  int def(int x, int y, int v) {     
        if(v > 0) {        
              return(x+y);
        } 
        else {        
              return(x-y);
        }
  }
  ```

  * 정답: 자료 결합도(Data Coupling), 교환적 응집도(Communication cohesion)
  
* (중요) 스탬프 결합도(Stamp Coupling)
  * 두 모듈이 동일한 복합 자료구조(배열, 구조체 등)를 매개변수로 전달하여 참조하는 경우
  * 예시) [감리사-2011-28] 다음 코드에서 함수의 결합도는?
  ```c
  struct {
        int x, y;
  } X;
  
  int doSomething(struct X p) {
        return p.x + p.y;
  } 
  ```
  * 정답: 스탬프(stamp) 결합도


* (중요) 제어 결합도(Control Coupling)
  * 한 모듈이 다른 모듈의 내부에서 작용하는 논리적 흐름을 제어하기 위해서 제어 플래그나 정보를 매개변수로 전달하는 경우

    ```c
    void setValue(String name, int value) 
    {   
          if ( name.equals(“height”) ) {
                height = value ;   
          }   
          
          if ( name.equals(“width”) ) {
                width = value ;
          }
    }
    
    void setHeight(int arg) {   _height = arg ; }
    void setWidth(int arg) {   _width = arg ; }
   ```

  * 정답: 제어 결합도(Control Coupling), 논리적 응집도(logical cohesion)

* 외부 결합도(External) Coupling)
  * 모듈들이 외부환경(OS, 컴파일러 등)과 연관되어 있는 경우


* (중요) 공통 결합도(Common Coupling)
  * 모듈들이 동일한 자료영역(전역변수)을 공통으로 조회하는 경우
  * 오류 발생 시, 타 모듈로 전파 가능성이 큼
  * 예시) [감리사-2012-45] 다음 코드에서 함수의 결합도는?
    ```c
    int xyz = 0; 
    int doSomething(int delta) {   
          xyz += delta;   
          return xyz;
    }
   ```


  * 정답: 제어 결합도(Control Coupling), 논리적 응집도(logical cohesion)

* (중요) 내용 결합도(Contents Coupling)
  * 한 모듈이 다른 모듈의 내부 기능 및 자료를 직접 참조하거나 수정하는 경우
  * 한 모듈에서 다른 모듈의 중간으로 분기되는 경우도 해당된다.


> (매우중요)응집도(Cohesion)

* `하나의 모듈 내부의` 처리요소들 간의 기능적 연관성을 측정하는 척도
* 따라서 독립적인 모듈이 되기 위해서는 각 모듈의 응집도가 강해야한다.

* 기능적 응집도(Functional Cohesion)
  * 모듈 내부의 모든 기능요소들이 단일문제와 연관되어 수행될 경우
  * 예시) 코사인 계산 함수

* 순차적 응집도(Sequential Cohesion)
  * 한 활동의 출력이 다음 활동의 입력으로 사용
  * 예시) 파일에서 데이터를 읽고 데이터를 처리하는 기능

* (중요)통신적 응집도(Communicational Cohesion)
  * 서로 다른 기능이 동일자료를 사용하나 처리순서는 상관없음
  * 모듈의 모든 기능이 동일한 자료구조를 참조하거나 업데이트하는 경우
  * 배열 또는 스택에 정의된 함수집합. (pop(), push()..? )

* 절차적 응집도(Procedural Cohesion)
  * 모듈이 다수의 관련 기능을 가질 경우 모듈 안의 구성요소들이 그 기능을 순차적으로 수행하는 경우
  * 관련없는 기능요소가 배열된 순서로 수행되는 것으로 한 모듈내의 활동들이 순차적으로 수행한다.

* 논리적 응집도(Logical Cohesion)
  * 논리적으로 유사한 기능을 수행하지만 서로의 관계는 밀접하지 않음
  * 모든 마우스 및 키보드 입력처리 루틴 그룹화
  * 예시)   [감리사-2010-32] 다음 코드에서 사용된 함수의 응집도는?   

```c  
  void readWrite(int type, int* data, int size) {
        switch(type) {
              0: read(data, size);
              break;
              
              1: write(data, size);
              break;
        }
  }
```

### 2017년 1번

* 화이트박스테스트 VS 블랙박스테스트

![TEST](http://www.dbguide.net/publishing/img/knowledge/110722_ok8_img01.jpg)

### 2017년 2번

* zigbee
  * 직비는 소형, 저전력 디지털 라디오를 이용해 개인 통신망을 구성하여 통신하기 위한 표준 기술이다. IEEE802.15 표준을 따른다.
  * 블루투스도 802.15 표준을 따른다.
  * 블루투스와 비슷하지만 블루투스보다 주파수대역이 낮고 전력소모가 낮다

* (추가)
  * 무선랜/와이파이는 IEEEE802.11을 따른다.

### 2017년 3번

* 공격기법
  * DRdos
    * 라우터에 위치한 반사기능을 이용하여 공격하는 방식
  * ICMP Flooding(= Smurfing)
    * IP의 Broadcast 성질을 이용한 공격기법
    * 다수의 HOST가 존재하는 네트워크에 ICMP echo를 계속보내는 것
  * Tear Drop
    * 네트워크 패킷의 사이즈가 MTU보다 큰 경우 분할하여 헤더에 flag, offset을 이용하여 알려준다.
    * 이 flag, offset값을 조작하여 패킷 재조합을 불가능하게 만드는 공격
  * ping of death
    * ping 명령어로 매우 큰 패킷을 전송하여 수신을 마비시키는 것
  * LAND Attack
    * 송/수신자 아이피를 같게하여 대량의 패킷을 보내는 것
  * ARP Spoofing
    * ARP는 IP주소를 MAC주소로 변환하는 프로토콜로 ARP Table에 주소들을 저장해놓는다.
    * 이를 조작하여 패킷을 가로채는 공격방법


### 2017년 4번

* 포인터개념
  * 택이가 예제찾고 풀이해주기로함

### 2017년 5번

* 브배형 강의, 문제는 해시 충돌횟수를 구하라는 문제

* 해시
  * 사전적의미 = 잘게썰다. 즉, 하나의 문제열을 더 짧은 길이의 값으로 변환하는 것
  * 충돌이 발생할 수 밖에 없는 구조로 충돌해결법이 중요하다.
  
* Index VS Hash
  * 인덱스
    * 데이터에 빠르게 접근하기 위해 <키, 포인터> 쌍으로 구성되는 데이터 구조
  * 해싱
    * 해싱함수를 사용하는 탐색방법
    * 레코드 키를 가지고 해싱 함수의 계산을 통해 변환된 주소에 해당 레코드를 저장한다.
    * Bucket: 동일한 해시 주소를 갖는 레코드들이 저장될 구역, Slot의 집합
    * Slot: 1개의 레코드를 저장할 수 있는 공간
    * Collision: 2개 이상의 레코드가 같은 해시주소를 갖는 현상
    * 장점
      * 빠르다
      * 공간을 적게 차지한다
    * 단점
      * 오버플로우가 발생될 경우 cost가 크다
      * 해시함수 선정이 어렵다.

### (외울거 많음)2017년 6번

* 이진트리 삽입순서 등에 관련된 문제



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


### 2017년 7번

* 자바코드 출력

### 2017년 8번

* 쿼리문 작성

### 2017년 9번

* 디스크 탐색시간 구하기
  * Access Time = Seek Time + Rotational Latency + Transfer Time
  * Seek time: 실린더에 헤드를 위치시키는 시간
  * Rotational Latency: 헤드가 원하는 위치까지 가는 시간
    * rmp/60 = 초당 회전수
    * 초당회전수/1000 = ms당 회전수
    * 1/ ms당 회전수 = 1회전 당 걸리는 시간
  * 예시)
    * 5400rmp
    * 1ms당 9/100바퀴, 1바퀴당 11ms
    * 평균회전시간 = r = 5.5ms (1/2바퀴 걸리는데 걸리는 시간)
  * Transfer Time: 데이터를 전송하는데 걸리는 시간

### 2017년 10번

* [2014년 6번 스케쥴링](https://h-noah.github.io//docs/final-ready#2014%EB%85%84-6%EB%B2%88-%EC%8A%A4%EC%BC%80%EC%A5%B4%EB%A7%81)과 동일


### 2017년 11번

* B트리와 B+트리의 차이를 약술하는 문제

* B트리와 B+트리에 데이터가 삽입/삭제되는 순서
  * 2,3,5,7,9,11,13,15,17... 처럼 오름차순으로 데이터가 삽일될 때 B트리, B+트리의 삽입순서와 최종산출물을 그리시오

### 2017년 12번 

[서브넷마스크 예제](https://tshooter.tistory.com/82)

* 네트워크 서브넷마스크 문제
  * 



### 2018년 1번

* SQL 작성

<<<<<<< HEAD
FROM WHERE SELECT GROUPBY HAVING 우선순위 보기

### ~~2015년 3번~~
### ~~2015년 4번~~

* 출력값. (이부분도 은근히 걱정인데)

### ~~2015년 5번~~

빅오 세타오 오메가오

### 2015년 6번

정렬방법 별 시간복잡도





### 2016년 7번

* 최소신장트리(Minimum Spanning Tree)
-
=======
### 2018년 2번

* [결합도 관련 문제](https://h-noah.github.io/docs/final-ready#2016%EB%85%84-4%EB%B2%88)

### 2018년 3번

* [서브넷마스크 문제](https://h-noah.github.io/docs/final-ready#2017%EB%85%84-12%EB%B2%88)

* 예제)C클래스 네트워크를 24개의 서브넷으로 나누려고 한다. 각 서브넷에는 4~5개의 호스트가 연결되어야 한다. 적절한 서브넷마스크는?
* 풀이)
  * C클래스, 24개 서브넷, 서브넷당 4~5개의 호스트
  * C클래스 디폴트 서브넷마스크 = 255.255.255.0 = 11111111/11111111/11111111/00000000 
  * C클래스는 서브넷마스크를 적용할 수 있는 부분이 마지막 8비트이다.
  * 4~5개의 호스트를 찾기 위해서는 최소 3비트가 필요하다. (네트워크주소와 브로드캐스트주소를 포함하면 6~7개이므로) 따라서 호스트는 오른쪽 3개비트를 사용할 수 있다.
  * 즉, 서브넷마스크가 11111111/11111111/11111111/NNNNN HHH/ 형태로 사용될 것이다(N= NETWORK, H= HOST)
  * 따라서 11111111/11111111/11111111/11111000 = 255.255.255.248이 된다.

* 예제)IP주소가 128.110.121.32(255.255.255.0)인 경우 네트워크 주소는?
* 풀이) 128.110.121.0 이다. 서브넷마스크와 IP주소를 AND연산하면 네트워크 주소가 나온다.

* 예제)IP 203.10.24.27(255.255.255.240)일 때, 네트워크의 호스트 범위와 브로드캐스트 주소는?
* 풀이)255.255.255.240 = 11111111/11111111/11111111/11110000이다. 따라서 네트워크주소는 IP주소와 AND연산하여 203.10.24.16 이며 호스트주소가 14(16-2)개이다. 
* 브로드캐스트주소는 호스트주소 마지막 +1 임,로 203.10.24.31이다.

### 2018년 4번

* 재귀함수 관련 문제

### 2018년 5번

* 복원X

### 2018년 6번

* 플레이페어 암호제작
  * 키 값이 들어간 카이사르 암호과 비슷하다.
  * 암호도표에서 중복된 철자는 하나로 취급한다
  * I, J는 구별하지 않고 하나로 취급한다. (총 25개)
  * 키 값이 Orchidee인 경우의 암호도표   

  ![encrpyt](https://mblogthumb-phinf.pstatic.net/20160917_79/shthddn90_1474105865933yC9K4_JPEG/20160917_185026.jpg?type=w800)


  * 암호화 할 문장: i come on Wednesday
  * 암호화 방법
    1. 2글자씩 쪼갠다 = ic om eo nw ed ne sd ay
      * case1. 두 철자가 같은 가로줄 안에 있는 경우 ex) ic -> rh, fe -> da
        * 바로 다음 철자를 선택한다. 만약 다음 철자가 없는 경우 처음 철자로 선택한다.
      * case2. 두 철자가 같은 세로줄 안에 있는 경우 ex) sa -> xl, zn -> iu
        * 바로 아래 철자를 선택한다. 만약 다음 철자가 없는 경우 처음 철자로 선택한다.
      * case3.... 이런방식

* DES, AES, RSA 공부 함께합시다.

### 2018년 7번

* RAIO 관련 문제

### 2018년 8번

* CPU 스케쥴링 알고리즘

### (추가)리눅스 명령어

  * cron

  * chmod
>>>>>>> f70938e5734ff9b10e630b2757f0e827a7321829
