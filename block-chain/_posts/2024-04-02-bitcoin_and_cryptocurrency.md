---
layout: post
title: 비트코인과 암호화폐
description: |
  비트코인과 암호화폐에 대한 포괄적인 이해를 제공하는 글입니다. 초기 비트코인의 발행과 작동 원리부터 블록체인 기술의 구조, 비트코인과 이더리움의 차이, 그리고 코인과 토큰의 개념까지 다루고 있습니다. 또한 알트코인과 스테이블코인, 그리고 지갑의 종류와 평가까지 포함되어 있습니다.
categories: 블록체인
sitemap: false
hide_last_modified: true
---

# 비트코인과 암호화폐

## 비트코인의 첫 번째 블록

- 사토시 나카모토는 비트코인의 첫번째 블록인 제네시스(genesis) 블록에 2009년 1월 3일 영국 The Times의 1면 기사 제목을 포함시킴. 중앙은행의 금융기관 규제에 대한 반발로 탈중앙화 기반의 가상화폐를 만들었다는 것을 암시적으로 표현함.

<p align="center">
<img src="/assets/img/blog/genessis_block.png">
</p>

## 비트코인과 블록체인 발명을 뒷받침하는 다양한 아이디어

- 전자화폐 체계, 분산 시스템, PoW 매커니즘, 암호화 방법들이 결합되어 비트코인과 블록체인 탄생에 영향을 줌.

<p align="center">
<img src="/assets/img/blog/bitcoin_ideas.png">
</p>

## 비트코인 작동 원리

- 블록체인에서 새로운 트랜잭션이 생성되어 전파되면 바로 동기화되는 것이 아니라 각 노드가 전파된 트랜잭션들을 모아서 후보블록을 각각 생성하고 각 노드에 있는 후보블록들이 경쟁하여 하나의 대표블록을 선정함.
- 그리고 이렇게 선정된 대표블록을 다시 전파하는 형식으로 동기화 함.

<p align="center">
<img src="/assets/img/blog/bitcoin_operation.png">
<img src="/assets/img/blog/bitcoin_operation2.png">
<img src="/assets/img/blog/bitcoin_operation3.png">
</p>

## 비트코인 노드 구성도

- 비트코인 네트워크에 참여하는 각각의 컴퓨터를 노드라고 함. 노드(Node)는 <u><span style="color:red">지갑, Memory Pool, 블록체인</span></u>으로 구성되어 있음.

<p align="center">
<img src="/assets/img/blog/bitcoin_node.png">
</p>

## 비트코인 노드 네트워크 참여

- Bitcoin Core라는 소프트웨어가 설치돼 있어야 노드로 참여할 수 있음.
- 각 노드는 모두 동등한 권한을 가지며 검증과 합의 과정을 거쳐 중앙시스템 없이도 작동이 가능.
- 노드들은 각각 동일한 블록체인 장부를 저장하고 있음.

<p align="center">
<img src="/assets/img/blog/bitcoin_node_network.png">
</p>

## 비트코인 블록

- 2024년 3월 기준으로 비트코인은 약 83만개의 블록까지 연결되어 있으며 10분마다 블록 생성.
- 첫번째 블록의 번호는 '0'이며 제네시스 블록(Genesis Block)이라고 함.
- 비트코인은 중앙권한이나 은행이 없는 운영을 위해 P2P 기술을 사용하고 거래의 관리와 비트코인의 발행은 네트워크에 의해 공동으로 이루어짐.
- 비트코인은 오픈소스이고 공개적으로 개발되었으며 그 누구도 비트코인을 소유하거나 조종하지 않으며, 누구나 비트코인을 사용하고 비트코인에 참여할 수 있음.

<p align="center">
<img src="/assets/img/blog/bitcoin_block.png">
</p>

## 비트코인 트랜잭션 - Transaction Per Second

- 트랜잭션 요청 &rarr; 노드 전달 &rarr; 검증 &rarr; 새로운 노드에 전달의 과정을 거치기 때문에 블록체인에서의 트랜잭션은 일반 은행의 거래 방식에 비해 상당히 많은 시간이 걸림.
- TPS(Transaction Per Second) 수치로 비교해보면, Visa의 경우 초당 평균 17,000개가 생성되지만 비트코인은 5개 이하의 트랜잭션이 생성됨.

<p align="center">
<img src="/assets/img/blog/bitcoin_transaction.png">
</p>

