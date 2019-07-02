---
title: "[요약]컴퓨터 네트워크"
permalink: docs/computer-network-1
last_modified_at: 2019-06-27T17:58:49-04:00
excerpt: "컴퓨터 네트워크에 관한 지식 중 핵심만 요약한 포스트입니다."
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

## 질문

### Q1. OSI 7계층에 대해 설명하시오.

### Q2. TCP/UDP에 대해 설명/비교하시오.

### Q3. TCP의 3way handshake와 4way handshake를 비교/설명하시오. (추가)

### Q4. HTTP와 HTTPS에 대해 설명하고 장/단점을 비교하시오.

### Q5. CORS란(추가)

### Q6. GET과 POST에 대해 설명하시오. GET/POST의 쓰임을 쓰시오. 장/단점을 비교하시오.

### Q7. REST와 REST API에 대해 설명하시오.


## 정답

### OSI 7계층

* OSI(Open Systems Interconnection Reference Model)란
    <img src=".assets/images/osi-7-layer.png" width="60%" height="60%">
    * 컴퓨터 네트워크 프로토콜 디자인과 통신을 계층으로 나누어 설명한 것이다.    

1. 물리 계층(Physical layer)    
    * 네트워크의 높은 수준의 논리 데이터 구조를 기초로 하는 필수 계층이다.
    * 전송 단위는 Bit이다.
2. 데이터 링크 계층(Data link layer)
    * **포인트 투 포인트**간 전송을 보장하기 위한 계층. **ex)이더넷**
    * 주소 값은 물리적으로 할당 받는다. 즉, 네트워크 카드가 만들어질 때부터 맥 주소(MAC address)가 정해져 있다.     
    * 데이터 전송 단위는 Frame이다. 
3. 네트워크 계층(Network layer)
    * 경로를 찾아주는 역할을 하는 계층으로 데이터를 전달하고, 그 과정에서 전송 계층이 요구하는 서비스 품질(QoS)을 제공하기 위한 기능적, 절차적 수단을 제공한다. 
    * 네트워크 계층은 라우팅, 세그멘테이션, 흐름 제어 등을 수행한다.
    * 데이터 전송 단위는 Datagram(Packet)이다.
4. 전송 계층(Transport layer)
    * **End to end**의 사용자들이 유효한 데이터를 효율적으로 받을 수 있도록 해준다.    
    * 전송 계층은 유효성을 제어하고, 연결 기반(connection oriented)이다. (이는 전송 계층이 패킷들의 전송이 유효한지 확인하고 전송 실패한 패킷들을 다시 전송한다는 것을 뜻한다.) 
    * 가장 잘 알려진 **전송 계층의 예는 TCP**이다.
    * 데이터 전송 단위는 Segment이다.
5. 세션 계층(Session layer)
    * 프로세스가 **통신을 관리하기 위한 방법을 제공**한다. 
    * 동시 송수신 방식(duplex), 반이중 방식(half-duplex), 전이중 방식(Full Duplex)의 통신과 함께, 체크 포인팅과 유휴, 종료, 다시 시작 과정 등을 수행한다. 
    * 이 계층은 **TCP/IP 세션을 만들고 없애는 책임**을 진다.
6. 표현 계층(Presentation layer)
    * **코드 간의 번역을 담당**하여 데이터의 형식상 차이를 다루는 부담을 응용 계층으로부터 덜어 준다. 
    * **MIME 인코딩이나 암호화** 등의 동작이 이 계층에서 이루어진다. 
7. 응용 계층(Application layer)
    * 응용 프로세스와 일반적인 응용 서비스를 수행한다. 
    * 일반적인 응용 서비스는 관련된 **응용 프로세스들 사이의 전환을 제공**한다. 


### TCP/UDP

