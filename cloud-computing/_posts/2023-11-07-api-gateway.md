---
layout: post
title: API Gateway
description: |
  API Gateway
categories: 클라우드컴퓨팅
sitemap: false
hide_last_modified: true
---

# API Gateway

## API란?
- API(Application Programming Interface): 두 어플리케이션이 서로 대화할 수 있게 해주는 소프트웨어 중개자
- 식당의 테이블에 앉아서 주문할 메누 중에서 선택하고 있다고 상상
- 주방은 주문을 준비할 시스템의 일부
- 빠진 것은 주방에 주문을 전달하고 음식을 테이블로 돌려주는 중요한 연결고리. 이것이 API
- 요청 또는 주문을 받아 주방(즉, 시스템)에게 어떤 작업을 해야 하는지 전달하는 API. 그런 다음 웨이터는 반응을 다시 당신에게 전달.(음식)

## API Gateway
- API Gateway는 API를 관리하고 트래픽을 처리하기 위한 서비스 또는 도구
- 이는 클라이언트와 백엔드 서비스 간의 중간자 역활을 하며, 요청 및 응답을 처리하는 중간 계층으로 작동
- Amazon API Gateway는 API를 손쉽게 생성, 게시, 유지 관리, 모니터링 및 보호할 수 있는 완전관리형 서비스
- API는 애플리케이션이 백엔드 서비스의 데이터, 비즈니스 로직 또는 기능에 엑세스할 수 있는 "정문" 역할.
- API Gateway를 사용하면 실시간 양방향 통신 애플리케이션이 가능하도록 하는 RESTful API 밒 WebSocket API를 구축할 수 있음
- API Gateway는 컨테이너식 서버리스 워크로드 및 웹 애플리케이션을 지원함
- API Gateway는 트래픽 관리, CORS 지원, 권한 부여 및 액세스 제어, 제한, 모니터링 및 API 버전 관리 등 최대 수십만 개의 동시 API 호풀을 수신 및 처리하는데 관계된 모든 작업을 처리함.

## RESTful API와 WebSocket API
- RESTful API와 WebSocket API는 모두 애플리케이션 간에 데이터를 주고받는 방법을 제공하는 API. 그러나 두 API는 서로 다른 방식으로 작동하며, 각각 고유한 장점과 단점이 있음. 사용 용도에 따라 적합한 API를 선택해야 함

||RESTful API|WebSocket API|
|:---:|:---:|:---:|
|기반 프로토콜|HTTP|WebSocket|
|상태|상태 비저장<br>서버의 부하를 줄일 수 있음|상태 유지<br>이전에 주고받은 데이터를 사용하여 통신을 수행|
|통신 방식|비동기|동기|
|사용 용도|일반적인 데이터 통신|실시간 통신|
|사용 예|웹 사이트에서 사용자의 프로필 정보를 조회하는 API<br>쇼핑몰에서 상품의 정보를 조회하는 API<br>SNS에서 게시물을 조회하는 API|게임에서 다른 플레이어와 채팅하는 API<br>채팅 서비스에서 채팅방의 메시지를 실시간으로 수신하는 API<br>스트리밍 서비스에서 실시간으로 영상을 송출하는 API|

## Edge-optimized
- "Edge-optimized"는 Amazon API Gateway와 같은 클라우드 서비스에서 주로 사용되는 용어로, API 호출이 최초로 도달하는 위치와 관련된 설정을 나타냄
- 빈번하게 전 세계의 사용자들에게 API 호출이 이루어지는 경우, "Edge-optimized"설정은 전 세계 어디에서든 좋은 성능과 낮은 지연 시간을 제공하려는 경우에 유용
- Amazon API Gateway를 예로 들면, 사용자가 API Gateway를 생성할 때 API를 "Regional" 또는 "Edge-optimized"로 설정할 수 있음

- **CloudFront 배포**: API Gateway는 자동으로 Amazon CloudFront 배포를 생성. CloudFront는 AWS의 글로벌 콘텐츠 전송
- **가까운 위치에서의 응답**: 사용자의 API 요청은 가장 가까운 CloudFront 위치(edge location)로 라우팅되어 API 호출이 실제 서비스 위치까지 여행할 필요가 없어지므로 지연 시간이 줄어들게 됨
- **캐싱**: Edge locations에서는 요청에 대한 응답을 캐싱할 수 있어, 이후 동일한 요청이 들어올 때 더 빠른 응답을 제공할 수 있음
- **보안**: CloudFront는 DDoS 공격과 같은 일부 보안 위협으로부터의 추가적인 보호 기능을 제공