## 블록체인 트릴레마(Blockchain Trilemma)

- 블록체인 트릴레마(Blockchain Trilemma)는 어떠한 블록체인도 탈중앙성, 보안성, 확장성 중 두 가지는 확보할 수 있으나, 동시에 세 가지 모두를 가질 수 없음을 표현.

<p align="center">
<img src="/assets/img/blog/blockchain_trilemma.png">
</p>

- 탈중앙화 보안을 최적화하는 것이 주요 우선순위라면, 통제의 분산으로 인해 트랜잭션을 검증하는 데 더 오랜 시간이 걸려 확장성이 낮아짐.
- 높은 보안과 확장성을 원한다면, 통제가 소수에 의해 이루어지기 때문에 탈중앙화 구성 요소는 약화됨.
- 탈중앙화와 확장성을 우선시한다면 보안 측면이 약해 짐. 참가자가 적을수록 블록체인은 공격에 더 취약해짐.

<p align="center">
<img src="/assets/img/blog/blockchain_trilemma2.png">
</p>

## 비트코인 발행계획

- 비트코인은 새로운 블록을 채굴할 때마다 고정된 수의 BTC를 발행할 권리를 얻음.
- 첫 50BTC는 비트코인 설계 시 정한 규칙에 따라 발행한 것이며, 21만 블록마다 보상이 반으로 줄어듦.
- 2024년 3월 24일 누적으로 836,111개의 블록을 생성하고 19,663,187개의 BTC를 채굴했으며, 이는 전체 발행양의 약 93.6%임(www.blockchain.com 참고).

<p align="center">
<img src="/assets/img/blog/bitcoin_issue.png">
</p>

## 비트코인 반간기 가격 변동

<p align="center">
<img src="/assets/img/blog/bitcoin_price.png">
</p>

## 비트코인과 이더리움의 차이 - 튜링 완전성

- 튜링 완전(turing complete)은 컴퓨터가 개발되기전인 1936년 영국의 수학자인 튜링에 의해 최초로 제시된 개념
- 이처럼 현존하는 모든 문제를 풀 수 있는 기계를 '튜링머신'이라고 했고 튜링머신은 튜링 완전 언어를 이용한 알고리즘을 통해서 구현될 수 있다고 주장.
- 튜링은 프로세스를 충분히 작은 단위로 분할하고 이를 조건문과 반복문을 통해 알고리즘으로 구현하면 세상의 모든 문제를 풀 수 있다고 생각.
- 즉, IF 조건문과 For/While 반복문을 활용하여 알고리즘을 구현하면 다양한 문제 해결이 가능하다고 생각함.

<p align="center">
<img src="/assets/img/blog/bitcoin_ethereum.png">
</p>

## 금화본위제와 비트코인의 화폐발행 방식

<p align="center">
<img src="/assets/img/blog/bitcoin_gold.png">
</p>

## 화폐발행 철학

<p align="center">The steady addition of a constant of amount of new coins is analogous to gold miners expending resources to add gold to circulation. In our case, it is CPU time and electricity that is expended.</p>
<p align="center">새로운 화폐 발행 방식은 금을 채굴하는 것과 유사하게 일정한 화폐량을 안정적으로 공급하는 방식이다. 금 채굴에 일정한 노력과 작업이 소요되는 것처럼 비트코인에서는 CPU 연산과 에너지 소비라는 자원을 통해 화폐를 발생한다.</p>

## 비트코인과 이더리움 차이

- 비트코인 블록체인은 화폐 서비스를 위해 개발되었고 화폐 시스템에 특화되어 있는 반면, 이더리움은 다양한 앱(App)이 블록체인 기반으로 서비스되는 것을 지원하는 기반 범용 블록체인 플랫폼.
- 이더리움은 플랫폼으로서 다양한 서비스가 구현되는 것을 지원하기 위해 스마트 컨트랙트와 EVM이라는 기능을 새롭게 설계했으며, 다양한 서비스(DApp) 구현이 가능하도록 개발 도구를 지우너할 뿐만 아니라 서비스 구현에 필요한 토큰을 발행할 수 있도록 ERC-20 표준도 제공.

<p align="center">
<img src="/assets/img/blog/bitcoin_ethereum2.png">
</p>

## 화폐의 세 가지 조건

<p align="center">
<img src="/assets/img/blog/money_condition.png">
</p>

## 비트코인 가격