* TCP(Transmission Control Protocol)      
    * 데이터를 메세지의 형태(**세그먼트**)로 보내기 위해 IP와 함께 사용하는 **프로토콜**이다.
     ![problem](/assets/images/tcp-virtual-circuit.png)    
    * IP가 데이터의 배달을 처리 TCP는 패킷 추적 및 관리 역할.    
    * **연결형 서비스로** 가상 회선 방식을 제공한다.
        * 3-way handshaking을 통해 연결설정, 4-way handshaking을 통해 연결해제.
    * 흐름제어 및 혼잡제어를 제공한다.
        * 흐름제어
            * 데이터 송신/수신 처리 속도를 조절하여 오버플로우를 방지            
        * 혼잡제어
            * 네트워크 내의 패킷 수 조절                
    * 전이중(Full-Duplex), 점대점(Point to Point) 방식이다.
        * 전이중
            * 전송이 양방향으로 동시에 일어날 수 있다.
        * 점대점
            * 각 연결이 정확히 2개의 종단점을 가지고 있다.
        * 멀티캐스팅이나 브로드캐스팅을 지원하지 않는다.
    * **연속성보다 신뢰성있는 전송이 중요할 때에 사용**된다.
* UDP(User Datagram Protocol)     
    ![problem](/assets/images/udp-datagram.png)    
    * 데이터를 **데이터그램** 단위로 처리하는 프로토콜이다.
    * **비연결형 서비스로** 데이터그램 방식을 제공한다.
        * 연결을 위해 할당되는 논리적인 경로가 없다. 패킷은 다른 경로로 전송되고 독립적이다. 
    * UDP헤더의 CheckSum 필드를 통해 최소한의 오류만 검출한다.    
    * **신뢰성보다는 연속성이 중요한 서비스, 예를 들면 실시간 서비스(streaming)에 사용**된다.
* 참고
  * UDP와 TCP는 각각 별도의 포트 주소 공간을 관리하므로 같은 포트 번호를 사용해도 무방하다. 
  * 또한 같은 모듈(UDP or TCP) 내에서도 클라이언트 프로그램에서 동시에 여러 커넥션을 확립한 경우에는 서로 다른 포트 번호를 동적으로 할당한다. (동적할당에 사용되는 포트번호는 49,152~65,535이다.)


### (추가)3-way handshake

* 즉, TCP/IP 프로토콜을 이용하는 응용 프로그램이 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정.
    * A 프로세스(Client)가 B 프로세스(Server)에 연결을 요청
      ![problem](/assets/images/3-way-handshaking.png)     
      1. A -> B: SYN
          * 접속 요청 프로세스 A가 연결 요청 메시지 전송 (SYN)
          * 송신자가 최초로 데이터를 전송할 때 Sequence Number를 임의의 랜덤 숫자로 지정하고, SYN 플래그 비트를 1로 설정한 세그먼트를 전송한다.
          * PORT 상태 - B: LISTEN, A: CLOSED
      2. B -> A: SYN + ACK
          * 접속 요청을 받은 프로세스 B가 요청을 수락했으며, 접속 요청 프로세스인 A도 포트를 열어 달라는 메시지 전송 (SYN + ACK)
          * 수신자는 Acknowledgement Number 필드를 (Sequence Number + 1)로 지정하고, SYN과 ACK 플래그 비트를 1로 설정한 세그먼트를 전송한다.
          * PORT 상태 - B: SYN_RCV, A: CLOSED
      3. A -> B: ACK
          * PORT 상태 - B: SYN_RCV, A: ESTABLISHED
          * 마지막으로 접속 요청 프로세스 A가 수락 확인을 보내 연결을 맺음 (ACK)
          * 이때, 전송할 데이터가 있으면 이 단계에서 데이터를 전송할 수 있다.
          * PORT 상태 - B: ESTABLISHED, A: ESTABLISHED

