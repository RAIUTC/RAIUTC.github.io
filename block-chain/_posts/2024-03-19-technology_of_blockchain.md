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

## 블록체인 기술의 구성요소 - P2P 네트워크 - 인터넷 서비스에서 보장해야 할 세가지 특성

- CAP theorem(CAP 이론)은 분산 시스템이 가질 수 있는 세 가지 특성인 일관성(Consistency), 가용성(Availability), 그리고 분할 내성(Partition Tolerance)을 의미함.
- 비트코인은 전 세계에 18,526개의 노드가 서로 통신하면서 동작함. 블록 생성 후, 모든 노드에 데이터가 반영될 때까지 어느 정도의 시간이 소요됨. 블록체인은 가용성과 분할 내성을 우선적으로 보장.

<p align="center">
<img src="/assets/img/blog/cap_theorem.png">
</p>

## 블록체인 기술의 구성요소 - P2P 네트워크 - 비트코인 노드 분포

<p align="center">
<img src="/assets/img/blog/bitcoin_node_distribution.png">
</p>

## 블록체인 기술의 구성요소 - 합의 알고리즘

- 합의 알고리즘은 블록체인 네트워크에서 다수의 참여자가 통일된 의사결정을 하기 위해 사용하는 알고리즘.
- 가장 일반적인 알고리즘은 작업증명(PoW: Proof of Work) 알고리즘과 지분증명(PoS: Proof of Stake) 알고리즘이며, 최초의 합의 알고리즘은 비트코인의 작업증명 알고리즘.
- 작업증명 알고리즘을 사용하는 블록체인(예: 비트코인)에서 트랜잭션을 정렬하고 블록을 생성하는 것을 마이닝(mining)이라고 함.
- 채굴자는 블록체인 네트워크에 포함된 트랜잭션을 순서대로 정렬하고 대가로 코인을 얻음.

<p align="center">
<img src="/assets/img/blog/consensus_algorithm.png">
</p>

## 블록체인 기술의 구성요소 - 합의 형성 알고리즘 - 작업증명(PoW: Proof of Work)

<p align="center">
<img src="/assets/img/blog/proof_of_work.png">
</p>

## 블록체인 기술의 구성요소 - 합의 알고리즘 - 지분증명(PoS: Proof of Stake)

- 작업 증명은 대량의 컴퓨팅 자원을 운용하여 많은 전력이 필요하므로 친환경적이지 않음.
- 이 문제를 해결하기 위해 고안한 분산 합의 형성 알고리즘이 지분 증명(Proof of Stake)
- PoS 매커니즘에서는 '검증자'(validators)가 블록을 생성하고 네트워크를 유지
- 검증자는 시스템에 일정량의 자신의 코인(이 경우에는 이더리움)을 '스테이킹'(staking)하여 블록을 생성하고 거래를 검증하는 권리를 얻음. 이들은 네트워크에 기여한 '지분'의 양에 비례하여 보상을 받음.

<p align="center">
<img src="/assets/img/blog/proof_of_stake.png">
</p>

- 지분증명은 전체 블록 생성에 관여하는 토큰 중 내가 차지하는 지분만큼의 확률로 새로운 블록을 생성할 권리를 주는 방식으로 정의할 수 있음.
- 블록 생성 확률을 높이기 위해서는 이제 하드웨어 성능을 높이는 것이 아니라 지분량을 늘려야 함.

<p align="center">
<img src="/assets/img/blog/proof_of_stake_2.png">
</p>

## 블록체인 기술의 구성요소 - 합의 형성 알고리즘 - 자본증명(PoS: Proof of Stake) - 이더리움 스테이킹

- 이더리움 2.0으로의 전환과 함께 지분 증명(Proof of Stake, PoS) 메커니즘이 도입되면서, 사용자들은 이더리움을 스테이킹하여 네트워크 보안에 기여하고 보상을 받을 수 있음.

<p align="center">
<img src="/assets/img/blog/ethereum_staking.png">
</p>

- 사용자 입장에서 ETH를 스테이킹 하는 방법은 직접 스테이킹, SaaS 서비스, 스테이킹 풀 프로토콜, 중앙화거래소 서비스로 크게 네 가지.
- 직접 스테이킹은 최소 스테이킹 기준인 32개의 ETH를 모아 컴퓨터를 세팅하고 직접 참여하는 방식. 어려울 수 있지만 중간단계에 수수료와 같은 비용 부담이 없어 수익성은 가장 높음.
- 스테이킹 서비스(Staking-as-a-Service)나 스테이킹 프로토콜은 스테이킹 환경 셋업, ETH 32개 모으기, 그리고 중앙화된 거래소의 서비스 사용이 부담스러울 경우 고려할 수 있는 대안.
- 거래소 스테이킹 서비스를 이용하는 방법은 간편하지만 일정 수수료를 지불해야 하기 때문에 사용자의 수익성도 낮을 수 있음.

