---
layout: post
title: Public Key Cipher
description: |
  Public Key Cipher(공개키 암호화)에 대한 글입니다.
categories: 컴퓨터보안(Security)
sitemap: false
hide_last_modified: true
---
# Public Key Cipher

## 현대암호의 분류

![200x50](/assets/img/blog/classification_of_modern_cryptography.drawio.png "현대암호의 분류")

## Symmetric vs Public key

- Encryption key와 Decryption key 동일여부
- 같으면 symmetric, 다르면 public key

## Why no Symmetric key?

- Symmetric은 빠르고 안전하다.
- 근데 왜?
- requires sender, receiver know shared secret key
- how to agree/share upon a common secret key on **<span style="color:red">Internet!</span>**

## Public Key Cipher

- senderm receiver do not share common key
- user has 2 keys(private, public)
  - public key known to all
  - private key known only to receiver
- public key로 잠그면 private key로 열고, private key로 잠그면 public key로 열린다
- Internet 환경에서 대표적으로 사용
> RSA, ECC, ElGamal