---
layout: post
title: Intro
description: |
  
categories: 블록체인
sitemap: false
hide_last_modified: true
---

# 블록체인 기술

## 블록체인 기술의 구성요소

<p align="center">
<img src="/assets/img/blog/components_of_blockchain_technology.png">
</p>

## 블록체인 기술의 구성요소 - P2P 연결과 P2P 네트워크

- 블록체인은 P2P 분산 네트워크상의 분산시스템임. P2P란 Peer to Peer의 약자로, 네트워크에 연결된 컴퓨터가 서버와 클라이언트의 기능을 동시에 수행하는 컴퓨터 네트워크를 의미함.
- P2P는 네트워크로 연결된 컴퓨터의 다양한 자원을 공유할 수 있고 이용자들의 협업적 활동을 지원함으로써 새로운 가치를 만들어낼 수 있음.

<p align="center">
<img src="/assets/img/blog/peer_to_peer_connection_and_network.png">
</p>

## 블록체인 기술의 구성요소 - P2P 네트워크

- 네트워크에 참여하는 각 노드가 중앙 서버 없이 직접 데이터를 주고 받는 방식
- 각 노드가 서버와 클라이언트 역할을 동시에 수행
- 블록체인 네트워크는 참여하는 모든 노드가 같은 데이터를 유지함.

<p align="center">
<img src="/assets/img/blog/peer_to_peer_network.png">
</p>

## 블록체인 기술의 구성요소 - P2P 네트워크 - P2P 분산 네트워크의 안정성과 신뢰성

- P2P 방식을 선택하는 가장 큰 이유는 사고 등으로 전체 시스템이 멈출 위험이 매우 낮기 때문임.
- 이는 장기간 안정적으로 네트워크를 운영하는데 적합하고 우연히 어느 노드가 고장이 나더라도 전체 시스템 동작에 거의 영향을 주지 않음.
- P2P에서 노드 각각을 연결하는 통신 경로는 그물망처럼 여러 개여서 어느 한 곳의 통신 경로가 끊어지더라도 시스템 전체 기능에 영향이 거의 없음.
- 물론, 여러 개의 노드가 동시에 고장이 나거나 여러 통신 경로가 동시에 끊어지는 일이 발생할 수도 있으므로, 노드수가 너무 적은 P2P 분산 시스템은 위험성이 다소 높아질 수 있음.

<p align="center">
<img src="/assets/img/blog/stability_and_reliability_of_p2p_distributed_network.png">
</p>

## 블록체인 기술의 구성요소 - P2P 네트워크 - 노드

<p align="center">
<img src="/assets/img/blog/node.png">
</p>

- Full Nodes
    - Keep and distribute copies of the entire blockchain ledger and thus guarantee the security and correctness of the data on the blockchain by validating data.
    > 전체 블록체인 장부의 사본을 유지하고 배포하여 데이터의 보안과 정확성을 보장하고, 데이터를 유효성 검사하여야 합니다.
    - Make decisions for the future of the network.
    > - 네트워크의 미래에 대한 결정을 내린다.
    - Validate blocks, transactions, business logic and smart contracts.
    > 블록, 거래, 비즈니스 로직, 스마트 계약을 유효성을 검사합니다.

- Light Nodes
    - Keep only a portion of the blockchain by downloading only the block header of previous transactions to confirm the validity of the blockchain.
    > 이전 거래의 블록 헤더만 다운로드하여 블록체인의 유효성을 확인하고 블록체인의 일부만을 유지한다.
    - Validate basic elements of the blocks, i.e., hashes, signatures, etc.
    > 블록의 기본 요소, 즉 해시, 서명 등을 유효성 검사하다.

- Validating Nodes
    - Produce the blocks for the blockchain.
    > 블록체인을 위한 블록을 공급한다.
    - Confirm the blocks that should be put into the list.
    > 리스트에 들어가야 하는 블록을 확인하다.