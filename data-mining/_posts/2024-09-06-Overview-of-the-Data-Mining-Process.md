---
layout: post
title: Overview of the Data Mining Process
description: |
  - Introduction
  - Core Ideas in Data Mining
  - The Steps in Data Mining
  - Preliminary Steps
  - Predictive Power and Overfitting
  - Building a Predictive Model
categories: Data_Mining
sitemap: false
hide_last_modified: true
---
# Overview of the Data Mining Process

## Introduction
- **<span style='background-color: #fff5b1'>데이터 모델링 과정</span>**

<p align="center">
<img src="/assets/img/blog/data-mining/OverviewOfTheDataMiningProcess/DataModelingProcess.png">
</p>

위 그림은 Data Modeling Process를 나타낸 것이다.
- 목적 정의
- 데이터 획득
- 데이터 탐색 및 정제
- DM 작업 결정
- DM 방법 선택
- 방법 적용, 최종 모델 선택
- 성능 평가
- 배포

Data Modeling Process는 이와 같이 이루어진다.

- Business Analytics 핵심 요소
    - 예측 분석(Predictive Analytics)
        - 분류(Classification) / 예측(Prediction)
    - 데이터 마이닝에서 많이 쓰이는 데이터베이스 기법
        - OLAP(Online Analytical Processing)과 SQL(Structured Query Language)
        - 예) 신용카드 고객 중에서 특정 지역에 살고, 연간지출액이 2만 달러를 넘고, 자기 주택을 소유하고 있고, 적어도 95%는 결제일을 맞춘 고객을 찾는 문제

## Core Ideas in Data Mining
- **<span style='background-color: #fff5b1'>Classification</span>**
    - 데이터 분석의 가장 많이 다루는 문제
    - 데이터를 집단으로 구분하기 위함
    - "응답" or "응답하지 않음" / "정상" or "사기" / "정상" or "고장" / "회복" or "진행중" or "사망"

<p align="center">
<img src="/assets/img/blog/data-mining/OverviewOfTheDataMiningProcess/Classification.png">
</p>

- **<span style='background-color: #fff5b1'>Prediction</span>**
    - 예측하고자 하는 변수가 숫자로 표현된 연속형 변수일 경우 예측 문제로 분류 <br>
     &#8251; 예측하고자 하는 변수가 범주형인 경우 분류 문제

<p align="center">
<img src="/assets/img/blog/data-mining/OverviewOfTheDataMiningProcess/Prediction.png">
</p>

- **Association Rules and Recommendation Systems**
    - 대량의 고객거래 데이터베이스는 구매항목들 간의 연관성, 즉 어떤 항목이 어떤 항목과 관련 되는지에 대한 분석
    - Collaborative Filtering: 개개인의 포괄적인 과거 구매정보와 다른 사람들의 구매정보를 이용하여 개개인의 구매성향을 예측하는 추천 시스템

<p align="center">
<img src="/assets/img/blog/data-mining/OverviewOfTheDataMiningProcess/Association Rules and Recommendation Systems.png">
</p>

- **Cluster Analysis(as Data reduction method)**
    - 비지도학습으로 데이터를 동질적인 군집들로 세분화
    - 측정값들로 구성된 레코드로부터 측정값들이 유사한 레코드의 모임 또는 군집을 형성하기 위해 사용

<p align="center">
<img src="/assets/img/blog/data-mining/OverviewOfTheDataMiningProcess/Cluster Analysis.png">
</p>

- **Dimension Reduction**
    - 변수의 개수를 줄이는 과정
    - 지도 학습 전에 수행되며, 예측 성능을 향상시키고 해석의 용이성 증대 목적

- **Data Exploration**
    - 데이터의 전반에 관한 이해와 이상치 탐지 목적
    - 수치적 혹은 시각적으로 데이터를 요약하는 방법론 사용

- **Data Visualization**
    - 수치형 변수: 히스토그램(histogram)과 상자그림(boxplot)을 이용하여, 변수값의 분포를 파악하고 극단치(outliers)를 찾음
    - 범주형 변수: 차트(charts)와 원형 차트(pie charts)를 이용. 변수 간의 가능한 관계들, 관계유형 그리고 극단치를 찾기 위해 한 쌍의 수치형 변수에 대한 산점도(scatter plots)을 조사

<p align="center">
<img src="/assets/img/blog/data-mining/OverviewOfTheDataMiningProcess/Histogram_and_Boxplot.png">
</p>

- **Supervised Learning**
    - 분류 또는 예측하고자 하는 변수가 존재할 경우 이를 labeled data(결과값)로 놓고 예측변수와의 관계를 통해 모델링
    - 학습 데이터를 이용하여 예측변수(종속변수)와 결과변수 간의 관계를 학습, 훈련함
    - 학습 데이터로부터 모델이 구축되면 결과를 알고 있는 검증 데이터를 사용하여 모델의 성능을 평가하고 다른 방법론과 비교
    - 다수의 모델을 비교하고자 할 경우, 평가 데이터를 통해 성능을 비교, 평가함
    - 최종적으로 검증이 끝난 모델은 예측변수의 값을 모르는 미래의 데이터 예측에 사용
    - 예) 단순 선형 회귀분석, 판별 분석, 역전파 신경망

- **Unsupervised Learning**
    - 예측 또는 분류를 위해 필요한 출력변수가 없는 경우에 사용되는 알고리즘
    - 예) 연관 규칙, 차원 축소 기법, 군집 분석 등