---
layout: post
title: Symmetric Key Cipher [대칭키 암호화]
description: |
  Symmetric Key Cipher(대칭키 암호화)에 대한 글입니다.
categories: 컴퓨터보안(Security)
sitemap: false
hide_last_modified: true
---

## Symmetric Key Cipher

### 현대암호의 분류

![100x50](/assets/img/blog/classification_of_modern_cryptography.drawio.png "현대암호의 분류")

### Symmetric vs Public Key

- Encryption Key와 Decryption Key 동일여부
- 같으면 Symmetric, 다르면 Public Key

> shift, affine, substitution, vigenere cipher는 모두 <span style="color:green">**symmetric**</span>

### Block vs Stream Cipher
- Block
  - 긴 평문을 일정한 길이의 블록으로 나누어 블록단위 암호화하는 방식
  > DES, AES 등
- Stream
  - Bit 혹은 Byte 단위로 암호화
  - 키를 키스트림 생성기라는 알고리즘에 입력하여 발생되는 1비트 키의 무한수열로 평문을 암호화
  > eStream, RC4 등

<center>
파일 다운로드 &rarr; Block (데이터가 정해져 있으므로)<br>
vs<br>
실시간 방송, 카카오 채팅 &rarr; Stream (언제 데이터가 전송될지 모르므로)
</center>

### Block Cipher
- 긴 평문을 일정한 길이의 블록으로 나누어 블록단위로 암호화하는 방식
- SW 구현이 쉽다
- Round를 사용하여 반복적으로 암호화하므로 안전
- 대부분 Fiestel cipher structure에 기반
> DES, AES, SEED, ARIA, Bluefish, Serpent 등

### Fiestel Cipher Structure란

- 대부분 Block cipher에 사용
- 입력 block을 반으로 나눈다
- 왼, 오른쪽 바꿔가며 여러 round 수행

![100x200](/assets/img/blog/300px-Feistel_cipher_diagram_en.svg.png "FiestelCipherStructure")

#### Fiestel Cipher parameters
- Block Size
- Key Size
- Round 회수<br>
**&rarr; 모든 파라미터는 크면 안전해지나 느려짐**

### Block Operation Mode

- Idea: Block들을 어떻게 운용하느냐로 안정성 향상
- 4가지 Mode
  - ECB(Electronic Code Block)
  - CBC(Cipher Block Chaining)
  - CFB(Cipher Feedback)
  - OFB(Output Feedback)

#### ECB(Electronic Code Block)

- 각 block이 서로 독립적
- 장점
  - simple
  - 병렬처리용이
- 단점
  - 같은 평문에 대해 동일한 암호문 생성

![200x100](/assets/img/blog/electronic-code-book-1.png "ECB")

#### CBC(Cipher Block Chaining)

- chain: 뒤에 것을 앞에 연결
- 최초의 평문 block은 IV(Initialize Vector)와 XOR
- 결과는 다음 평문 block과 XOR 해서 암호화한다
- 장점
  - 같은 평문 block이라도 다른 암호문 block 생성
- 단점
  - Error propagation: 에러 발생 지점부터 암호화 재실행
> Ipsec, Kerberos5 등에서 사용

![200x100](/assets/img/blog/Cipher-Block-Chaining-1.png "CBC")

#### CFB(Cipher Feedback)

- Feedback: 출력을 입력으로
- 초기 block을 암호화하여 결과를 평문 block과 XOR
- 결과는 다음 encrypt시에 입력으로 사용
- 평문을 적집 암호화하는것이 아니다!
- 장점
  - 같은 plaintext block이라도 다른 cipher block 생성
- 단점
  - Error propagation

![200x100](/assets/img/blog/cipher-feedback-mode-1.png "CFB")

#### OFB(Output Feedback)

- CFB와 차이: 평문 block과 XOR연산 이전의 값을 다음 블록 암호화 과정의 입력으로 사용
- 장단점은 CFB와 동일
- CFB에 비해 빠름

![200x100](/assets/img/blog/output-feedback-mode.png "OFB")

### 스트림 암호

- Stream: 시내, 냇가, 흐름
- Block을 만들 수 없는 경우 사용
- 평문을 1 bit (or byte, word)씩 순차적으로 암호화하는 방식
- 평문과 난수 키 스트림을 1bit씩 단순 XOR
- 빠름(XOR 연산)
- 일반적으로 block cipher에 비해 보안성 낮다

> 무선통신, 실시간 음성, 영상 스트림 서비스

> RC4, ChCha, A5/1, SEAL, SOBER 등