---
layout: post
title: 아날로그
description: |
  아두이노(Arduino)를 통한 아날로그 디지털 신호에 대한 글입니다.

sitemap: false
hide_last_modified: true
---

# 아날로그와 디지털 신호 비교

- 디지털 신호
  - 0과 1의 <span style="color:red">이산적</span>인 값으로 표현
  - 아두이노에서 처리할 수 있는 신호

- 아날로그 신호
  - 주변환경에서 얻을 수 있는 값
  - 무수히 많은 <span style="color:red">연속적</span>인 값으로 표현
  - 아두이노에서 처리할 수 없는 신호
    - ADC를 통해 디지털 신호로 변환해야 함

- **아날로그 디지털 변환기(ADC, Analog Digital Converter)**
  - 정해진 범위의 아날로그 값을 정해진 해상도로 디지털 값으로 변환

- **아두이노 우노의 ADC**
  - 10비트 해상도
  - 0~5V 범위의 아날로그 값을 0~1023의 디지털 값으로 변환
    - 기준 전압: 5V &rarr; 1023, 0V &rarr; 0, 2.5V &rarr; 512

## 아두이노로 아날로그 센서 읽기: analogRead()

### 가변저항 읽기

- 가변저항(potentiometer 또는 pot)
  - 손잡이를 돌리면 저항값이 변하는 전자부품
  - 오디오, 스피커, 온도 조절기, 자동차 등에 흔히 사용
  - 3개 핀으로 구성
    - 바깥쪽 2개 핀: VCC와 GND에 연결
    - 가운데 핀: 가변저항의 저항값을 읽는 핀

~~~cpp
// 가변저항 읽기 프로그램
const int POT = 0;    // 아날로그 0번 핀에 가변저항 연결
int val = 0;    // 가변저항 값을 읽어 저장하기 위한 변수

void setup() {
  Serial.begin(9600);   // 통신 속도(보율, 9600)을 지정하여 컴퓨터와의 시리얼 통신 초기화
}

void loop() {
  val = analogRead(POT);    // 아날로그 입력 핀으로 가변저항 전압을 ADC를 거쳐 읽기
  Serial.println(val);    // 시리얼 통신으로 컴퓨터로 가변저항 값 출력
  delay(500);
}
~~~

- **센서**
  - 주변환경의 물리량을 감지하는 장치
- **센서의 예**
  - 가속도 센서 : 움직임과 기울어짐 감지 (예: 스마트폰 게임 컨트롤)
  - 자력 센서: 자기장 감지(예: 스마트폰의 나침반)
  - 적외선 센서: 물체와 센서 사이의 거리 감지
  - 온도 센서: 주변 온도 감지

## 온도 경보 시스템

~~~cpp
void loop() {
  int val = analogRead(TEMP);
  if(val < LOWER_BOUND) {   // LED를 파란색으로 켬
    digitalWrite(RLED, HIGH);
    digitalWrite(GLED, HIGH);
    digitalWrite(BLED, LOW);
  }
  else if(val > UPPER_BOUND) {    // LED를 빨간색으로 켬
    digitalWrite(RLED, LOW);
    digitalWrite(GLED, HIGH);
    digitalWrite(BLED, HIGH);
  }
  else {    // LED를 초록색으로 켬
    digitalWrite(RLED, HIGH);
    digitalWrite(GLED, LOW);
    digitalWrite(BLED, HIGH);
  }
}
~~~

## 가변저항을 사용하여 아날로그 센서 만들기

### 아날로그 센서

- 물리량 변화에 따라 저항 성질이 바뀌는 재료를 활용하여 센서 제작
- 가변저항과 같은 방식으로 전원을 가하여 저항값을 알아내고 물리량 파악
- 저항 성질이 바뀌는 재료를 사용하는 센서
  - 힘 센서, 구부림 센서: 누르거나 구부릴 때 저항 성질이 변함
  - 포토 레지스터: 빛의 양에 따라 저항 성질이 변함
  - 서비스터(thermistor): 온도에 따라 저항 성질이 변함

- analogRead
  - 물리량 변화에 따른 센서의 저항값을 디지털 값으로 변환하여 읽기
  - 0~1023 사이 값

- analogWrite
  - PWM 신호를 이용하여 LED 밝기 제어
  - 0~255 사이 값

- map
  - output = map(value, fromLow, fromHigh, toLow, toHigh)
  - 입력값(value)의 범위(fromLow~fromHigh)를 다른 범위(toLow~toHigh)로 선형 사상하여 출력
  - toLow가 toHigh보다 작을 필요는 없음

- constrain
  - output = constrain(value, min, max)
  - 입력값(value)이 최소 min 값, 최대 max 값을 가지도록 제한하여 출력

## 자동 조명등 스케치

~~~cpp
// 자동 조명등
const int WLED = 9;   // 백색 LED 양극을 9번 핀에 연결(PWM 출력 핀)
const int LIGHT = 0;    // 조도 센서를 A0 핀에 연결
const int MIN_LIGHT = 200;    // 최소 조도 값
const int MAX_LIGHT = 900;    // 최대 조도 값
int val = 0;    // 아날로그 입력 값을 저장하는 변수

void setup() {
  pinMode(WLED, OUTPUT);    // 백색 LED 연결 핀을 출력으로 설정
}

void loop() {
  val = analogRead(LIGHT);    // 조도 센서 읽기
  val = constrain(val, 0, 255);   // 밝기 범위 제한
  val = map(val, MIN_LIGHT, MAX_LIGHT, 0, 255);   // 조도 -> 밝기 선셩 사상
  analogWrite(WLED, val);   // LED 밝기 제어
}
~~~