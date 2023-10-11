---
layout: post
title: Introduction to cryptography [암호학 개론]
description: |
  암호학의 전반적인 개론을 다루는 글입니다.

sitemap: false
hide_last_modified: true
---
## Introduction to cryptography

## 암호의 개념도

![300x50](/assets/img/blog/a%20conceptual%20diagram%20of%20a%20password.drawio.png "암호의 개념도")

- <span style="color:blue">평문(plaintext): </span>암호화전 문장
- <span style="color:blue">암호문(ciphertext): </span>암호화된 문장
- <span style="color:green">암호화(encryption): </span>평문을 암호문으로 바꾸는 과정
- <span style="color:green">복호화(decryption): </span>암호문을 평문으로 바꾸는 과정
- 암호 알고리즘: 암호화 알고리즘과 복호화 알고리즘
- <span style="color:red">키(key): </span>암호 알고리즘에 사용되는 정보

![200x50](/assets/img/blog/encryption_process.drawio2.png)

## 현대암호의 분류

![100x50](/assets/img/blog/classification_of_modern_cryptography.drawio.png "현대암호의 분류")

## Symmetric vs Public Key

- Encryption Key와 Decryption Key 동일여부
- 같으면 Symmetric, 다르면 Public Key

## Block vs Stream cypher

- **Block**
  - 긴 평문을 일정한 길이의 블록으로 나누어 블록단위 암호화하는 방식
  > DES, AES 등

- **Stream**
  - Bit 혹은 Byte 단위로 암호화
  - 키를 키스트림 생성기라는 알고리즘에 입력하여 발생되는 1비트 키의 무한수열로 평문을 암호화
  > eStream, RC4 등