## Authorizers
- "Authorizers"는 Amazon API Gaeteway에서 주로 사용되는 용어로, 클라이언트 요청의 인증 및 권한 부여를 처리하는 역할을 함

- **요청 검증**: 클라이언트로부터의 API 요청이 인증 및 권한 부여를 거쳐야 할 때, Authorizer는 해당 요청을 검증함
- **토큰 기반 인증**: 많은 Authorizers는 Bearer Token, 예를 들면 JWT (Json Web Token)과 같은 토큰을 사용하여 클라이언트 인증을 수행함
- **캐싱**: API Gateway의 Authorizers는 인증 결정을 일정 시간 동안 캐싱할 수 있음. 이로 인해 반복된 요청에 대한 인증의 오버헤드를 줄일 수 있음
- **종류**:
  - API Gateway에서는 다양한 유형의 Autorizers를 제공함. Lambda Authorizer는 AWS Lambda 함수를 사용하여 인증 로직을 정의하는 방식. 클라이언트 요청이 오면 해당 Lambda 함수가 호출되어 인증 과정을 수행
  - Cognito User Pool Authorizer는 Amazon Cognito User Pools와 통합하여 사용자 관리 및 인증을 수행하는 방식
- **유연성**: 
  - 특히 Lambda Authorizer를 사용하면 매우 유연한 인증 및 권한 부여 로직을 구현할 수 있음
  - 예를 들어, 사용자의 역할에 따른 다른 API 액세스 권한을 부여하거나, 특정 IP 주소에서 오는 요청만을 허용하는 등의 로직을 구현할 수 있음

## Authorizers - Bearer Token
- Bearer Token은 인증에 사용되는 토큰 유형 중 하나임. "Bearer"는 소유자를 의미하는 단어로, 이 토큰을 가진 사람(소유자)이 인증된 사용자로 간주됨. 일반적으로 이 토큰은 API 호출의 Authorization 헤더에 포함되어 전송됨
- "Bearer Token"을 사용할 때 주의해야 할 점은, 이 토큰이 탈취되면 공격자가 토큰 소유자로서의 권한을 가질 수 있기때문에 토큰의 보안 및 관리가 매우 중요함.
- Bearer Token의 특징
  - **상태 없음(Stateless)**: 각 요청에 대한 인증은 토큰만을 기반으로 하며, 서버 측에서는 별도의 세션 상태를 유지할 필요가 없음
  - **자체 포함적(Self-contained)**: 토큰은 일반적으로 사용자 정보, 발행 시간, 만료 시간 등의 정보를 포함할 수 있음
  - **보안**: Bearer Token은 공개되면 누구나 해당 토큰을 사용하여 인증된 사용자처럼 행동할 수 있기 때문에 안전하게 전송하고 저장하는 것이 중요함
  - **일반적으로 JWT와 함께 사용**: 일반적으로 JWT(JSON Web Token)는 "Bearer Token"으로 사용되는 인증 토큰의 일반적인 형식

## Authorizers - AWS Cognito
- AWS Cognito는 Amazon Web Services(AWS)에서 제공하는 사용자 식별 및 데이터 동기화 서비스
- Cognito를 사용하면 웹 및 모바일 앱에서 안전하게 사용자를 관리하고 인증할 수 있음
- Cognito의 주요 기능과 특징
  - **연합 아이덴티티(Federated Identities)**: 
    - 게스트 사용자를 포함하여 다양한 식별 소스로부터 안전하게 AWS 리소스에 대한 액세스를 부여함
    - 연합 아이덴티티를 사용하면 사용자는 Amazon, Facebook, Google 등의 외부 서비스 공급자를 통해 AWS 리소스에 액세스할 수 있음
  - **데이터 동기화**: Cognito는 다른 AWS 서비스와 쉽게 통합될 수 있음. 예를 들어, 연합 아이덴티티를 사용하여 Amazon S3버킷이나 DynamoDB 테이블에 대한 액세스를 제어할 수 있음
  - **확정성**: 수 백만 명의 사용자를 처리할 수 있는 확장성을 제공하므로 큰 규모의 애플리케이션에서도 사용할 수 있음

