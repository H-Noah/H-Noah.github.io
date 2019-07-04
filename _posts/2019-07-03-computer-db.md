---
title: "[요약]데이터베이스"
permalink: docs/computer-db
last_modified_at: 2019-06-27T17:58:49-04:00
excerpt: "db에 관한 지식 중 핵심만 요약한 포스트입니다."
toc: true
classes: wide
author_profile: false
sidebar:
  title: "Order List"
  nav: sidebar-sample
tags:
  - Database
  - computer

---

## 질문

1. 트랜잭션/ACID
    * 트랜잭션이란?
    * 트랜잭션의 성질 4가지를 쓰시오.

2. 조인
    * 조인이란 무엇이고 그 종류와 종류별 사용예시를 쓰시오.    
    

## DB 쿼리 연습

- http://sqlfiddle.com/
- 무설치형태로 쿼리를 연습할 수 있다.
- 연습문제를 찾아서 풀도록

### 데이터베이스 정규화 

- 정규화 이론과 문제를 풀도록

## DB 이론

### 트랜잭션이란
* 트랜잭션(Transaction) 이란
    * 데이터베이스의 상태를 변환시키는 논리적인 작업 단위(연산의 집합)
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



### Join
* 조인이란
    * **한 데이터베이스 내의 여러 테이블의 레코드를 조합하여 하나의 열로 표현한 것**이다.
* 조인의 필요성
    * 각 테이블에 저장된 데이터를 효과적으로 검색하기 위해 
    * 정규화를 수행하면 각 테이블끼리 관계(Relationship)를 갖게 된다. 그러나, 서로 관계있는 데이터가 나뉘어 저장되므로 조인이 필요하다.
    ![problem](/assets/images/join-table.png)     

* 조인의 종류
    1. **내부 조인(INNER JOIN)**
        * 가장 흔한 결합 방식으로 기본 조인 형식이다.
        * 2개의 테이블(A, B)의 컬럼 값을 결합함으로써 새로운 결과 테이블을 생성한다.        
        * 명시적 조인 표현
            * JOIN 키워드를 사용하며 ON 키워드로 구문을 지정한다.
                ```sql
                SELECT *
                FROM employee INNER JOIN department
                ON employee.DepartmentID = department.DepartmentID;
                ```
        * 암시적 조인 표현
            * SELECT 구문의 FROM 절에서 컴마를 사용해서 테이블을 나열하기만 한다.
                ```sql
                SELECT *
                FROM employee, department
                WHERE employee.DepartmentID = department.DepartmentID;
                ```
        * 결과  
            ![problem](/assets/images/inner-join.png)                 
        1. **자연 조인(NATURAL JOIN)**
            * 동등 조인의 한 유형으로 조인 구문이 조인된 테이블에서 동일한 컬럼명을 가진 2개의 테이블에서 모든 컬럼들을 비교함으로써, 암시적으로 일어나는 구문이다.
            * 결과적으로 나온 조인된 테이블은 동일한 이름을 가진 컬럼의 각 쌍에 대한 단 하나의 컬럼만 포함하고 있다.
            * SQL
                ```sql
                SELECT * FROM employee NATURAL JOIN department;
                ```
            * 결과  
                ![problem](/assets/images/natural-join.png)
        2. **교차 조인(CROSS JOIN)**
            * 조인되는 두 테이블에서 곱집합을 반환한다. 
            * 즉, 두 번째 테이블로부터 각 행과 첫 번째 테이블에서 각 행이 한번씩 결합된 열을 만들 것이다.
            * 예를 들어 m행을 가진 테이블과 n행을 가진 테이블이 교차 조인되면 m*n 개의 행을 생성한다 
            ```sql
            SELECT * FROM employee CROSS JOIN department;
            ```
            * 결과  
                ![problem](/assets/images/cross-join.png)
    2. **외부 조인(OUTER JOIN)**
        * 조인 대상 테이블에서 **특정 테이블의 데이터가 모두 필요한 상황**에서 외부 조인을 활용하여 효과적으로 결과 집합을 생성할 수 있다.
        1. **왼쪽 외부 조인(LEFT OUTER JOIN)**            
            * **좌측 테이블의 모든 데이터를 포함하는 결과** 집합을 생성한다.
            * SQL
                ```sql
                SELECT *
                FROM employee LEFT OUTER JOIN department
                ON employee.DepartmentID = department.DepartmentID;
                ```
            * 결과 
                ![problem](/assets/images/left-outer-join.png)                 
        2. **오른쪽 외부 조인(RIGHT OUTER JOIN)**            
            * 즉, **우측 테이블의 모든 데이터를 포함**하는 결과 집합을 생성한다.
            * SQL
                ```sql
                SELECT *
                FROM employee RIGHT OUTER JOIN department
                ON employee.DepartmentID = department.DepartmentID;
                ```
            * 결과  
                ![problem](/assets/images/right-outer-join.png)                 
        3. **완전 외부 조인(FULL OUTER JOIN)**
            * 양쪽 테이블 모두 OUTER JOIN이 필요할 때 사용한다.
            * SQL
                ```sql
                SELECT *
                FROM employee FULL OUTER JOIN department
                ON employee.DepartmentID = department.DepartmentID;
                ```
            * 결과 
                ![problem](/assets/images/full-outer-join.png)                  

### 파티셔닝
* 파티셔닝의 개념
  * **큰 table이나 index를, 관리하기 쉬운 partition이라는 작은 단위로 물리적으로 분할하는 것을 의미**한다. 하나의 DBMS에 너무 큰 table이 들어가면서 용량과 성능 이슈가 발생, 이를 해결하기 위한 방법으로 생성되었다.    
* 파티셔닝의 장점
  * 데이터 가용성 향상
  * 검색속도 향상
  * UPDATE 성능 향상    
* 파티셔닝의 단점
  * JOIN 비용  
* 파티셔닝의 종류
  1. 수평(horizontal) 파티셔닝 = **샤딩(Sharding)**      
  2. 수직(vertical) 파티셔닝
  ![problem](/assets/images/right-outer-join.png)                 

### 샤딩
  * 샤딩은 물리적으로 다른 데이터베이스에 데이터를 수평 분할 방식으로 분산 저장하고 조회하는 방법을 말한다.
  * 샤딩은 주로 키값(해쉬값 또는 특정 컬럼값)을 이용하여 테이블들의 데이터 자체를 나눠서 분산저장하거나, 특정 분류기준을 가지고(저장 데이터 종류-유저, 일반데이터 등) 테이블을 분류하여 저장하는 것
  * 샤딩은 수평 파티션과 동일한 개념이다.
  * ex) '주민' 테이블이 여러 DB에 있을 때, 서현동 주민에 대한 정보는 A DB에, 정자동 주민에 대한 정보는 B DB에 저장되도록 하는 방식을 말한다. 여러 데이터베이스를 대상으로 작업해야 하기 때문에 경우에 따라서는 기능에 제약이 있을 수 있고(JOIN 연산 등) 일관성(consistency)과 복제(replication) 등에서 불리한 점이 많다. 