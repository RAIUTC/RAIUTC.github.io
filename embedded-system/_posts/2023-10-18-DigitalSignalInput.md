---
layout: post
title: 디지털 신호 입력
description: |
  아두이노(Arduino)를 통한 디지털 신호 입력에 대한 글입니다.
categories: 임베디드시스템(EmbeddedSystem)
sitemap: false
hide_last_modified: true
---
# 디지털 신호 입력

## 스위치 입력

- 스위치를 이용하여 디지털 신호를 입력 받아 스위치가 눌러졌을 때 LED를 점등

~~~cpp
int inputPin = 2;
int ledPin = 13;

void setup() {
  Serial.begin(9600);
  pinMode(swInput, INPUT_PULLUP);
  pinMode(ledPin, OUTPUT);
}

void loop() {
  if(difitalRead(inputPin) == LOW) {
    digitalWrite(ledPin, HIGH);
  }else {
    digitalWrite(ledPin, LOW);
  }
}
~~~

### 응용문제

- 스위치 입력이 감지될 때 마다 LED가 점등되어있다면 소등시키고, 소등되어 있다면 점등

~~~cpp
void loop() {
  int swInput = digitalRead(inputPin);    // 스위치 입력을 받는다
  int ledOutput = digitalREad(ledPin);    // LED의 출력 상태를 확인한다

  if(swInput == LOW) {
    if(ledOutput) digitalWrite(ledPin, LOW);    // LED가 점등되어 있으면 소등
    else digitalWrite(ledPinm HIGH);    // LED가 소등되어 있으면 점등
  }
}
~~~

## 안정적인 스위치 입력

- 스위치를 이용하여 디지털 신호 입력을 받아 LED를 점멸
- 스위치가 입력된 횟수를 시리얼 통신으로 전송

~~~cpp
int inputPin = 2;
int ledPin = 13;

void setup() {
  Serial.begin(9600);
  pinMode(inputPin, INPUT_PULLUP);
  pinMode(ledPin, OUTPUT);
  int count = 0;
}

void loop() {
  swInput = digitalRead(inputPin);
  if(swInput == LOW) {
    delay(100);
    digitalWrite(ledPin, HIGH);
    ++count;
    Serial.println(count);
  }
}
~~~

### 응용문제

- 스위치를 누르고 있는 동안에는 'if(swInput == LOW){}'내의 명령어는 수없이 반복된다. 실제 디지털 입력을 받을 때에는 단 한번의 명령만 실행되어야 한다. 이를 위해서 이 예제의 스위치가 눌러졌을 때 처리되는 부분 수정

~~~cpp
// 스위치가 눌렸을 때
if(swInput == LOW) {
  delay(100);
  if(ledOutput) digitalWrite(ledPin, LOW);    // LED가 점등되어 있으면 소등
  else digitalWrite(ledPin, HIGH);    // LED가 소등되어 있으면 점등
  ++couunt;

  // 스위치 입력 횟수를 시리얼 통신으로 전송
  Serial.println(count);
}
~~~