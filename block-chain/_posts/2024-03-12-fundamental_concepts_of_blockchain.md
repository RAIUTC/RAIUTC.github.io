---
layout: post
title: Intro
description: |
  
categories: 블록체인
sitemap: false
hide_last_modified: true
---
# 블록체인 기초개념

## 블록체인의 정의

- NonFungible.com: A blockchain is a free tool to exchange information, ensuring better control of user data through cryptography. It is a unique database. There are rules on how data can be added but once uploaded, it's designed to be impossible for it to be erased, adapted or altered in any way.

> 블록체인은 정보 교환을 위한 무료 도구로, 암호학을 통해 사용자 데이터를 보다 효과적으로 통제합니다. 이는 독특한 데이터베이스입니다. 데이터가 추가되는 방법에는 규칙이 있지만 일단 업로드 되면 어떠한 방법으로도 삭제, 수정 또는 변경이 불가능하도록 설계되어 있습니다.

- Built In: A blockchain is a digital ledger or database where encrypted blocks of digital asset data are stored and chained together, forming a chronological single-source-of-truth for the data.

> 블록체인은 디지털 자산 데이터의 암호화된 블록이 저장되고 연결된 디지털 장부 또는 데이터베이스로, 데이터의 일관된 시간순 흐름을 형성한다.

- IBM: Blockchain is a shared, immutable ledger that facilitates the process of recording transactions and tracking assets in a business network.

> 블록체인은 기업 네트워크에서 거래 기록과 자산 추적 과정을 용이하게 하는 공유되고 변경할 수 없는 장부입니다.

- Deloitte: A blockchain is a "a technology that allows people who don't know each other to trust a shared record of events.". This shared record, or ledger, is distributed to all participants in a network who use their computers to validate transactions and thus remove the need for a third party to intermediate.

> 블록체인은 "서로를 모르는 사람들이 공유된 사건 기록을 신뢰할 수 있게 하는 기술"입니다. 이 공유된 기록 또는 장부는 모든 네트워크 참여자에게 분산되어 있으며, 그들은 자신의 컴퓨터를 사용하여 거래를 검증함으로써 중개자의 필요성을 제거합니다.

- AWS: Blockchain technology is an advanced database mechanism that allows transparent information sharing within a business network. A blockchain database stores data in blocks that are linked together in a chain. The data is chronologically consistent because you cannot delete or modify the chain without consensus from the network.

> 블록체인 기술은 기업 네트워크 내에서 투명한 정보 공유를 가능케 하는 고급 데이터베이스 매커니즘입니다. 블록체인 데이터베이스는 연결된 블록에 데이터를 저장합니다. 데이터는 네트워크의 합의 없이는 체인을 삭제하거나 수정할 수 없이 일관된 시간순 상태를 유지합니다.

- pwc: A blockchain is a decentralized ledger of all transactions across a peer-to-peer network. Using this technology, participants can confirm transactions without a need for a central clearing authority.

> 블록체인은 P2P(Person to Person)네트워크를 통한 모든 거래의 분산 장부입니다. 이 기술을 사용하면 참여자들은 중앙 결제 기관 없이도 거래를 확인할 수 있습니다.

- ChatGPT: A blockchain is a distributed database or ledger that is shared among the nodes of a computer network. As a database, a blockchain stores information electronically in digital format. Blockchains are best known for their crucial role in cryptocurrency systems, such as Bitcoin, for maintaining a secure and decentralized record of transactions. The innovation with blockchain is that it gurantees the fidelity and security of a record of data and generates trust without the need for a trusted third party.

> 블록체인은 컴퓨터 네트워크의 노드들 사이에서 공유되는 분산 데이터베이스 또는 장부입니다. 데이터베이스로서 블록체인은 정보를 전자적으로 디지털 형식으로 저장합니다. 블록체인은 암호화폐 시스템인 비트코인과 같은 곳에서 안전하고 분산된 거래 기록을 유지하는 데 가장 잘 알려져 있습니다. 블록체인의 혁신적인 점은 데이터 기록의 충실성과 안정성을 보장하여 신뢰를 생성하는 데에 신뢰할 수 있는 제 3자가 필요하지 않다는 것입니다.

## Blockchain Database vs Traditional Database

