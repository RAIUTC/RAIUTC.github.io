---
layout: post
title: Key Management - KDC & CA
description: |
  Key Management-(KDC & CA)에 대한 글입니다.
categories: 컴퓨터보안(Security)
sitemap: false
hide_last_modified: true
---

# Key Management - KDC & CA

## Key Management
- <span style="color:red">Symmetric key cryptography</span>
  - <span style="color:red">How to determine a shared secret key</span>
  > 공유 비밀 키를 결정하는 방법
- <span style="color:red">Public key cryptography</span>
  - <span style="color:red">How to obtain other's true public key</span>
  > 다른 사람의 진정한 공개 키를 얻는 방법
- <span style="color:red">KDC for symmetric key, CA for public key</span>

## Session Key
- Session: 회기, 입회시간
- 통신 session이 시작될 때 생성되서 종료될 때 폐기되는 동적 대칭키
- 통신 session마다 다른 키를 사용하면 안전

## 다중사용자가 세션키사용 할 경우
- 2명의 사용자 간에 1개의 비밀키 사용
- 3명의 사용자 간에 3개의 비밀키 사용
  - 사용자 A, B, C에 대해 비밀키 KAB, KBC, KCA를 필요

![100x50](/assets/img/blog/session_key_3_people.drawio.png "2명의 사용자 간에 1개의 비밀키 사용")

- 사용자 1명 추가시 3개의 비밀키가 추가로 필요
  - 추가 사용자 D에 대해 비밀키 KAD, KBD, KCD 추가

![100x50](/assets/img/blog/session_key_4_people.drawio.png "사용자 1명 추가시 3개의 비밀키가 추가로 필요")

![100x50](/assets/img/blog/session_key_n_people.drawio.png)

- n system need n(n-1)/2 pairs of secret keys
- Each system remembers n-1 keys
- If a new system comes in n new key are generated
- If a system leaves, n-1 keys are no removed

<span style="color:red"> **대칭키 유지 및 관리 부하!** </span>

## KDC (Key distribution center)
- 중앙의 신뢰할 수 있는 키관리, 분배 책임주체
- 사용자들은 KDC 등록신청하면, KDC가 각 사용자들과 비밀키를 공유
- Each user communicate with KDC using this key

![100x50](/assets/img/blog/KDC.png "KDC")

## Operation

<span style="color:red">Alice와 Bob은 KDC와의 통신을 위한 KA-KDC, KB-KDC를 알고 있다.</span><br>
<span style="color:red">Alice는 KDC와 통신하여 세션키 R1과 KB-KDC(A, R1)을 얻는다</span><br>
<span style="color:red">Alice는 Bob에게 KB-KDC(A, R1)을 보내고, Bob은 R1을 추출해낸다</span>

![100x50](/assets/img/blog/KDC_operation.png "KDC operation")

## KDC 장단점
- KDC의 단점
  - 단일 실패 지점(SPoF, Single Point of Failure)
    - KDC가 고장나면 전혀 서비스를 할 수 없음
    - 해결책: 미러 서버(mirror server) 가동
      - 서버와 미러 간의 일관성(consistency)문제 발생 가능
  - KDC가 공격되면 모든 비밀키가 노출될 수 있음
  - KDC의 신뢰성이 매우 중요함
  - KDC에 대한 병복현상(bottle neck) 발생
- KDC의 장점
  - 비밀키 방식은 비교적 속도가 빠름
  - 서버를 사용하지 않는 경우보다 키 관리를 쉽게 해줌

## <span style="color:blue">Hierarchical Key Control</span>

- 단일 KDC는 대규모 네트워크에서 비효율적
- KDC를 계층화
  - local KDC
    - single LAN or building
    - 같은 domain에서의 통신시 키 분배
  - global KDC
    - 다른 domain간의 통신시 키 선택
  - KDC의 손상시 지역에 한정

### Issue: Every pair of KDC needs a shared key &rarr; KDC hierarchy