### (추가)4-way handshake 
  * TCP의 **연결을 해제(Connection Termination)** 하는 과정
      * A 프로세스(Client)가 B 프로세스(Server)에 연결 해제를 요청
        ![problem](/assets/images/4-way-handshaking.png)   
        1. A -> B: FIN
            * 프로세스 A가 연결을 종료하겠다는 FIN 플래그를 전송
            * 프로세스 B가 FIN 플래그로 응답하기 전까지 연결을 계속 유지
        2. B -> A: ACK
            * 프로세스 B는 일단 확인 메시지를 보내고 자신의 통신이 끝날 때까지 기다린다. (이 상태가 TIME_WAIT 상태)
            * 수신자는 Acknowledgement Number 필드를 (Sequence Number + 1)로 지정하고, ACK 플래그 비트를 1로 설정한 세그먼트를 전송한다.
            * 그리고 자신이 전송할 데이터가 남아있다면 이어서 계속 전송한다.
        3. B -> A: FIN
            * 프로세스 B가 통신이 끝났으면 연결 종료 요청에 합의한다는 의미로 프로세스 A에게 FIN 플래그를 전송
        4. A -> B: ACK
            * 프로세스 A는 확인했다는 메시지를 전송
* 참고 - ***포트(PORT) 상태 정보***
  * CLOSED: 포트가 닫힌 상태
  * LISTEN: 포트가 열린 상태로 연결 요청 대기 중
  * SYN_RCV: SYNC 요청을 받고 상대방의 응답을 기다리는 중
  * ESTABLISHED: 포트 연결 상태
  

### HTTP와 HTTPS
- HTTP 프로토콜
    - 개념 
        - HyperText Transfer Protocol
        - 웹 상에서 클라이언트와 서버 간에 요청/응답(request/response)으로 정보를 주고 받을 수 있는 **프로토콜**
    - 특징 
        - 주로 HTML 문서를 주고받는 데에 쓰인다. 
        - TCP와 UDP를 사용하며, **80번 포트**를 사용한다.
        - 1) 비연결(Connectionless)
            - 클라이언트가 요청을 서버에 보내고 서버가 적절한 응답을 클라이언트에 보내면 바로 연결이 끊긴다.
        - 2) 무상태(Stateless)
            - 연결을 끊는 순간 클라이언트와 서버의 통신은 끝나며 상태 정보를 유지하지 않는다.
- HTTPS 프로토콜 
    - 개념 
        - HyperText Transfer Protocol over Secure Socket Layer            
        - 보안이 강화된 버전의 HTTP
    - 특징 
        - HTTPS의 기본 TCP/IP 포트로 **443번 포트**를 사용한다.
        - HTTPS는 소켓 통신에서 일반 텍스트를 이용하는 대신에, 웹 상에서 정보를 암호화하는 SSL이나 TLS(발전형 SSL) 프로토콜을 통해 **세션 데이터를 암호화**한다.            

- HTTPS가 필요한 이유?
    - 웹브라우저가 서버에 HTTP를 통해 정보를 요청하면 서버는 응답하여 정보를 제공.
    - HTML은 텍스트이다. 따라서, 중간에서 민감정보를 볼 수 없도록 주고받는 정보를 암호화한다.

