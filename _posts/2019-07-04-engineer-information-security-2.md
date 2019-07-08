---
title: "[요약]정보보안기사-네트워크"
permalink: docs/engineer-information-security(2)
last_modified_at: 2019-07-04T17:56:49-04:00
excerpt: "정보보안기사 대비(네트워크)"
toc: true
classes: wide
author_profile: false
sidebar:
  title: "Order List"
  nav: sidebar-sample
tags:
  - network
  - computer

---

## 운영체제

### 프로세스 명령 실행주기를 적으시오.

- Fetch -> Decode -> Excute

### 캐시메모리 사상방식 3가지를 적고 장/단점을 적으시오.

- Direct/Associate/혼합형
 
### (중요)캐시메모리 교체알고리즘 & Page Fault 횟수    
![FIFO-1](https://mblogthumb-phinf.pstatic.net/20120605_169/kyung778_1338902847430wA0MX_JPEG/FIFO.jpg?type=w2)

* **한 프로세스에게 할당된 페이지가 가득 찬 경우, 다음 페이지를 작업하기 위해 가장 먼저 올라간 페이지를 교체한다**
![FIFO-2](https://mblogthumb-phinf.pstatic.net/20120607_23/kyung778_1339068905504cjFU2_PNG/FIFO.PNG?type=w2)
* Belady의 변치(FIFO 모순)
    - 프로세스에 할당된 페이지 수가 증가하면 page fault가 줄어들어야 하지만 현실적으로 더 증가하는 경우가 발생한다.
* page fault란?
    - 캐시에 올라간 데이터를 page 단위로 처리한다.
    - 일반적으로 사용하고자 하는 데이터가 캐시되어 있지 않을 때 발생한다. 

![LFU-1](https://mblogthumb-phinf.pstatic.net/20120605_165/kyung778_1338902847737YjBKd_JPEG/LFU.jpg?type=w2)


* **Least Frequently Used의 약어로 가장 빈번하지 않게 사용되는 즉, 제일 참조가 안되었던 순서로 교체한다.**

![LFU-2](https://mblogthumb-phinf.pstatic.net/20120607_234/kyung778_1339069005438fGnnr_PNG/LFU.PNG?type=w2)

![LRU-1](https://mblogthumb-phinf.pstatic.net/20120605_58/kyung778_1338902847942gsAbq_JPEG/LRU.jpg?type=w2)

* **Least Recently Used의 약어로 가장 빈번하지 않게 사용되는 즉, 가장 사용한지 오래된 녀석부터 교체한다**

![LRU-2](https://mblogthumb-phinf.pstatic.net/20120607_23/kyung778_1339068905504cjFU2_PNG/FIFO.PNG?type=w800)

### (중요)데드락에 대한 설명과 발생조건, 해결방법

* 데드락은 아래의 네 조건을 모두 만족(**AND 조건**)할 때 발생한다.
    1. Mutual exclusion: 자원 동시접근 불가
    2. Hold and wait: 할당된 자원을 가진 상태에서 다른 자원을 대기
    3. circular queue: 순환형태 대기
    4. non-preemption: 다른 프로세스의 자원을 선점할 수 없음

* 데드락 예방(Prevention)
    - 따라서, 위 네 가지 조건 중 **하나만 풀어내도 데드락은 발생하지 않는다.**

* 데드락 회피(Avoidance)
    - 지나치게 보수적이라 병렬성이 감소될 수 있으며 병목현상 발생가능성이 있다.

     1. (Resource 1개)자원 할당 그래프 알고리즘
        - 자원할당 graph에 request edge와 allocate edge를 추가하여 claim edge를 도입한다.
        - 그래프에 사이클이 존재할 때, 교착상태 가능성

        ![allocatio-graph](https://t1.daumcdn.net/cfile/tistory/201B9A494FA1FC3131)

        * 교착상태

        ![allocatio-graph](https://t1.daumcdn.net/cfile/tistory/201B9A494FA1FC3131)

        * 비교착상태 (P1 종류 후, P3에 R3 할당하면 해결)

    1. Banker's algorithm
        - safe state를 유지할 수 있는 요규만을 수락하는 방법
        - (중요)최대 요구자원수에 대한 정보가 있을 경우에 수행가능
        
        
        ```c++
        int Available[]; //사용가능한 자원의 수
        int request[][]; //추가요구량 (Max - Allocation)
        int Max[][]; //프로세스 별 최대 자원의 요구
        int Allocation[][]; //현재 프로세스 별 할당된 자원 수
        ```

        > MAX[A] = 10, MAX[B] = 5, MAX[C] = 7

        ![problem](/assets/images/bankers-1.png)

        * Safe state인지 확인하기 위해 Need가 가장 적게 남은 프로세스부터 리소스를 할당해주고 반환받아보자.

        ![problem](/assets/images/bankers-2.png)

        * 위 경우 `P3-P1-P4-P2-P0`, `P1-P3-P4-P0-P2`도 가능한 등 많은 경우가 SAFE하다.

        * 아래는 다른 방식으로 해석한 것이다

        ![bankers-1](http://www.jidum.com/upload/ckeditor/2016/09/20160908140937598.png)

        * Available을 구한다.

        ![bankers-2](http://www.jidum.com/upload/ckeditor/2016/09/20160908141003714.png)

        * Request를 구한다. (Request = Max-Allocation)

        ![bankers-3](http://www.jidum.com/upload/ckeditor/2016/09/20160908141142168.png)

        * Request가 Available보다 적은 프로세스를 찾는다.

        ![bankers-4](http://www.jidum.com/upload/ckeditor/2016/09/20160908141235670.png)

        * 수행가능한 프로세스가 점유한 자원(Allocation)을 여유 자원(Available)로 반환한 뒤, 다시 Request가 Available보다 적은 프로세스를 찾는다. (Available = Available + Allocation)


* 데드락 감지(Detection)
    - Banker's algorithm과 유사하다. 단, Detection은 예상이아니라 현재상태만 보고 데드락인지 아닌지 판단하면 되므로 좀 더 간단하다. 
    - 즉, Request 리소스와 Available 리소스를 비교하여 Deadlock을 판단한다.

### (중요)디스크 스케쥴링 알고리즘

* FCFS(First Come First Scan)
    - 선입선출, 빠르지는 않다.
    - `start = 53`, 53->98->183->37->122->14->124->65->67

    ![FCFS-1](https://mblogthumb-phinf.pstatic.net/20130726_4/jevida_1374822482883XyVjE_PNG/2.png?type=w2)

* SSTF(Shortest Seek Time First)
    - 가장 가까운 것부터 이동
    - `start = 53` 53->65->67->37->98->122->124->183->199
    - starvation 발생가능.

    ![SSTF-1](https://mblogthumb-phinf.pstatic.net/20130726_85/jevida_1374822483023IKYq8_PNG/3.png?type=w2)

* SCAN(SCAN Scheduling)
    - 일명 엘리베이터 알고리즘, 한 끝에서 시작하여 다른 끝으로 이동 (현재 진행중인 방향으로 가장 짧은 탐색 거리에 있는 요청을 먼저 서비스
    - `start = 53` 53->37->14->0->65->67->98->122->124->183   
    - 또는, 53->65->67->98->122->124->183->37->14

    ![SCAN](https://mblogthumb-phinf.pstatic.net/20130726_158/jevida_1374822483175TOygk_PNG/4.png?type=w2)


* C-SCAN(C-SCAN Scheduling)
    - SCAN의 변형버전.
    - 역방향으로 도는 것이 아니라. 처음 시작했던 자리로 다시 되돌아가서 스캔한다.
    - 디스크는 원형이므로 끝점 = 시작점이다.
    - 따라서, 53->65->67->98->122->124->183->199->0->14->37;

    ![SCAN](https://t1.daumcdn.net/cfile/tistory/99C6553C5BDF03AF30)


* (중요)LOOK
    - SCAN의 강화버전.
    - **SCAN, C-SCAN은 요청이 없어도 끝까지 가야하므로 비효율적이다.**
    
    * SCAN VS LOOK

    ![SCAN](https://t1.daumcdn.net/cfile/tistory/997ABB3C5BDF03B026)

    ![LOOK](https://t1.daumcdn.net/cfile/tistory/993BC6455BDF09B605)


* (중요)C-LOOK
    - C-SCAN의 강화버전.
       
    * C-SCAN VS C-LOOK
    
    ![SCAN](https://t1.daumcdn.net/cfile/tistory/99C6553C5BDF03AF30)

    ![LOOK](https://t1.daumcdn.net/cfile/tistory/9992D4455BDF09B60D)


## (거름)RAID

- Claydox 