|구분|Database|Public Blockchain|
|:--:|:--:|:--:|
|유형|Permissioned|Public|
|작동|the Database has Create, Read, Update, and Delete operations.|Blockchain has only an Insert operation. or Read.|
|통제|Centralized|Decentralized|
|아키텍처|Client-Server architecture|Public Peer-to-Peer architecture|
|데이터 영속성|Non-persistence|Immutable(지속됨)|
|장애 가능성|Yes|No|
|속도|Extremely fast|Slow|

<p align="center">
<img src="/assets/img/blog/blockchain_vs_traditional.png">
</p>

## 블록체인과 분산원장

- 분산원장은 거래 정보를 기록한 원장을 특정 기관의 중앙화된 서버가 아닌 분산화된 네트워크에서 참여자들이 공동으로 기록 및 관리하는 기술임.
- 블록체인은 분산 장부 기술(Distributed Ledger Technology: DLT)을 활용하지만, 모든 분산장부 기술이 블록체인의 형태를 띠는 것은 아님.
- 비트코인(Bitcoin), 이더리움(Ethereum) 등이 '블록체인'에 해당함.
- 하이퍼레저 패브릭(Hyperledger Fabric), 코다(Corda), 인터레저(Interledger)등이 분산 장부 기술에 해당함.

<p align="center">
<img src="/assets/img/blog/distributed_ledger_tech.png">
</p>

## 블록체인과 기존 거래 방식의 차이 - 중앙관리자의 부재와 데이터 저장의 분산화

<p align="center">
<img src="/assets/img/blog/difference_beetween_blockchain_and_traditional_way.png">
</p>

## Economic Inefficiencies & Blockchain capability

> 경제적 비효율성 및 블록체인의 능력