- HTTPS의 원리 
    - **[공개키 알고리즘 방식](https://github.com/WeareSoft/tech-interview/blob/master/contents/security.md#대칭키와-비대칭키-차이)**
    - 서로 다른 키(공개키, 개인키)를 이용한 암호화 방법       
    - 클라이언트 -> 서버 
        - 사용자의 데이터를 **공개키로 암호화** (공개키를 얻은 인증된 사용자)
        - 서버로 전송 (데이터를 가로채도 개인키가 없으므로 **복호화할 수 없음**)
        - 서버의 **개인키를 통해 복호화**하여 요청 처리 
- HTTPS의 장단점
    - 장점 
        - 네트워크 상에서 열람, 수정이 불가능하므로 안전하다.
    - 단점 
        - 암호화를 하는 과정이 웹 서버에 부하를 준다.
        - HTTPS는 설치 및 인증서를 유지하는데 추가 비용이 발생한다.
        - HTTP에 비해 느리다. 
        - 인터넷 연결이 끊긴 경우 재인증 시간이 소요된다.
            - HTTP는 비연결형으로 웹 페이지를 보는 중 인터넷 연결이 끊겼다가 다시 연결되어도 페이지를 계속 볼 수 있다.

### (추가)CORS란 
- CORS(Cross Origin Resource **Sharing**)란 
    - 웹 서버에게 보안 cross-domain 데이터 전송을 활성화하는 접근 제어권을 부여한다.
- 배경
    - 처음 전송되는 리소스의 도메인과 다른 도메인으로부터 리소스가 요청될 경우 해당 리소스는 cross-origin HTTP 요청에 의해 요청된다.
    - 보안 상의 이유로, 브라우저들은 스크립트 내에서 초기화되는 cross-origin HTTP 요청을 제한한다.
        - 예를 들면, XMLHttpRequest는 same-origin 정책을 따르기에 XMLHttpRequest을 사용하는 웹 애플리케이션은 자신과 동일한 도메인으로 HTTP 요청을 보내는 것만 가능했다.
        - 웹 애플리케이션을 개선시키기 위해, 개발자들은 브라우저 벤더사들에게 XMLHttpRequest가 cross-domain 요청을 할 수 있도록 요청했고 이에 따라 CORS가 생겼다.
- 과정
    - CORS 요청 시에는 미리 OPTIONS 주소로 서버가 CORS를 허용하는지 물어본다.
    - 이때 Access-Control-Request-Method로 실제로 보내고자 하는 메서드를 알리고,
    - Access-Control-Request-Headers로 실제로 보내고자 하는 헤더들을 알린다.
    - Allow 항목들은 Request에 대응되는 것으로, 서버가 허용하는 메서드와 헤더를 응답하는데 사용된다.
    - Request랑 Allow가 일치하면 CORS 요청이 이루어진다.


### (추가)GET/POST

* HTTP 프로토콜을 이용해서 서버에 데이터(요청 정보)를 전달할 때 사용하는 방식
* GET 
  * 개념
    * 정보를 조회하여 보여주기 위한 위한 메서드 (**가져오는 것(Select)**)
  * 사용 방법
    * Query String
    * Ex) `www.urladdress.xyz?name1=value1&name2=value2`    
  * 특징
    * URL에 요청 정보를 붙여서 전송한다.따라서, 길이 제한(255자)이 있다. 
      * HTTP/1.1은 2048자
    * POST 방식보다 보안상 취약하다.          
    * POST 방식보다 빠르다. (캐싱사용 가능)      
* POST
  * 개념
    * 서버의 값이나 상태를 바꾸기 위한 용도의 메서드(**수행하는 것(Insert, Update, Delete)**)    
  * 사용 방법
    * 요청 정보를 HTTP 패킷의 Body 안에 숨겨서 서버로 전송한다.
    <!-- * Form 태그을 이용해서 submit 하는 형태 -->
    * Request Header의 Content-Type에 해당 데이터 타입이 표현되며, 전송하고자 하는 데이터 타입을 적어주어야 한다.
      * Default: application/octet-stream
      * 단순 txt의 경우: text/plain
      * 파일의 경우: multipart/form-date
  * 특징
    * Body 안에 숨겨서 요청 정보를 전송하기 때문에 대용량의 데이터를 전송하기에 적합하다.
    * 클라이언트 쪽에서 데이터를 인코딩, 받은 서버 쪽이 데이터를 디코딩한다.    