<p align="center">
<img src="/assets/img/blog/ethereum_staking_2.png">
</p>

## 블록체인 기술의 구성요소 - 합의 형성 알고리즘 - 위임 지분 증명(Delegated Proof of Stake, DPoS)

- 위임지분증명은 코인 보유자들이 자신들의 작업을 제 3자에게 위임하는 투표 시스템을 통해 운영되는 블록체인 방식으로 대표는 새로운 블록의 생성과 검증 과정에 합의를 도출할 책임이 있음.
- 투표의 영향력은 해당 이용자가 보유한 코인 수에 비례하고 대표는 선출된 노드로서 검증에 참여하며 그 대가로 코인을 받음.
- 선출된 노드가 잘못 행동하거나 효율적으로 작업하지 않는 경우, 즉시 퇴출되고 다른 노드로 대체됨.
- 성능 측면에서 위임 지분 증명 블록체인은 확장성이 뛰어나 작업 증명(PoW) 및 지분 증명(PoS)보다 속도가 빠름.

<p align="center">
<img src="/assets/img/blog/delegated_proof_of_stake.png">
</p>

## 멤풀(mempool)

- 작업증명 방식의 블록체인에서 채굴자(miner)는 우선 자신의 컴퓨터에 임시 블록(candidate block)을 만듦.
- 채굴자는 유저들의 트랜잭션을 멤풀(mempool)이라는 저장공간에 임시로 저장해 놓고 그 중에서 몇 개의 트랜잭션을 선택하여 임시 블록에 포함시킴.
- 이 임시 블록은 아직 네트워크를 통해 다른 블록체인 노드들에게 전파되지 않아 채굴자 자신만 가지고 있는 블록으로, 이후 블록체인에 연결될 수 있는 후보 블록임.
- 채굴자 보상을 받기 위해서는 이 임시 블록을 네트워크에 전파하고, 모든 채굴자들이 그 특정 채굴자가 제안한 임시 블록을 그들의 컴퓨터에 저장해야 함.

<p align="center">
<img src="/assets/img/blog/mempool.png">
</p>

Nodes will pick transactions from their memory pool in order to build blocks to add to the blockchain, but they will not follow a First in First Out strategy, they will pick what they will consider the most convenient transactions for them, basically those that pay the highest fees since they will be the ones to collect them.

>  노드는 블록체인에 추가할 블록을 구성하기 위해 메모리 풀에서 트랜잭션을 선택하지만, FIFO(First-in First-Out) 전략을 따르지 않습니다. 대신, 가장 유리한 트랜잭션을 선택합니다. 즉, 노드는 수수료가 가장 높은 트랜잭션을 선택하게 됩니다. 왜냐하면 노드는 해당 수수료를 받게 되기 때문입니다.

<p align="center">
<img src="/assets/img/blog/mempool_2.png">
</p>

## 블록체인 기술의 구성요소 - 합의 형성 알고리즘 - 합의 형성 알고리즘별 에너지 소비

<p align="center">
<img src="/assets/img/blog/energy_consumption_by_consensus_algorithm.png">
<img src="/assets/img/blog/energy_consumption_by_consensus_algorithm_2.png">
</p>

## 암호화 기술 - 블록체인을 지원하는 암호화 기술

- 암호화 기술은 모든 정보 시스템의 신뢰성을 지원함. 생활 관련 인프라와 교통 시스템, 금융 결제 시스템 등 우리 삶에 필수적인 체제에는 반드시 암호화 기술을 적용함.
- 인넷에서 교환하는 데이터는 항상 누군가 가로챌 수 있는 위험이 존재하고 블록체인도 예외는 아님.
- 블록체인의 안전한 운영과 이용을 위해서는 암호화 기술과 세부 메커니즘에 대한 지식을 이해해야 함.
- 사람이 이해하는 문장을 어떤 규칙에 따라 이해하지 못하는 형태로 변환해 교환하는 것을 암호화(Encryption)라고 함.
- 사람이 이해하는 문장을 '평문', 암호화한 문장을 '암호문(Cipher text)'이라고 하며, 암호문(또는 암호)을 평문으로 되돌리는 것을 '복호화(Decryption)'라고 함.

<p align="center">
<img src="/assets/img/blog/encryption_technology.png">
</p>

## 암호화 기술 - 과거의 암호화 기술

- 보통 암호화의 요소에는 '암호 만들기(암호화)', '암호 풀기(복호화)', 암호 만들기와 풀기에 사용하는 '키'가 있음.
- 기원전에는 특정 숫자만큼 알파벳 순서를 밀어내 읽는 '카이사르 암호(Caesar Cipher)'가 등장했고, 16세기에는 문자마다 배치를 바꾼 후 배치 변경 방식의 원리를 