<p align="center">
<img src="/assets/img/blog/bitcoin_price2.png">
</p>

## 비트코인으로 거래된 최초의 피자

- 2010년 5월 22일, 플로리다에 거주 중인 핸예츠가 피자 2판을 구매함.
- 그는 당시 30달러 정도 하는 파파존스 피자 2판을 당시 약 41달러의 가치가 매겨져 있던 1만 비트코인과 맞바꿔서 구매했음.

<p align="center">
<img src="/assets/img/blog/bitcoin_pizza.png">
</p>

- 영국 웨일스 뉴포트에 사는 제임스 하웰스(38)는 IT 기술자로 일하던 2009년 당시 재미삼아 비트코인을 채굴.
- 이후 컴퓨터를 교체하면서 비트코인 블록체인에 접속할 수 있는 하드 드라이브를 서랍에 따로 보관.
- 자신의 여자친구가 집을 청소하면서 비트코인 전자지갑이 보관된 하드 드라이브를 버림.

<p align="center">
<img src="/assets/img/blog/bitcoin_harddrive.png">
</p>

## 비트코인 시가총액

<p align="center">
<img src="/assets/img/blog/bitcoin_marketcap.png">
</p>

## 비트코인 얻는 방법

- 비트코인을 얻으려면 사용자가 직접 노드로 참여해 블록을 발견하여 채굴의 보상으로 비트코인을 얻을 수 있음.
- 비트코인 채굴은 비트코인 네트워크 운영에 기여하는 행위로 IT 관련 지식이 없는 사람이 쉽게 하기는 어려움. 따라서 수수료를 지불하고 실제 화폐를 비트코인으로 교환하는 방법이 현실적이고 쉬운 방법임.

<p align="center">
<img src="/assets/img/blog/bitcoin_get.png">
</p>

## 비트코인과 블록체인

<p align="center">
<img src="/assets/img/blog/bitcoin_blockchain.png">
</p>

> 초기 암호화폐 변종

> 거래 기록을 저장하는 분산원장

> 정부 제약이 없는 거래 속도의 단순화 및 개선

> 저비용, 안전하고 안전한 환경에서의 개인 간 거래 환경 제공

> 통화의 역할에 제한됨

> 변화에 대한 더 나은 적응력과 주요 기업의 더 많은 지원

> 통화 거래만 제공

> 통화뿐만 아니라 계약 및 재산권의 이전도 지원 가능

## 코인과 토큰의 차이

<p align="center">
<img src="/assets/img/blog/coin_token.png">
</p>

코인
- 코인은 물리적 화폐와 유사한 디지털 화폐입니다.
- **코인은 자체 블록체인과 프로토콜을 가지고 운영됩니다.**
- 코인은 주로 결제 수단으로 사용됩니다.

토큰
- 토큰은 특정 프로젝트에서 발행된 디지털 자산입니다.
- **토큰은 자체 블록체인에서 운영되지 않습니다. 예를 들어, 이더리움 네트워크를 사용합니다.**
- 토큰은 결제 및 디지털 계약에 사용됩니다.

## 코인의 종류

<p align="center">
<img src="/assets/img/blog/coin_type.png">
</p>

## 주요 섹터(유틸리티)별 코인

|분류|주요 코인|
|:--:|:-:|
|콘텐츠|세타(THETA), 코스모스(ATOM), 스팀(STEEM)|
|탈중앙 금융(Defi)|유니스왑(UNI), 체인링크(LINK), 에이브(AAVE)|
|분산 컴퓨팅|인터넷컴퓨터(ICP), 파일코인(FIL), 비트토렌스(BTT)|
|사물인터넷|아이오타(IOTA), 헬륨(Helium), 이오스트(IOST)|
|메타버스|디센트럴랜드(MANA), 더샌드박스(SAND)|
|보안 인증|온톨로지(ONT), 시빅(CVC), 월드코인(WLD)|
|자산 대출|메이커(MKR), 컴파운드(COMP)|
|물류|비체인(VET)|
|스포츠|칠리즈(CHZ)|
|헬스케어|메디블록(MED)|

## 알트코인(altcoins)

- 암호화폐 시장의 선구자인 비트코인 이외의 후발 암호화폐를 의미함. **Alternative coin**의 축약어.
- 알트코인은 법적인 화폐가 아니므로 ISO 4217처럼 표준화된 단축 코드가 없음. 괄호 안에 대문자로 표시한 것은 업계에서 흔히 사용되는 비공식적 코드.

