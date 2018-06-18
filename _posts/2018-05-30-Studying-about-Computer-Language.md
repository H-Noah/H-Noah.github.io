---
title: "학습자료"
permalink: /docs/Studying-about-Computer-Language/
last_modified_at: 2018-05-30T15:58:49-04:00
toc: true
classes: wide
author_profile: false
sidebar:
  title: "Order List"
  nav: sidebar-sample
---



---
> PHP 학습 정보
---  

```php
strlen( string A )  return LENGTH // 길이  
str_word_count( string A ) return COUNT_NUM // 단어 개수  
strrev( string A ) return GNIRTS // 역순 출력  
strpos( string A, string WordforSearch ) return POSITION or FALSE // 단어 검색 (첫 글자 = 0 출력)  
str_replace( string Original, string Replace, string A) return STRING // 단어 치환  

array() = //어레이 생성 함수  
Associative array //(결합형 배열) - ex) $age = array(“peter”=>“35”, “Ben”=>“37);  

sort( $array ) return 0;  //- sorting 함수, rsort()는 역소팅  
asort //결합형 배열에서 value를 따라 ascending ordering  
ksort //결합형 배열에서 Key를 따라 ascending ordering  

SERVER[“PHP_SELF”]) = //동작중인 스크립트의 파일이름을 리턴한다.  
htmlspecialchars() = //코드를 injecting하거나 exploiting하는 공격자로부터 방어하기 위한 변환 함수  
자바스크립트 안에 <script>가 추가되는 것을 주의하라.  

fgets() //- read a single line from a file.   
feof() //- checks if the “end-of-file” has been reached  
fgetc() //- read a single char froma a file.  
```  

```PHP
$_SERVER, $_REQUEST, $_POST // 등의 수퍼글로벌 변수들은 미리 정의되어 있다. 언제든 사용가능  
```  

함수 밖이나 다른 곳에서 선언된 함수를 전역으로 사용하고 싶으면 $GLOBALS[‘ ’]형태로 호출한다.{: .small}



-  PHP Form Validation(유효성 검증)

```PHP
<form method="post" action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]);?>">
```    

- php include VS require

{: .small}
 include: 삽입한 php가 없거나 문제가 있을 경우 동작을 계속한다. 파일이 없어도 진행돼야 할 때 사용  
 require: 삽입한 php가 없거나 문제가 있을 경우 동작을 멈춘다.  