* Q. 조회하기 위한 용도 POST가 아닌 GET 방식을 사용하는 이유?
  1. 설계 원칙에 따라 GET 방식은 서버에게 여러 번 요청을 하더라도 동일한 응답이 돌아와야 한다. (Idempotent, 멱등)
      * GET 방식은 **가져오는 것(Select)** 으로, 서버의 데이터나 상태를 변경시키지 않아야 한다.
          * Ex) 게시판의 리스트, 게시글 보기 기능
          * 예외) 방문자의 로그 남기기, 글을 읽은 횟수 증가 기능
      * POST 방식은 **수행하는 것** 으로, 서버의 값이나 상태를 바꾸기 위한 용도이다.
          * Ex) 게시판에 글쓰기 기능
  2. 웹에서 모든 리소스는 Link할 수 있는 URL을 가지고 있어야 한다.
      * 어떤 웹페이지를 보고 있을 때 다른 사람한테 그 주소를 주기 위해서 주소창의 URL을 복사해서 줄 수 있어야 한다.
      * 즉, 어떤 웹페이지를 조회할 때 원하는 페이지로 바로 이동하거나 이동시키기 위해서는 해당 링크의 정보가 필요하다.
      * 이때 POST 방식을 사용할 경우에 값(링크의 정보)이 Body에 있기 때문에 URL만 전달할 수 없으므로 GET 방식을 사용해야한다. 그러나 글을 저장하는 경우에는 URL을 제공할 필요가 없기 때문에 POST 방식을 사용한다.

### (추가)쿠키와 세션

* 쿠키와 세션의 필요성
    * HTTP 프로토콜 현재 사용자가 이전 사용자와 같은지 알 수 없다.    
    * 따라서, HTTP에서 상태를 유지하기 위한 기술로 쿠키와 세션이 있다.
* 쿠키(Cookie)란?
  * 개념
      * 로컬에 저장되는 키와 값이 들어있는 파일로 이름, 값, 유호 시간 등을 포함.      
  * 동작 방식
      ![problem](/assets/images/cookie-process.png)     
      1. 웹브라우저가 서버에 요청
      2. 상태를 유지하고 싶은 값을 쿠키(cookie)로 생성
      3. 서버가 응답할 때 HTTP 헤더(Set-Cookie)에 쿠키를 포함해서 전송
          ```java
          Set−Cookie: id=doy
          ```
      4. 전달받은 쿠키는 웹브라우저에서 관리하고 있다가, 다음 요청 때 쿠키를 HTTP 헤더에 넣어서 전송
          ```java
          cookie: id=doy
          ```
      5. 서버에서는 쿠키 정보를 읽어 이전 상태 정보를 확인한 후 응답
  * 쿠키 사용 예
      * 아이디, 비밀번호 저장
      * 쇼핑몰 장바구니
* 세션(Session)이란?
  * 개념
      * **일정 시간 동안** 브라우저의 요청을 하나의 상태로 보고 그 상태를 유지하는 기술이다.
      * 즉, 웹 브라우저를 통해 접속한 이후부터 종료할 때까지 유지되는 상태이다.
  * 동작 방식
      ![problem](/assets/images/session-process.png)     
      1. 웹브라우저가 서버에 요청
      2. 서버가 해당 웹브라우저(클라이언트)에 유일한 ID(Session ID)를 부여함
      3. 서버가 응답할 때 HTTP 헤더(Set-Cookie)에 Session ID를 포함해서 전송  
      쿠키에 Session ID를 JSESSIONID 라는 이름으로 저장
          ```java
          Set−Cookie: JSESSIONID=xslei13f
          ```
      4. 웹브라우저는 이후 웹브라우저를 닫기까지 다음 요청 때 부여된 Session ID가 담겨있는 쿠키를 HTTP 헤더에 넣어서 전송
          ```java
          Cookie: JSESSIONID=xslei13f
          ```
      5. 서버는 세션 ID를 확인하고, 해당 세션에 관련된 정보를 확인한 후 응답
  * 세션 사용 예
    * 로그인