<p align="center">
<img src="/assets/img/blog/altcoin.png">
</p>

## 스테이블코인(Stablecoins)

- 암호화폐 중 시가총액이 가장 큰 비트코인, 이더리움은 가격변동성이 매우 큼. 이는 교환의 매개로 쓰이는데 장애가 됨.
- 암호화폐를 교환의 매개체로 폭넓게 사용하기 위해서는 가격을 안정적으로 유지할 수 있는 스테이블코인의 필요성 대두.
- 스테이블코인은 가치가 항상 특정 화폐에 연결된 토큰으로 **<u><span style="color:red">법정화폐 담보방식, 암호화폐 담보, 알고리즘 방식</span></u>**으로 운영됨.

<p align="center">
<img src="/assets/img/blog/stablecoin.png">
</p>

## 스테이블코인(Stablecoins) 작동방식

<p align="center">
<img src="/assets/img/blog/stablecoin2.png">
</p>

## 비트코인 트랜잭션 - 송금거래의 예

- UTXO는 Unspent Transaction Output의 약자로서 '미사용 트랜잭션 출력값'으로 인터넷 계좌에서 잔고만 표시되는 계좌잔고 방식과 달리 UTXO는 마치 우리가 일상에서 휴대한 지갑속의 지폐와 유사하게 작동
- UTXO와 상대적인 개념으로 STXO(Spent Transaction Output)라는 용어도 사용한다. UTXO 상태에서 사용했다면 해당 UTXO는 STXO 상태로 변경

<p align="center">
<img src="/assets/img/blog/bitcoin_transaction2.png">
</p>

- 금융시스템에선 결제가 일어난 후 일정기간 동안 청산(settlement)과정을 거치고 그 과정 속에서 법적, 기술적으로 소유권을 증명함.
- 비트코인 네트워크에서 이루어지는 거래의 모호성을 대량의 컴퓨팅 파워를 이용한 채굴(Proof of Work)로 해결함.
- 즉 비트코인 네트워크에서 결제는 증명이 가능한 법적 증거로 청산되는 것이 아니라 전 세계에 분산된 익명의 사람들의 컴퓨팅 파워로 청산되는 것임.

<p align="center">
<img src="/assets/img/blog/bitcoin_transaction3.png">
</p>

- 비트코인 백서에서 Satoshi Nakamoto가 UTXO(Unspent transaction output)모델로 알려진 트랜젹션의 input과 output 개념을 소개.
- 암호화폐 7,000원을 송금한다면 지갑 주소 잔액 8,000원을 INPUT에 기록한 후 OUTPUT에는 B에게 7,000원을 송금하고, 1,000원은 자신에게 다시 되돌리는 요청을 함.

<p align="center">
<img src="/assets/img/blog/bitcoin_transaction4.png">
</p>

## 블록체인 기록 보관 방식의 차이점: 비트코인(UTXO) vs. 이더리움(계좌/잔고)

<p align="center">
<img src="/assets/img/blog/bitcoin_ethereum3.png">
</p>

## 지갑(Wallet)의

- 지갑(wallet)은 주소와 키(key) 관리, 잔액 관리, 거래 생성, 거래 확인, 거래 내역 관리 등의 기능을 수행함. 지갑은 모바일 앱과 웹 서비스로 블록체인과의 인터페이스 역할.
- 비트코인의 지갑은 공개 키 암호로 만든 키로 스마트폰 앱에서 사용하는 모바일 지갑, QR코드가 인쇄된 종이 지갑 등 그 종류가 다양함.

<p align="center">
<img src="/assets/img/blog/bitcoin_wallet.png">
</p>

## Hot Wallet(뜨거운 지갑)과 Cold Wallet(차가운 지갑)비교

<p align="center">
<img src="/assets/img/blog/hot_cold_wallet.png">
</p>

## Cold Wallet 평가

- 암호화폐 시장이 지속적으로 성장하면서 이와 관련한 하드웨어 지갑에 대한 관심도 커지고 있음.
- 중앙은행 디지털화폐, 네오뱅크 및 챌린저 뱅크 등장과 맞물린 암호화폐 거래소 확산, 예비 사용자들의 암호화폐 거래소 접근성 향상 등 여러 요인들이 콜드 스토리지 시장의 성장을 견인하고 있음.

<p align="center">
<img src="/assets/img/blog/cold_wallet.png">
</p>