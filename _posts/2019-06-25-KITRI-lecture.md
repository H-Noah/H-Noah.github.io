---
title: "[교육]IOT 클라우드 서비스 구축 및 API 개발과정(1)"
permalink: docs/KITRI-IOT-lecture(I)
last_modified_at: 2019-06-25T17:58:49-04:00
excerpt: "IOT 클라우드 서비스 구축 및 API 개발과정 내용입니다."
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


## 도입

- 1교시동안은 이론만 주루룩. 
- JEKYLL 설치에 오류가 있었다. (폴더이름에 공백이 있으면 발생하는 오류였음..)

## 사물인터넷기술


### 센서

- 센서가 많이 발달했다.

### 디바이스

- oss.kr에서 오픈소스 라이센스 및 도입가이드/사례 체크


## 아두이노 

아래 보드(아두이노 우노)로 진행했다. 옛 추억이 새록새록

 ![problem](/assets/images/2019-06-25-KITRI-lecture-uno.jpg)

 6개핀은 PWM으로 사용가능하다 (digital 3,5,6,9,10,11)

* PWM: High와 Low의 값을 조절하여 밝기조절, 온도조절 등 아날로그처럼 사용할 때 사용


### IDE 설치하기

[공식사이트](https://www.arduino.cc/) 참조

### blink


아래 센서더미에서 원하는 것을 빼서 사용한다.

![problem](/assets/images/2019-06-25-KITRI-lecture-kit.jpg)

```c
void setup() {
pinMode(13, OUTPUT); //intel edison GPIO 40
}
void loop() {
 digitalWrite(13, HIGH);
 delay(1000);
 digitalWrite(13, LOW);
 delay(1000);
}
```

테스트용으로 LED가 깜빡이도록 해보았습니다.

- setup() : 초기화
- loop() : 원하는 내용 작성

### 아두이노 함수 및 센서


[아두이노 공식사이트](https://www.arduino.cc/reference/ko/) 참조.

- map 함수를 기억하라
- delay 함수를 기억하라

 ![problem](/assets/images/2019-06-25-KITRI-lecture-1.PNG)
 ![problem](/assets/images/2019-06-25-KITRI-lecture-2.PNG)



순서대로 LED, 부저, 버튼 센서를 사용해서 변경해보았다.

![problem](/assets/images/2019-06-25-KITRI-lecture-sensor.jpg)

```c
int buttonState = 0;
void setup() {
 pinMode(13, OUTPUT);
 pinMode(2, INPUT);
}
void loop() {
 buttonState = digitalRead(2);
 if (buttonState == HIGH) {
 digitalWrite(13, HIGH);
 }else {
 digitalWrite(13, LOW);
 }
}
```

위 코드는 버튼 센서를 DIGITAL 2번 핀에 연결하고 13번 핀에 부저 센서를 연결하여
2번 핀에 HIGH(버튼을 누르면)신호가 들어올 경우 13번 핀에 digital write를 실행하여 부저가 울리도록 작성한 코드이다.

연결을 위해 장착한 extension kit
![problem](/assets/images/2019-06-25-KITRI-lecture-uno-extension.jpg)


조도는 Analog LED는 PWM을 이용하여 조도가 변하면 불이 켜지는 코드

```c
int flame=A0; 
int Buzzer=8; 
int val=0; 


void setup() 
{ 
  pinMode(Buzzer,OUTPUT);  //Set LED as output 
  pinMode(flame,INPUT);  //Set buzzer as input 
  Serial.begin(9600);  //Set baud rate as 9600 
} 

void loop() 
{ 
  val=analogRead(flame);  //Read the analog value 
  Serial.println(val);  //Output analog value and print it out 
  if(val<10) // When analog value 〉600，buzzer make sound 
  { 
    digitalWrite(Buzzer,HIGH); 
  } 
  else 
  { 
    digitalWrite(Buzzer,LOW); 
  } 
}
```

조도센서값이 10 이하로 떨어지면 불이 켜지게 제작하였다. 아래는 조도값이 들어오는 화면이다.

![problem](/assets/images/2019-06-25-KITRI-lecture-3.PNG)


### 아두이노 통신

RX, TX를 이용하여 직렬통신 수/송신을 진행한다.


### 결과물

- 조도센서, LED, 버튼, 부저

부저는 멜로디가 나오도록

1. 버튼을 누르면 모든 상황을 종료한다.
2. 조도센서값이 내려가면 LED가 점점켜진다.
3. 온도가 올라가면 부저가 켜진다
4. Flame 센서값이 올라가면 부저와 LED가 켜진다.

( 6개핀은 PWM으로 사용가능하다 (digital 3,5,6,9,10,11) )

> 온도가 올라가면 부저가 켜진다.

먼저, 온도센서의 값을 받아보자.

온도센서의 값은 아날로그 2번 핀에서 받아보겠다.
스피커의 값은 디지털 9번 핀에서 받아보겠다.

어쨌든 귀찮아서 아래와 같이 코드를 작성했다. Flame 센서는 제외했으며 버튼을 누른 동안에는 아무것도 실행되지 않게 작성했다. 조도가 낮아지는만큼 LED가 깜빡이게 구현해보아야겠다.

```c
#define  c     3830    // 261 Hz 
#define  d     3400    // 294 Hz 
#define  e     3038    // 329 Hz 
#define  f     2864    // 349 Hz 
#define  g     2550    // 392 Hz 
#define  a     2272    // 440 Hz 
#define  b     2028    // 493 Hz 
#define  C     1912    // 523 Hz 
// Define a special note, 'R', to represent a rest
#define  R     0

int melody[] = {  C,  b,  g,  C,  b,   e,  R,  C,  c,  g, a, C };
int beats[]  = { 16, 16, 16,  8,  8,  16, 32, 16, 16, 16, 8, 8 }; 
int MAX_COUNT = sizeof(melody) / 2; // Melody length, for looping.

long tempo = 10000;
int pause = 1000;
int rest_count = 100; //<-BLETCHEROUS HACK; See NOTES


int luxval=0;  //조도값
int tone_ = 0;
int beat = 0;
long duration  = 0;


int ledpin=13; //13번 핀에서 LED 출력
int buttonPin = 11; //11번 핀에 버튼 입력
int speakerOut = 9; //9번 핀에서 스피커를 출력할 것이다.
int luxpin= 0;  //0번 핀에서 조도센서 값을 받는다.
int potPin = 2; //2번 핀에서 온도센서 값을 받는다.

int buttonState;


void setup() 
{ 
  pinMode(speakerOut, OUTPUT);
  pinMode(ledpin,OUTPUT);
  pinMode(luxpin,INPUT);  
  pinMode(buttonPin, INPUT);

  Serial.begin(9600);//Set baud rate as 9600 

} 

void playTone() {
  if (tone_ > 0) {
      digitalWrite(speakerOut,HIGH);
      delayMicroseconds(tone_ / 2);
  }                              
}

void loop() 
{ 
  buttonState = digitalRead(11);
  Serial.print(" Button is ");
  Serial.print(buttonState);//output dat value 

  //버튼이 눌러진 상태에서만 LOOP가 동작한다.
  
  if(buttonState == LOW){
    //시끄러우니까 천천히하자
    /////////////////////////////////////////온도 감지 및 출력 시작/////////////////////////////////////////
    int temperature;
    int dat;//define variable 
    
    temperature=analogRead(2);// read the analog value and assign to val 
    dat=(125*temperature)>>8;//temperature calculation formula 
    
    Serial.print(" Tep:");
    Serial.print(dat);//output dat value 
    Serial.println("C");//output character string C 
    
    tone_ = melody[dat-20];
    beat = beats[dat-20];
    playTone();   
    delay(500);//delay 0.5 s   
  
    
    //조도 변화에 따라 LED가 변하도록 소스변경 
    /////////////////////////////////////////조도 감지 및 출력 시작/////////////////////////////////////////
  
    luxval=analogRead(luxpin);//read analog   
    Serial.print("luxval is ");
    Serial.print(luxval);
    delay(10);//delay 0.01 s 
    //조도가 100 이하면 LED가 켜진다.
    if(luxval<=100){
        digitalWrite(ledpin,HIGH); 
    }   
    else
    {
      digitalWrite(ledpin,LOW); 
    }

  }
  else{
    Serial.print("AFTER Button is HIGH ");    
    delay(1000);//delay 0.5 s   

  }
}
```