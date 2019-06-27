---
title: "[교육]IOT 클라우드 서비스 구축 및 API 개발과정(2)"
permalink: docs/KITRI-IOT-lecture(II)
last_modified_at: 2019-06-26T17:58:49-04:00
excerpt: "IOT 클라우드 서비스 구축 및 API 개발과정 내용입니다."
toc: true
classes: wide
author_profile: false
sidebar:
  title: "Order List"
  nav: sidebar-sample
tags:
  - hareware
  - edison board

---


## 지난 수업 복습

- 아두이노 보드의 스펙 등을 다루었다.


## 에디슨보드

- PWM출력을 위해 4개의 GPIO가 사용된다 (33,35,37,39)
PWM 출력주파수 및 주기는 다음 과 같다. 
 * Target frequency ~= 19.2 MHz * Base_unit value/256 
 * Target PWM duty cycle ~= PWM_on_time_divisor / 256


OTG 파워와 USB를 꼭아야한다. 센서를 여러개 쓰면 전력이 딸릴수도 있음

Notice
 ※ Intel Edison의 경우 저 전력 장치로 평상시 부하전류가 200mA를 넘지 않는다. Wi-Fi장치 또는 외부 확장장치를 사용하는 경우 500mA를 넘는 경우가 발생한다. 즉 일반적으로 디버깅 환경에서는 USB(5V, 500mA)만으로도 전원이 충분이 공급이 가능하나 네트워크 환경 및 추가적인 장치를 구동하기 위해서는 안정적으로 DC 12V어댑터를 연결한다. (DC12V의 경우 DC-DC컨버트를 통해 5V로 변환)

 netlink: 커널과 통신하기위한 소켓 (유용)
 hostapd: ap모드를 활성화시킬 수 있는 오픈소스

 rssi() in wifi.h : 주파수 세기를 체크하는 함수


 ## WIFI 이용 서버구축 

## bluetooth 

bluetoothctl을 통해 접속한 뒤, 아래 명령어들을 사용할 수 있다.

- defalut agent 등록
- pair
- trust
- unblock

동작 후, tmp폴더로 가서 ls-l을 통해 arduino_pipe_out 파일을 확인해야한다. 말그대로 temp역할을 하므로 저게 제대로 안되거나 없으면 동작하지 않을 가능성이 높다.


일단 208page부터

pin파일은 블루투스 핀 변경
현재 py파일만 사용해보았음

암튼 서비스파일 이동해서 블루투스 자동켜지게 한다.

에디슨은 75200 보드레이트가 defalut

결론적으로 블루투스를 통해서 LE가 켜지거나 꺼지면 된다.