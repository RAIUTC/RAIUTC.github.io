---
layout: post
title: Public Key Cipher(공개키 암호화)
description: |
  Public Key Cipher(공개키 암호화)의 개념, 사용 사례, 그리고 주요한 특징들을 살펴보겠습니다.
categories: 컴퓨터보안(Security)
sitemap: false
hide_last_modified: true
---
## Public Key Cipher(공개키 암호화)

![400x200](/assets/img/blog/public-key.gif "OTP(ONE-TIME-PAD)")

### Why no Symmetric Key?
- **Symmetric(대칭키)**은 빠르고, 안전하다.
- 그렇지만 송신자, 수신자 모두 공유된 비밀 키를 필요한다.
> requires sender, receiver know shared secret key.
- 이를 <span style="color:red"> **인터넷** </span>에서 공통 비밀키에 허가/공유할 수 있는가?
> how ro agree/share upon a common key on <span style="color:red"> **Internet!** </span>

### Public Key Cipher
- 송신자, 수신자는 공통 키를 공유하지 않는다.
> sender, receiver do not share common key
- 사용자는 2개의 키를 가진다.(private, public)
> user has 2 keys (private, public)
  - public key는 모두에게 알려진다.
  > public key known to all
  - private key는 수신자에게만 알려진다.
  > private key known only to receiver
- Public key로 잠그면 private key로 열고, private key로 잠그면 public key로 열린다.
- Internet환경에서 대표적으로 사용
> RSA, ECC, El Gammal
- 주로 수학적 이론에 바탕 &rarr; 정수론 필요