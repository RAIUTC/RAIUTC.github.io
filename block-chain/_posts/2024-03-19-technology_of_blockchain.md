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

## 암호화 기술 - 메시지 전송의 위험

<p align="center">
<img src="/assets/img/blog/risk_of_message_transmission.png">
</p>

## 암호화 기술 - 보안의 3요소

- 정보 보안(Information Security)은 조직이나 개인의 중요 정보를 보호하는 과정과 관행.
- 보안의 3요소는 정보 보안을 유지하는 데 있어 필수적인 원칙

<p align="center">
<img src="/assets/img/blog/three_elements_of_security.png">
</p>

## 암호화 기술 - 인증 구현 방법

<p align="center">
<img src="/assets/img/blog/authentication_implementation_method.png">
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
- 기원전에는 특정 숫자만큼 알파벳 순서를 밀어내 읽는 '카이사르 암호(Caesar Cipher)'가 등장했고, 16세기에는 문자마다 배치를 바꾼 후 배치 변경 방식의 원리를 배열 형태로 표로 기록한 '비즈네르 암호(Vigenere Cipher)'가 등장했음.
- 이러한 암호화 방법의 특징을 합해 20세기 중반에는 암호 기계를 이용하는 '에니그마(Enigma) 암호' 등도 등장.
- 다양한 암호화 방식이 있지만, 공통적인 특징은 암호화와 복호화 방법, 암호를 푸는 키를 외부에 알리지 않아야 하는 것임.

<p align="center">
<img src="/assets/img/blog/encryption_technology_2.png">
</p>

## 암호화 기술 - 현대의 암호화 기술

- 현대 암호화 기술의 특징은 암호화, 복호화, 키를 만드는 방법 자체는 비밀이 아니라는 것임. 비밀로 해야 할 사항은 공개된 방법대로 만든 개별 키임.
- 현대 암호화 기술은 보통 대칭 키 암호(Symmetric Key Cryptography)와 공개 키 암호(Public Key Crtptography) 방식을 사용함.
- 블록체인에서는 공개 키 암호를 많이 사용하고 키 길이가 짧은 타원 곡선 암호(Elliptic Curve Cryptography)를 자주 사용함.
- 공개 키는 용어 그래로 널리 공개해도 상관없는 키지만, 비밀 키는 문서 작성자만 알아야 하는 키로 절대로 다른 사람에게 알려져서는 안됨.

<p align="center">
<img src="/assets/img/blog/modern_encryption_technology.png">
</p>

## 암호화 기술 - 대칭키 암호(Symmetric-key algorithm)

- 암호화와 암호 해독에 사용되는 키가 동일함. 간결한 방식이어서 네트워크나 CPU의 오버헤드 부담이 적고 속도가 빠름. 데이터 교환보다는 한 곳에 보관될 때 선호하는 암호화 방법.
- 송신자에서 수신자에게 안전하게 키가 전송되어야 하므로 두 당사자는 서로를 신뢰하고 키 전송을 위한 <u><span style="color:red">신뢰할 수 있는 채널 설정이 필요함</span></u>.
- 신뢰할 수 있는 보안 채널을 설정하는 것은 비용이 많이 들 수 있어서 대칭 키 암호화는 서로를 알고 신뢰할 수 있는 채널 인프라를 구축하는 데 투자할 수 있는 당사자로 제한됨.
- 허가 받지 않은 제삼자가 해당 키를 가지게 되면 해당 키를 사용한 모든 데이터의 보안에 위협이 됨.

<p align="center">
<img src="/assets/img/blog/symmetric_key_algorithm.png">
</p>

## 암호화 기술 - 공개키 암호(Public-key Cryptography or asymmetric cryptography)

- 공개 키 암호는 암호를 만드는 키와 푸는 키가 서로 다른 비대칭 암호화. 공개 키로 암호화한 문서는 짝을 이루는 비밀 키로 풀어야 한다는 특성이 있음.
- 블록체인처럼 여러 참여자가 있는 네트워크에서 특정 사람에게만 문서 접근과 제어 권한을 부여할 때는 '공개 키 암호'가 유용함.
- 공개키로 암호화한 문서는 비밀키로만 복호화하는 특성 때문에 특정 사람만 어떤 작업이 가능한 구조를 만드는데 적합.

<p align="center">
<img src="/assets/img/blog/public_key_algorithm.png">
</p>

## 암호화 기술 - 디지털 서명

- 디지털 서명(Digital Signatures)은 작성자를 증명하는 기술로 해싱, 서명, 검증 이 세 가지 알고리즘으로 이루어짐.
- 블록체인에서 디지털자산의 트랜잭션에 서명하고 승인하는 데 사용되기도 하며, 데이터 전송, 계약, 분산신원인증(DID, Decentralized Identity) 등에 사용됨.

<p align="center">
<img src="/assets/img/blog/digital_signature.png">
</p>

## 암호화 기술 - 해시 함수(hash function)