> 세션도 쿠키를 사용하여 값을 주고받으며 클라이언트의 상태 정보를 유지한다.  
> 즉, 상태 정보를 유지하는 수단은 **쿠키** 이다.
* 쿠키와 세션의 차이점
  * **쿠키 - 빠르고 보안취약하고 휘발성, 세션은 반대.**
  * 저장 위치
      * 쿠키 : 클라이언트
      * 세션 : 서버
  * 보안
      * 쿠키 : 클라이언트에 저장되므로 보안에 취약하다.
      * 세션 : 쿠키를 이용해 Session ID만 저장하고 이 값으로 구분해서 서버에서 처리하므로 비교적 보안성이 좋다.
  * 라이프사이클
      * 쿠키 : 만료시간에 따라 브라우저를 종료해도 계속해서 남아 있을 수 있다.
      * 세션 : 만료시간을 정할 수 있지만 브라우저가 종료되면 만료시간에 상관없이 삭제된다.
  * 속도
      * 쿠키 : 클라이언트에 저장되어서 서버에 요청 시 빠르다.
      * 세션 : 실제 저장된 정보가 서버에 있으므로 서버의 처리가 필요해 쿠키보다 느리다.

### (추가)REST/RESTful

* REST란
  * REST의 정의
    * "Representational State Transfer(대표적인 상태 전달)"의 약자로 Client와 Server 사이의 통신 방식 중 하나이다.
  * REST의 구체적인 개념
    * **HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP Method(Post, Get, Put, Delete)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미한다.**      
  * REST 장단점
    * 장점      
      * 범용성을 보장한다.
      * HTTP 프로토콜의 표준을 최대한 활용
    * 단점      
      * 구형 브라우저에서 PUT, DELETE를 사용하지 못한다.          
  * REST 구성 요소
    1. 자원(Resource): URI
        * 모든 자원에 고유한 ID가 존재하고, 이 자원은 Server에 존재한다.
        * 자원을 구별하는 ID는 '/groups/:group_id'와 같은 HTTP **URI** 다.
        * Client는 URI를 이용해서 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 Server에 요청한다.
    2. 행위(Verb): HTTP Method        
        * HTTP 프로토콜은 **GET, POST, PUT, DELETE, HEAD** 와 같은 메서드를 제공한다.
    3. 표현(Representation of Resource)
        * Client가 자원의 상태(정보)에 대한 조작을 요청하면 Server는 이에 적절한 응답(Representation)을 보낸다.
        * REST에서 하나의 자원은 **JSON, XML, TEXT, RSS** 등 여러 형태의 Representation으로 나타내어 질 수 있다.          
* REST API
  * REST API의 정의
    * REST 기반으로 서비스 API를 구현한 것
    * 최근 OpenAPI(누구나 사용할 수 있도록 공개된 API: 구글 맵, 공공 데이터 등), 마이크로 서비스(하나의 큰 애플리케이션을 여러 개의 작은 애플리케이션으로 쪼개어 변경과 조합이 가능하도록 만든 아키텍처) 등을 제공하는 업체 대부분은 REST API를 제공한다.
  * REST API의 특징
    * 사내 시스템들도 REST 기반으로 시스템을 분산해 확장성과 재사용성을 높여 유지보수 및 운용을 편리하게 할 수 있다.
    * REST는 HTTP 표준을 기반으로 구현하므로, HTTP를 지원하는 프로그램 언어로 클라이언트, 서버를 구현할 수 있다.
    * 즉, REST API를 제작하면 델파이 클라이언트 뿐 아니라, 자바, C#, 웹 등을 이용해 클라이언트를 제작할 수 있다.
  * REST API 설계 **기본 규칙**
    1. URI는 정보의 자원을 표현해야 한다.
        * resource는 동사보다는 명사를 사용한다.
        * resource는 영어 소문자 복수형을 사용하여 표현한다.
        * Ex) `GET /Member/1` -> `GET /members/1`
    2. 자원에 대한 행위는 HTTP Method(GET, PUT, POST, DELETE 등)로 표현한다.
        * URI에 HTTP Method가 들어가면 안된다.
        * Ex) `GET /members/delete/1` -> `DELETE /members/1`
        * URI에 행위에 대한 동사 표현이 들어가면 안된다.
        * Ex) `GET /members/show/1` -> `GET /members/1`
        * Ex) `GET /members/insert/2` -> `POST /members/2`

### 소켓이란

* TCP/IP를 이용하는 API로 소프트웨어로 작성된 통신의 접속점이다.