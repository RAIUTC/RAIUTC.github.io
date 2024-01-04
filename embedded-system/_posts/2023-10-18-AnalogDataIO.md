---
layout: post
title: 아날로그 데이터 입출력
description: |
  아두이노(Arduino)를 통한 아날로그 데이터 입출력에 대한 글입니다.
categories: 임베디드시스템(EmbeddedSystem)
sitemap: false
hide_last_modified: true
---
# 아날로그 데이터 입출력

## 아날로그 데이터 처리

- 아날로그 데이터 입력
  - ATmega2560 마이크로컨트롤러에는 16채널의 10비트 해상도 아날로그-디지털 변환기(ADC)가 포함되어 있음
  - 각 채널에는 'A0~A15'까지의 상수가 할당
  > - A0는 디지털 54번, A15는 디지털 69번과 동일

## 아날로그 데이터 입출력 함수

~~~cpp
int analogRead(unit8_t pin)
~~~

- **매개변수**
  - pin: 핀 번호
- **반환값**: 0에서 1023 사이의 정수값

~~~cpp
void analogReference(unit8_t type)
~~~

- **매개변수**
  - type: DEFAULT, INTERNAL, INTERNAL1V1, INTERNAL2V56, EXTERNAL 중 한 가지
- **반환값**: 없음

~~~cpp
void analogWrite(unit8_t pin, int value)
~~~

- **매개변수**
  - pin: 핀 번호
  - value: 듀티 사이클(duty cycle). 0(항상 OFF)에서 255(항상 ON)사이의 값
- **반환값**: 없음

|옵션|설명|
|---|---|
|DEFAULT|uC의 동작 전압(5V)으로 설정|
|INTERVAL|내부 기준 전압(1.1V)으로 설정|
|INTERNAL1V1|내부 1.1V로 설정|
|INTERNAL2V56|내부 2.56V로 설정|
|EXTERNAL|AREF 핀에 인가된 0~5V 사이 전압으로 설정|

## 가변저항 값 출력

~~~cpp
int vResistor = A0;   // A0 핀에 가변저항 연결

void setup() {
  Serial.begin(9600);   // 시리얼 통신 초기화
  pinMode(vResistor, INPUT);
}

void loop() {
  Serial.println(analorRead(vResistor));

  delay(1000);
}
~~~

## 가변저항으로 LED 개수 조절

~~~cpp
void loop() {
  int adc = analogRead(vResistor);    // 가변저항 값 읽기
  int count_led = (adc >> 8) + 1;   // LED 개수 설정 * 비트 이동에 의해 10비트 결과값을 2브트의 1~4 사이 값으로 변환

  for(int i = 0; i < 4; i++) {    // LED 점멸
    if(i < count_led) {
      digitalWrite(pins_led[i], HIGH);
    }
    else {
      digitalWrite(pins_led[i], LOW);
    }
  }
}
~~~

## 가변저항으로 밝기 제어

~~~cpp
void loop() {
  int ADC_value = analogRead(A0);   //ADC 값
  int PWM_value = ADC_value >> 2;   //PWM 값

  Serial.print(String("ADC value : ") + ADC_value);
  Serial.println(String(", PWM value : " + PWM_value));

  for(int i = 0; i < 4; i++) {    // LED 밝기 조절
    analogWrite(pins_LED[i], PWM_value);
  }

  delay(1000);
}
~~~

- 4개의 LED를 1024 단계로 밝기가 변하는 하나의 LED처럼 제어

~~~cpp
for(int i = 3; i >= 0; i--) {   // 4개 LED의 밝기로 나눔
  if(ADC_value >= 256 * i) {
    PWM_value[i] = ADC_value - 256 * i;
    ADC_value -= (PWM_value[i] + 1);
  }

  analogWrite(pins_led[i], PWM_value[i]);   // LED 밝기 조절
  Serial.print(" ");
  Serial.print(PWM_value[i]);
}
~~~

## 주기적인 처리를 위한 함수

~~~cpp
void delay(unsigned long ms)
~~~

- **매개변수**
  - ms: 밀리초 단위의 지연 시간
- **반환값:** 없음

~~~cpp
void delayMicroseconds(unsigned int us)
~~~

- **매개변수**
  - us: 마이크로초 단위의 지연 시간
- **반환값**: 없음

~~~cpp
unsigned long millis(void)
~~~

- **매개변수**: 없음
- **반환값**: 프로그램이 시작된 이후의 밀리초(millisecond)단위 경과 시간

## 주기적인 LED 제어 - delay

~~~cpp
void loop() {
  digitalWrite(pin_LED1, LED_state);
  delay(1000);    //1초 대기    *1초 대기 시간 동안 버튼의 눌림 여부를 검사하지 못하므로 2번째 LED가 버튼에 즉각적으로 반응하지 못함
  LED_state = !LED_state1;    // 13번 LED 반전

  if(digitalRead(pin_button)) {   // 버ㅡㄴ이 눌러진 경우
    LED_state2 = ~LED_state2;   // 2번 LED 반점
    digitalWrite(pin_LED2, LED_state2);
  }
}
~~~

## delay 함수 없는 Blink

~~~cpp
void loop() {
  time_current = millis();    // 현재 시간
  count++;    // loop 함수 실행 횟수

  if(time_current - time_previous >= 1000) {
    time_previous = time_current;   // 시작 시간 갱신

    LED_state = !Led_state;   // LED 반전
    digitalWrite(pin_LED, LED_state);

    Serial.println(count);
    count = 0;
  }
}
~~~

## millis 함수로 주기적인 LED 제어 - delay 수정

~~~cpp
void loop() {
  ////////////첫 번째 LED의 blink///////////////
  time_current = millis();
  if(time_current - time_previous >= 1000) {
    time_previous = time_current;   // 시작 시간 갱신

    LED_state1 = !LED_state1;   // LED 반전
    digitalWrite(pin_LED1, LED_state1);
  }
  /////////////////////////////////////////////

  if(digitalRead(pin_button)) {   // 버튼이 눌러진 경우
    LED_state2 = !LED_state2;   // 2번 LED 반전
    digitalWrite(pin_LED2, LED_state2);
    delay(100);
  }
}
~~~

## 버튼을 누르는 순간 감지

- 버튼의 이전과 현재 상태를 저장하여 상태가 바뀌는 순간에만 LED를 반전

~~~cpp
button_state_current = digitalRead(pin_button);
if(button_state_current) {    // 버튼이 눌러진 경우
  if(button_state_previous == false) {
    button_state_previous = true;
    LED_state2 = !LED_state2;   // 2번 LED 반전
    digitalWrite(pin_LED2, LED_state2);
  }
}
else {
  button_state_previous = false;
}
~~~

## 가변저항으로 블링크 속도 제어

~~~cpp
void loop() {
  time_current = millis();

  if(time_current - time_previous >= interval) {
    Serial.print("Current interval is ");
    Serial.print(interval);
    Serial.println("ms.");

    time_previous = time_current;   //시작 시간 갱신

    LED_state = !LED_state;   // LED 반전
    digitalWrite(pin_LED, LED_state);
  }

  ////////////////0.5 ~ 1.5초 사이의 시간으로 매핑////////////////
  int adc = analogRead(A0);
  interval = map(adc, 0, 1023, 500, 1500);
  //////////////////////////////////////////////////////////
}
~~~