- 블록체인의 거래 내역을 암호화하기 위해 해시함수(hash function)을 사용함. 해시 함수는 임의의 길이의 데이터를 고정된 길이의 데이터로 매핑하는 함수.
- 비트코인뿐만 아니라 정보 보안 분야에서 널리 쓰이는 함수로, 데이터를 정해진 길이의 무작위 문자열로 치환함.
- 입력 문자열 데이터의 크기에 상관없이 출력의 길이는 항상 고정되어 있음. 예를 들어 SHA-256 해싱 알고리즘과 함수를 임의의 입력 길이로 사용하면 항상 256비트 출력 데이터가 생성됨.
- 결과값에서 입력 데이터를 추론할 수 없기 때문에 입력 데이터의 추론을 불가능함.

<p align="center">
<img src="/assets/img/blog/hash_function.png">
</p>

- SHA-256 해싱 알고리즘을 이용한 해시 함수는 입력값이 1바이트든, 1메가바이트든 출력값은 항상 64자리의 16진수 고정임.
- 입력한 값이 조금만 달라도 전혀 다른 값을 얻고 누가 함수를 실행하든 같은 값을 넣으면 같은 결과값을 얻게 됨.
- 이러한 특성들 때문에 원래 텍스트와 같은 지 다른 지를 쉽게 알 수 있음.
- 텍스트 뿐만 아니라 파일에도 해시 함수를 적용할 수 있음. 특정 파일에 대해 원본과 같고 손상되지 않았다는 것을 확인 할 수 있음.

<p align="center">
<img src="/assets/img/blog/hash_function_2.png">
</p>

<p align="center">
<img src="/assets/img/blog/hash_function_3.png">
</p>

## 암호화 기술 - 해시 함수(hash function) - 논스

- 블록의 해시값은 해당 블록의 생성일시, 버전, 비츠(bits), 루트해시, 이전 블록의 해시, 그리고 논스(nonce)라고 불리는 임시값 등을 조합한 후 해시로 변환하여 생성함.
- 해시는 랜덤하게 생성되기 때문에, 수없이 많은 연산을 반복해서 난이도에 따라 미리 자동으로 정해진 목표값 이하의 해시값을 찾아야 함. 이때 랜덤한 해시값을 생성할 수 있도록 매번 임시값을 사용해야 하는데, 그 임시값이 바로 논스임.
- 이처럼 특정한 블록에 대해 목표값 이하의 크기를 가진 해시값을 생성하는 논스값을 찾음으로써 새로운 블록을 생성하는 행위를 작업증명(PoW)이라고 함.

<p align="center">
<img src="/assets/img/blog/nonce.png">
</p>

<p align="center">
<img src="/assets/img/blog/nonce_2.png">
</p>

- 아래 그램은 모든 트랜잭션 데이터에 단계적으로 해시함수를 적용하여 하나의 해시값으로 나타내는 구조를 '머글트리'라고 함.
- 우측 그림에서 만일 세 번째 트랜잭션에서 데이터를 4BTC에서 5BTC로 변경한다면 관련된 모든 해시값이 연달아 변경되는 것을 확인할 수 있음.
- 모든 데이터에 대한 수정 여부를 점검할 필요 없이 머클 루트만 점검해도 모든 데이터의 수정 여부를 체크할 수 있음.

<p align="center">
<img src="/assets/img/blog/merkle_tree.png">
</p>

<p align="center">
<img src="/assets/img/blog/merkle_tree_2.png">
</p>

> 암호학적 알고리즘에서의 '적인효과'
- 데이터의 작은 변경이 크게 다른 출력을 유발할 수 있습니다.
- 이 기능은 블록체인에서 데이터를 신뢰할 수 있고 안전하게 만듭니다.
- 블록 데이터의 변경은 일관성을 상실하고 블록체인을 망가뜨려 무효화할 수 있습니다.

> 고유성
- 각 입력에는 고유한 출력이 있습니다.

> 결정론적
- 동일한 해시 함수를 통과하는 경우 입력이 항상 동일한 출력을 가집니다.

> 빠름
- 출력은 매우 짧은 시간 내에 생성될 수 있습니다.

> 역공학 불가
- 출력과 해시 함수를 가지고 입력을 생성할 수 없습니다.
- 더 나아가, 해시 함수는 블록 간의 연결 및 각 블록 내에 저장된 데이터의 무결성을 유지하는 데 중요한 역할을 합니다.

## 암호화 기술 - 영지식 증명이란?

- 영지식 증명(Zero-knowledge proof, ZKP)은 증명자(prover)가 검증자(verifier)에게 자신의 주장(statement)이 사실임을 증명하는데 사용되는 암호화 기술이라고 할 수 있으며, 증명자는 자신의 주장을 증명하기 위해서 검증자에게 자신의 주장에 관한 어떤 정보도 제공(유출)하지 않으며, 검증자는 증명자의 주장에 대한 어떤 정보도 알지 못한 상태에서 검증을 수행하게 됨.
- 이처럼 영지식 증명에서는 증명자가 자신의 주장과 관련된 정보 노출을 배제시키면서 자신의 주장을 증명할 수 있기 때문에 사용자의 프라이버시가 중요한 부분에 사용될 수 있음.

<p align="center">
<img src="/assets/img/blog/zero_knowledge_proof.png">
</p>