|Economic Inefficiency|Brief description|Blockchain capability|
|:--:|:--:|:--:|
|Time to settle transactions|In the current business environment, transactions can take days, weeks, or months to settle.|The automatic execution of the agreed-upon well-understood consensus protocol with the peace of mind that transactions once committed cannot be altered reduces the time to settle transactions.|
|Fees paid to third parties|Financial institutions such as banks and credit card processors charge fees to process currency exchange transactions.|P2P transactions eliminate powerful, centralized third parties, reducing fees. Fees in blockchain are designed to incentivize transacting parties to maintain the working of the consensus protocol and the synchronization of the distributed ledgers.|
|Data-related redundant work, rework, and reconciliation work[the three R's]|Since each party involved in a business maintains proprietary data, they incurunncecessary costs creating, maintaining, and reconciling these data.|Authentically identical copies of the distributed ledger, well-understood consensus protocol, and software-based smart contracts will greatly reduce the inefficiency.|
|Fraud|The complexity in our current systems for value exchange and the lack of transparency create opportunities for fraud.|The transparency of the consensus protocol and smart contracts reduce the opportunity of fraud.|
|Constraints from goverment regulations and rules from nongovermental organizations|Goverment regulations, created ostensibly to help, lead to increased unnecessary costs. In some industries, firms voluntarily agree to adhere to rules imposed by nongovermental industry groups that can also add costs and stifle innovation.|The ability for parties that do not trust each orhter to transact without the facilitation of third parties reduces the necessity of goverment regulations and rules from membership and advocacy nongovermental organizaions.|
|Data security risks|Proprietary centralized data stroes are inviting targets for dalicious actors to breach and harness.|The lack of centralized proprietary data sources reduces security breach targets, encryption, and hashing, and the ability to reconstruct the distributed ledger reduces the impact of a security breach.|

|경제적 비효율성|간략한 설명|블록체인의 능력|
|:--:|:--:|:--:|
|거래 결제 시간|현재의 비즈니스 환경에서는 거래가 처리되기까지 몇 일, 몇 주 또는 몇 달이 소요될 수 있습니다.|거래가 일단 처리되면 변경할 수 없다는 확신과 함께 합의된 명확한 합의 프로토콜의 자동 실행은 거래 결제 시간을 줄입니다.|
|제 3자에게 지불되는 수수료|은행 및 신용카드 프로세서와 같은 금웅 기관은 화폐 교환 거래를 처리하기 위해 수수료를 부과합니다.|P2P 거래는 강력하고 중앙집중화된 제 3자를 제거하여 수수료를 감소시킵니다. 블록체인의 수수료는 거래 당사자들에게 합의 프로토콜의 작동과 분산 장부의 동기화를 유지하도록 동기 부여하기 위해 설계되었습니다.|
|데이터 관련 중복 작업, 재작업 및 조정 작업(the three R's)|각 사업 참여 당사자가 독자적인 데이터를 유지하기 때문에, 이들은 이러한 데이터를 생성, 유지 및 조정하는 데 불필요한 비용을 발생합니다.|분산 원장, 명확한 합의 프로토콜 및 소프트웨어 기반 스마트 계약의 진정한 동일한 사본은 비효울성을 크게 감소시킬 것입니다.|
|사기 위험성|현재 가치 교환 시스템의 복잡성과 투명성의 부재는 사기 가능성을 만들어냅니다.|합의 프로토콜과 스마트 계약의 투명성은 사기 가능성을 줄입니다.|
|정부 규정 및 비정부 기관의 규칙으로 인한 제약|도움을 위해 만들어진 정부 규정은 불필요한 비용 증가로 이어집니다. 일부 산업에서는 비정부 산업 단체가 부과한 규칙을 자발적으로 준수하는 회사도 있으며, 이는 비용을 증가시키고 혁신을 억제할 수 있습니다.|서로 신뢰하지 않는 당사자들이 제3자의 중계 없이 거래할 수 있는 능력은 정부 규정 및 회원 및 지지 비정부 단체 규칙의 필요성을 줄입니다.|
|정보 보안 위험성|독립적인 중앙 집중식 데이터 저장소는 악의적인 행위자들이 침입하여 이용할 수 있는 적극적 대상입니다.|중앙 집중식 독점 데이터 소스의 부재는 보안 침해 대상을 줄이며, 암호화 및 해싱, 그리고 분산 장부를 재구성할 수 있는 능력이 줄어들어 보안 침해의 영향을 줄입니다.|

## 블록체인 트랜잭션 프로세스

<p align="center">
<img src="/assets/img/blog/blockchain_transaction_process.png">
</p>

## 블록과 블록체인

<p align="center">
<img src="/assets/img/blog/block_and_blockchain.png">
</p>

## 블록 해시로 연결된 블록 간의 관계

<p align="center">
<img src="/assets/img/blog/block_hash_relationship.png">
</p>

## 중요 서류와 블록체인 기반 원장의 연결구조 비교

<p align="center">
<img src="/assets/img/blog/important_documents_and_blockchain_ledger.png">
</p>

## 블록체인 거래정보 기록 예

<p align="center">
<img src="/assets/img/blog/blockchain_transaction_record_example.png">
</p>

## 채굴(Mining) 하드웨어

<p align="center">
<img src="/assets/img/blog/mining_hardware.png">
</p>

## 블록체인 유형 - 퍼블릭 블록체인

- 퍼블릭 블록체인은 누구든지 자유롭게 블록체인 네트워크에 참여하여 이용할 수 있는 방식.
- 원칙적으로 모든 거래 내용이 블록에 저장되어 모든 참가자 사이에 공유.
- 블록체인의 전형적인 특징을 갖추고 있는 유형으로, 비트코인이나 이더리움 같이 일반적인 암호화폐에서 사용되는 방식.
- 메인서버가 없이 전체 노드가 데이터베이스를 공동 관리하기 때문에 해킹등 데이터 위변조가 사실상 불가능하다는 장점이 있음.
- 하지만 네트워크 확장이 어렵고 속도가 느리다는 단점이 있어 중앙시스템 제어가 필요한 금융서비스에는 부적합.

<p align="center">
<img src="/assets/img/blog/public_blockchain.png">
</p>

## 블록체인 유형 - 프라이빗 블록체인

- 프라이빗 블록체인에서는 네트워크를 운영하는 주체가 있고, 이러한 주체가 새로운 참가자의 네트워크 참여 여부를 결정하며 허가할 권한과 관련 규칙을 결정할 권한을 가짐.
- 주로 특정한 기관이나 업체들이 자신들의 필요와 특성에 맞게 설계한 블록체인으로, 관리자의 의도대로 규칙 변경이나 기존 기록 수정 등을 할 수 있기 때문에 블록체인의 장점이자 특성인 투명성과 탈중앙화는 사라지게 됨.
- 프라이빗 블록체인은 네트워크 참가자 수가 상대적으로 적어 거래 정보가 적은 수의 노드에서만 공유되고 처리되기 때문에 퍼블릭 블록체인보다 거래 속도가 빠르고 효율적이라는 장점이 있음.
- B2B 거래 처리의 인프라로 많이 사용되는 방식임.

<p align="center">
<img src="/assets/img/blog/private_blockchain.png">
</p>

## 블록체인 유형 - Hybrid/Consortium 블록체인

- 하이브리드 블록체인은 사전에 설정된 기준을 충족하는 사용자에게 액세스 권한을 부여하는 <span style="color:red"><u>단일 기업이 운영</u></span>. 
- 진정한 의미의 분산형은 아니지만, 이러한 '허가형' 블록체인은 B2B 사용 사례 및 정부 응용 분야에 적합.
- 블록체인을 읽거나 블록체인에 트랜잭션을 제출할 권한은 공개될 수도 있고 참여자에게만 제한될 수도 있음.
- 컨소시엄 블록체인에서 합의 프로세스는 <span style="color:red"><u>사전 선택 그룹</u></span>(예: 기업 그룹 등)으로 제한되고 블록체인을 읽거나 블록체인에 트랜잭션을 제출할 권한은 공개될 수도 있고 참여자에게만 제한될 수도 있음.
- 컨소시업 블록체인은 '허가된 블록체인'으로 간주되며, 비즈니스에서 사용하기에 가장 적합.

<p align="center">
<img src="/assets/img/blog/hybrid_consortium_blockchain.png">
</p>

## 블록체인 유형 - 유형별 특징

|구분|퍼블릭 블록체인|폐쇄형 블록체인(프라이빗 블록체인)|폐쇄형 블록체인(컨소시험 블록체인)|
|:--:|:--:|:--:|:--:|
|관리주체|모든 거래 참여자|하나의 중앙기관|컨소시엄 참여자|
|거버넌스|한 번 정해진 규칙은 바꾸기 어려움|중앙기관이 쉽게 규칙을 바꿀 수 있음|참여자들 간 합의로 규칙을 바꿀 수 있음|
|네트워크 확장|어려움|매우 쉬움|쉬움|
|네트워크 유지 비용|유지비용이 큼|유지비용이 작음|비용이 거의 없음|
|거래속도|느림|빠름|퍼블릭 블록체인에 비해 빠름|
|데이터 접근|모든 사용자에 제한 없음|허가 받은 사용자|허가 받은 사용자|
|식별성|익명성|식별 가능|식별 가능|
|거래증명|네트워크 참여자 누구나 거래 검증 및 승인을 할 수 있음. 거래 증명자는 사후에 알고리즘에 따라 결정|중앙기관이 거래 증명|거래증명자가 인증을 거쳐 알려진 상태|
|활용사례|비트코인, 이더리움|Ripple Labs, BrurstIQ, 링크(Linq)|하이퍼레저 패브릭, Corda, Quorum|

## 블록체인 유형 선택

- The <span style="color:red">access dimension</span> determines who is allowed to participate in the blockchain network. Participation in the blockchain would imply getting access to the blockchain software, creating a node that executes this software, and being connected to one or more peer nodes.

> <span style="color:red">접근 차원</span>은 누가 블록체인 네트워크에 참여할 수 있는지를 결정합니다. 블록체인에 참여하는 것은 블록체인 소프트웨어에 액세스하고, 이 소프트웨어를 실행하는 노드를 생성하며, 하나 이상의 동료 노드에 연결되는 것을 의미합니다.

- The <span style="color:red">privacy dimension</span> determines whether transactions require information identifying the parties involved in the transaction or not.

> - <span style="color:red">개인 정보 보호 차원</span>은 거래가 거래에 참여한 당사자를 식별하는 정보를 필요로 하는지 여부를 결정합니다.

<p align="center">
<img src="/assets/img/blog/choose_blockchain_type.png">
</p>

## Benefits and features of blockchain

- **Faster dealings**
    - 무역금융, 보험, 자본시장 등의 업무에서 검증, 조정, 승인 등에 필요한 긴 프로세스를 짧은 시간에 처리할 수 있음.

- **Cost-saving**
    - 제 3자 기관이 필요하지 않기때문에 수수료 형태의 간접비를 절감.

- **Smart property**
    - 디지털 자산이나 물리적 재산을 다른 사람이 권리를 주장할 수 없게 안전하고 정확한 방식으로 블록체인에 연동하는 것이 가능함.
    - 소유권자는 자신의 자산을 완전히 통제하고 있으며, 타인이 중복 사용하거나 소유할 수 없음.

- **Decentralization**
    - 블록체인의 핵심 개념이자 장점으로 신뢰할 수 있는 제3자나 중개자가 거래를 검증할 필요가 없으며, 대신 합의 매커니즘을 사용하여 거래의 유효성을 합의함.

- **Transparency and trust**
    - 블록체인이 공유되고 모든 사람이 블록체인에 무엇이 있는지 볼 수 있기 때문에 시스템이 투명해지고 신뢰가 확립됨.
    - 이는 수익자 선정과 관련하여 개인의 재량권이 제한되어야 하는 기금 또는 복리후생과 같은 시나리오에서 적절하게 사용될 수 있음.

- **Immutability**
    - 일단 블록체인에 데이터가 작성되면 다시 데이터를 변경하는 것은 거의 불가능함.
    - 이는 불변하는 거래 대장을 유지하는 이점으로 간주되며, 특히 감사 및 규정 준수 시나리오에서 유용하게 적용할 수 있음.

- **High availability**
    - 시스템이 P2P 네트워크의 수천 개의 노드를 기반으로 하고 데이터가 모든 노드에서 복제 및 업데이트 되므로 시스템의 가용성이 높아짐.
    - 일부 노드가 네트워크에 액세스할 수 없게 되더라도 네트워크는 계속 작동하므로 가용성이 높음.

- **Highly secure**
    - 블록체인의 모든 트랜잭션은 데이터의 무결성과 가용성을 보장하는 입증된 암호화 기술을 기반으로 함.

- **Platform for smart contracts**
    - 블록체인은 사용자를 대신하여 비즈니스 로직을 실행하는 프로그램을 실행할 수 있는 플랫폼.

## Limitaions of blockchain technology

- **Interoperability**
    - 기업 시스템과의 블록체인의 상호운영성과 서로 다른 블록체인 간의 상호운용성, 즉 크로스 체인 상호운용성이 확보되어야 함.
    - 블록체인은 사일로에 존재할 수 없으며, 기업 내부 시스템과 통신할 수 있어야 기업이 기술을 최대한 활용하고 서로 간에 이점을 누릴 수 있음.
    - 예를 들어 이더리움과 솔라나 블록체인은 서로 간에 자산을 이전할 수 있어야 함.
    - 또한 블록체인의 데이터는 기업 애플리케이션이 블록체인 기술의 장점을 활용할 수 있도록 내부 기업 네트워크로 이동할 수 있어야 하며, 그 반대도 가능해야 함.

- **Relatively immature technology**
    - 기존 IT 시스템에 비해 블록체인은 상대적으로 신기술이며 기술 완성도를 높이기 위한 시간과 노력이 필요함.
    - Solana, Polkadot, Avalanche와 같은 최신 블록체인은 완성도가 높은 편이지만 사용자 경험, 개발자 경험, 보안과 상호 운용성과 같은 부분은 더욱 개선되어야 함.

- **Adoption barrier**
    - 블록체인 기술이 대량으로 도입되기까지는 확장성, 보안, 규제 및 고객 신뢰도 측면에서 발생하는 일부 문제를 해결해야 함.
    - 해킹으로 수백만 명이 손해를 본 디파이처럼 보안 문제로 인해 고객 신뢰도가 떨어지면, 일부 사용자가 네트워크에 가입하지 못할 수 있음.

- **Privacy**
    - 모든 사람이 모든 거래를 볼 수 있는 비트코인과 같은 퍼블릭 블록체인의 경우 사생활 침해가 우려되고, 이러한 투명성은 금융, 법률 또는 의료 분야와 같은 산업에서는 바람직하지 않음.

## 블록체인 발전 역사

<p align="center">
<img src="/assets/img/blog/history_of_blockchain.png">
</p>