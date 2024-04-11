---
layout: post
title: 비트코인과 암호화폐 (2)
description: |
  
categories: 블록체인
sitemap: false
hide_last_modified: true
---

# 비트코인과 암호화폐 (2)

## 비트코인 UTXO - 트랜잭션 데이터 구조

- 트랜잭션 데이터는 크게 입력부와 출력부로 구분.
- 입력부에는 송금자의 UTXO 포인터, 전자서명, 공개키가 기록됨. 공개키는 다른 사람들이 전자서명을 검증할 때 사용.
- 출력부에는 송금할 금액과 수금자의 공개키 해시가 기록.
- 'UTXO라는 화폐 방식'으로 '비대칭키를 이용하여 송금'하는 과정을 '입력(Input)과 출력(Output)구조'로 정형화한 구현체가 바로 비트코인 트랜잭션.

<p align="center">
<img src="/assets/img/blog/bitcoin_utxo.png">
</p>

## 비대칭키와 UTXO 개념을 이용한 송금방식

<p align="center">
<img src="/assets/img/blog/bitcoin_utxo_transaction.png">
</p>

## 비트코인 트랜잭션 전자서명 생성 및 검증

<p align="center">
<img src="/assets/img/blog/bitcoin_transaction_sign.png">
</p>

## 지갑(Wallet) 유형

<p align="center">
<img src="/assets/img/blog/bitcoin_wallet_2.png">
</p>

## Massive Market Potential of Bitcoin Smart Contracts

<p align="center">
<img src="/assets/img/blog/bitcoin_smart_contract.png">
</p>

## 비트코인 에코시스템

<p align="center">
<img src="/assets/img/blog/bitcoin_ecosystem.png">
</p>