- 영지식 증명이 무엇이고 어떻게 가능한지를 설명할 때 가장 흔하게 볼 수 있는 예가 알리바바의 동굴(AliBaba cave) 문제임. 즉, 앨리스(Alice)와 밥(Bob)이 있을 때, 밥은 자신이 동굴 안에 있는 문을 열 수 잇는 열쇠가 있다는 것을 증명하고 싶고 증명 과정은 다음과 같은 과정으로 진행됨.
- 이때 중요한 부분은, 밥은 자신이 열쇠가 있다는 사실을 증명하기 위해서 앨리스에게 열쇠를 보여 주지 않고 증명 과정이 수행된다는 것임.

<p align="center">
<img src="/assets/img/blog/zero_knowledge_proof_2.png">
</p>

## 암호화 기술 - 영지식 증명 - 활용분야

<p align="center">
<img src="/assets/img/blog/zero_knowledge_proof_3.png">
</p>

## 스마트 계약(Smart contract)

- 스마트 컨트랙트(smart contract)은 중간에 제3의 보증기관 없이 상호간에 계약상의 급부와 반대급부를 프로토콜화(protocolization)하여 소프트웨어 및 하드웨어에 미리 저장하고 해당 계약을 이행하는 과정에서 조건 충족 여부에 대한 판단을 인간이 아닌 컴퓨터 등의 기계가 대신 실행하는 개념.
- 프로그래밍 언어를 사용하여 계약 기간, 금액, 조건 등을 미리 코딩해두면 부동산 거래, 중고 자동차 거래, 무역 거래 등 어떠한 종류의 계약도 자동 실행되도록 만들 수 있음.

<p align="center">
<img src="/assets/img/blog/smart_contract.png">
</p>

## 스마트 계약 - 블록체인의 스마트 계약

- 스마트 계약은 1994년 닉 재보(Nick Szabo)가 처음 고안한 개념으로 "계약에 필요한 요소를 코드를 통해 스스로 실행되게 하는 전산화된 거래 약속"이라고 정의함.
- 계약 성립의 필요 조건이 기록된 거래 내용이 변조하기 어려운 상태로 블록체인에 기록되어, 거래 내용에 적힌 조건이 충족되면 자동으로 성립하는 트랜잭션이 스마트 계약임.
- 아래의 그림과 같이 트랜잭션을 블록체인에 배포하고 승인한 시점에 아직 계약조건을 충족하지 않았지만 일주일이 지나면 조건을 자동으로 만족한다고 해석하여 계약을 이행함.
- 기존의 블록체인 1.0 기술이 '과거에 일어났던 일'을 기록한다면, 스마트 계약 기능을 구현한 블록체인 2.0 기술은 '미래에 일어날 일'을 미리 기록해 둘 수 있음.

<p align="center">
<img src="/assets/img/blog/smart_contract_2.png">
</p>

<p align="center">
<img src="/assets/img/blog/smart_contract_3.png">
</p>

> 스마트 계약은 계약 조건을 실행하는 전자 거래 프로토콜입니다. 일반적인 목표는 일반적인 계약 조건 (결제 조건, 저당, 비밀 유지 등)을 충족시키고, 악의적이거나 우연한 예외를 최소화하며, 신뢰할 수 있는 중개인의 필요성을 최소화하는 것입니다. 관련된 경제적 목표에는 사기 손실, 중재 및 집행 비용, 그리고 기타 거래 비용을 줄이는 것이 포함됩니다.

- 이더리움 네트워크가 트랜잭션을 처리한 후, 이더리움 네트워크에 스마트 계약을 바이트코드 형식으로 저장.

<p align="center">
<img src="/assets/img/blog/smart_contract_4.png">
</p>

## 스마트 계약 설계의 기본 원칙

- 스마트 계약은 자동화된 조건부 실행을 허용하는 프로그래밍 코드로, 블록체인 기술을 기반으로 함.
- 스마트 계약을 설계할 때는 이러한 특성을 고려한 기본 원칙을 고려해야 함.

<p align="center">
<img src="/assets/img/blog/smart_contract_design_principles.png">
</p>

## 스마트 계약(Smart contract) - 보험사례

- 스마트 컨트랙트는 블록체인 상에서 전자 계약서로 이루어지며, 계약 당사자들끼리 합의한 내용 및 조건이 충족되면 자동으로 실행(self-execution)되도록 설계되어 있음.
- 계약 내용을 스마트 컨트랙트 소스 코드로 작성하여 블록체인 네트워크에 전송하면 네트워크 참여자(노드)들의 유효성 검증이 이뤄지며, 검증 완료 시 해당 스마트 컨트랙트가 포함된 블록이 생성되며 배포됨.
- 예를 들면, 계절적 강우량 등 특정 날씨 정보를 기반으로 보험에 가입하는 스마트 계약을 사용하여 특정 장소의 강우량이 당초 명시된 양을 초과할 경우 자동으로 보험금을 지급.

<p align="center">
<img src="/assets/img/blog/smart_contract_insurance.png">
<img src="/assets/img/blog/smart_contract_insurance_2.png">
</p>