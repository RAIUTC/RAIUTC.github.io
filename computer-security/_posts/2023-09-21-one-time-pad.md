---
layout: post
title: 일회성 패드(ONE-TIME PAD)
description: |
  OTP(One-Time Pad)의 개념, 동작 원리, 사용 사례, 그리고 주요한 특징들을 살펴보겠습니다.
categories: 컴퓨터보안(Security)
sitemap: false
hide_last_modified: true
---
## 일회성 패드(ONE-TIME-PAD)

![800x400](/assets/img/blog/otp_overview_example.png "OTP(ONE-TIME-PAD)")

### OTP(One-Time Pad)의 개념
- OTP는 평문을 암호화하기 위해 무작위한 키를 사용하는 방식으로 동작한다. 이 키는 평문과 동일한 길이여야 하며, 한 번 사용한 키는 재사용하지 않는다.

### 동작 원리
- OTP에서는 평문과 키를 XOR 연산을 통해 암호화한다. XOR연산은 비트 단위로 작동하며, 같은 비트일 경우 0을 반환하고 다른 비트일 경우 1을 반환한다.

- 평문과 키의 XOR 결과는 암호문을 생성하며, 암호화된 메시지는 무작위한 값처럼 보인다.

### 보안성과 한계
- OTP는 정보 이론적으로 완벽한 기밀성을 제공한다. 암호문만으로는 평문을 예측할 수 없다.

- 그러나 OTP를 사용하려면 키를 안전하게 관리하고 전달해야 한다. 이는 키 관리의 어려움과 비용을 의미한다.

### 사용 사례
- OTP는 극도로 높은 보안이 필요한 상황에서 사용된다.

> 예: 국가 기밀 정보, 국가 통신, 대사관 통신 등

### 주의 사항

OTP의 핵심은 키의 안전한 관리와 한 번 사용한 키의 재사용을 하지 않는 것이다.