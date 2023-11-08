---
layout: post
title: 대칭키 암호(Symmetric Key Cipher)
description: |
  대칭키 암호(Symmetric Key Cipher)는 현대 정보 보안에서 핵심적인 역할을 하는 암호화 기술 중 하나입니다. 
  이 기술은 데이터의 기밀성을 유지하고 무단 액세스로부터 보호하기 위해 많이 사용됩니다. 
  이 글에서는 대칭키 암호화의 작동 원리와 중요성에 대해 알아보겠습니다.
categories: 컴퓨터보안(Security)
sitemap: false
hide_last_modified: true
---
## Symmetric Key Cipher[대칭키 암호]

## 현대암호의 분류
![800x400](/assets/img/blog/modern-cipher-classification.png "현대암호의 분류")

### Symmetric key VS Public key
Symmetric key와 Public key의 차이점은 Encryption(암호화) key와 Decryption(복호화) key의 동일여부이다.

Symmetric key는 암호화 키와 복호화 키가 같고 Public key는 다르다.

### Block VS Stream cypher

- **Block**: 긴 평문(plaintext)을 일정한 길이의 블록으로 나누어 블록단위 암호화하는 방식이다.
>예: DES, AES 등
- **Stream**: Bit 혹은 byte 단위로 암호화 하는 방식. 키를 키스트림 생성기라는 알고리즘에 입력하여 발생되는 1비트 키의 무한수열로 평문을 암호화한다.
>예: eStream, RC4등

암호화할 데이터 type을 고려해 Block과 Stream cypher중 결정하면 된다. Block cypher는 미리 보내야할 데이터가 정해져 있는 파일 다운로드에 사용해야 하고 Stream cypher는 실시간으로 서비스 해야하는 실시간 방송, 카카오 채팅에 사용한다.

#### Block Cipher
- 긴 평문을 일정한 길이의 블록으로 나누어 블록단위로 암호화하는 방식
- SW구현이 쉽다.
- Round를 사용하여 반복적으로 암호화하므로 안전하다.
- 대부분 Feistel cipher structure에 기반한다.
> DES, AES, SEED, ARIA, Bluefish, Serpent 등이 있다.

#### Feistel Cipher Structure란
![400x600](/assets/img/blog/feistel-cipher-structure.png "Feistel Cipher Structure")

**Feistel Cipher Structure**는 대부분 Block cipher에 사용한다. 입력 block을 반으로 나누고 왼, 오른쪽을 바꿔가며 여러 round를 수행한다.

### 암호화 방식의 스펙 확인법
![800x200](/assets/img/blog/feistel-cipher-spac.png "Feistel Cipher Parameters")

- Block size: 크면 안전해지나 느려짐
- Key size: 크면 안전해지나 느려짐
- Round 회수: 크면 안전해지나 느려짐 

### DES(Data Encryption Standard)
- Feistel cipher structure
- Block size: 64bit
- Key size: 56bit
- Round: 16 round

~~~python
# DES
!pip uninstall pycrypto
!pip install pycryptodome

from Crypto.Cipher import DES

# byte 객체로 바이트 객체 생성
key = b'12345678' # 8bytes
iv = b'12345678'

# key: DES에서 대칭할 키, MODE_CFB는 사용할 모드를 지정, iv: 입력 데이터와 조합되어 초기 상태를 설정하는데 사용
cipher1 = DES.new(key, DES.MODE_CFB, iv)

msg = input("plaintext : ")
plaintext = bytes(msg, 'utf-8')
ciphertext = cipher1.encrypt(plaintext)
print('ciphertext : ', ciphertext)

cipher2 = DES.new(key, DES.MODE_CFB, iv)
print("decrypting... ", cipher2.decrypt(ciphertext))
~~~

#### DES의 변형
- 2DES: 2개 key 사용
![400x200](/assets/img/blog/2des.png "2DES")

- 3DES: 2~3개 key로 3회 암복호화
![400x200](/assets/img/blog/3des.png "2DES")

#### 3DES
~~~python
# 3DES
from Crypto.Cipher import DES3

# DES는 8bytes 객체
key = b'1234567890abcdef'
iv = b'12345678'

# 보안 전문가가 할 일은 MODE를 정확히 지정해 주는 것이다.
cipher1 = DES3.new(key, DES3.MODE_OFB, iv)

msg = input("plaintext : ")
plaintext = bytes(msg, 'utf-8')
ciphertext = cipher1.encrypt(plaintext)
print('ciphertext : ', ciphertext)

cipher2 = DES3.new(key, DES3.MODE_OFB, iv)
print("decrypting... ", cipher2.decrypt(ciphertext))
~~~

### AES(Advanced Encryption Standard)
- Block size: 128bit
- Key size: 128, 192, 256bit
- Round: 각 키 크기에 따라 10, 12, 14 rounds

~~~python
# AES
from Crypto.Cipher import AES

key = b'1234567890abcdef' # 16 bytes
cipher1 = AES.new(key, AES.MODE_EAX)

nonce = cipher1.nonce

msg = input("plaintext : ")
plaintext = bytes(msg, 'utf-8')
ciphertext = cipher1.encrypt(plaintext)
print('ciphertext : ', ciphertext)

cipher2 = AES.new(key, AES.MODE_EAX, cipher1.nonce)
print("decrypting... ", cipher2.decrypt(ciphertext))
~~~

### 4가지 Block Operation Mode

- **ECB(Electronic Code Block)**
![400x200](/assets/img/blog/ecb.png "ECB(Electronic Code Block)")

각 블록이 서로 독립적이다.
> 장점: Simple, 병렬처리용이

> 단점: 같은 평문에 대해 동일한 암호문 생성

- **CBC(Cipher Block Chaining)**
![400x200](/assets/img/blog/CBC.png "Cipher Block Chaining")

Chain: 뒤에 것을 앞에 연결

최초의 편문 block은 IV와 XOR한다. 결과는 다음 평문 block과 XOR해서 암호화한다.
> 장점: 같은 평문 block이라도 다른 암호문 block 생성

> 단점: Error propagation(오류 전파)

- **CFB(Cipher Feedback)**
![400x200](/assets/img/blog/cfb.png "ECB(Electronic Code Block)")

FeedBack: 출력을 입력으로

초기 block을 암호화하여 결과를 평문 block과 XOR한다. 결과는 다음 encrypt시에 입력으로 사용된다. 평문을 직접 암호화하는것이 아니다!
> 장점: 같은 plaintext block이라도 다른 cipher block 생성

> 단점: Error propagation(오류 전파)

- **OFB(Output Feeedback)**
![400x200](/assets/img/blog/ofb.png "OFB(Output FeedBack)")

장단점은 CFB와 동일하다. CFB에 비해 빠르다.

### Stream Cipher(스트림 암호)

- Stream: 시내, 냇가, 흐름

Block을 만들 수 없는 경우 사용한다. 평문을 1 bit (or byte, word)씩 순차적으로 암호화하는 방식이다. 평문과 난수 키 스트림을 1 bit씩 단순 XOR한다.
> 빠르다(XOR 연산)

> 일반적으로 block cipher에 비해 보안성이 낮다.

> 사용 예: 무선통신, 실시간 음성, 영상 스트림 서비스