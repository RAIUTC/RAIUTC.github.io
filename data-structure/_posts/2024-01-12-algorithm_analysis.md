---
layout: post
title: Algorithm Analysis
description: |
  이번 글에서는 알고리즘 분석에 초점을 맞춰 성능을 평가하고 최적화하는 방법을 살펴봅니다. 
  시간 복잡도와 공간 복잡도의 중요성을 이해하고, 각 알고리즘의 효율성을 비교하는 기술을 소개합니다. 
  코드의 성능 향상을 위한 핵심 테크닉을 알고리즘 분석을 통해 익혀봅시다.
categories: 자료구조
sitemap: false
hide_last_modified: true
---
# Algorithm Analysis

## 알고리즘이란?

- **컴퓨터로 문제를 풀기 위한 단계적인 절차**
<p align="center">
<img src="/assets/img/blog/what_is_algorithm.png">
</p>
  - 자료구조의 연산(operation)은 알고리즘으로 표현됨
    - 특정 연산의 성능 분석 시 알고리즘 성능 분석을 통해 분석

- **주로 쓰는 알고리즘 기술 방법**
  - 영어/한국어와 같은 자연어
  - 의사코드(pseudo-code)
  - 특정한 프로그래밍 언어(e.g., C++/Java 등)

- **예시 알고리즘**
  - 배열에서 최대값 찾기 알고리즘

- **자연어로 표현한 알고리즘**
  - 사람이 이해하기 쉬움
    - <span style="color:blue">알고리즘의 핵심 아이디어를 기술하는데 활용</span>
  - 단어들이 정확하게 정의되지 않으면 의미 전달이 모호해질 우려가 있음

- **예시) 배열에서 최대값 찾기 알고리즘**
  - Step1. 배열 A의 0번째 요소를 변수 tmpMax에 복사
  - Step2. 배열 A의 다음 요소들을 차례대로 비교하면서 더 크면 tmpMax에 복사
  - Step3. 배열 A의 모든 요소를 비교했으면 tmpMax를 반환

- **의사코드(Pseudo-code)로 표현한 알고리즘**
  - 알고리즘의 고수준 기술 방법
    - 알고리즘의 핵심적인 내용/원리에만 집중하고 구현적인 디테일은 감춤
    - 자연어보다 <span style="color:blue">더 구조적인</span> 표현 방법
    - 프로그래밍 언어보다는 <span style="color:red">덜 구체적인</span> 표현 방법
  - 알고리즘 기술에 가장 많이 사용 (Python 스타일로 표현)
<p align="center">
<img src="/assets/img/blog/pseudo_code_example.png">
</p>

- **특정 프로그래밍 언어로 표현한 알고리즘**
  - 알고리즘의 가장 정확한 기술 가능
  - 그러나, 실제 구현시 많은 구체적인 사항들이 알고리즘의 핵심을 이해하는데 방해가 될 수 있음
<p align="center">
<img src="/assets//img//blog/algorithm_expressed_with_cpp.png">
</p>

## 알고리즘의 효율이란?

- **하나의 문제는 여러가지 방법(알고리즘)으로 해결될 수 있음**
  - 문제: n을 n번 더하기
<p align="center">
<img src="/assets/img/blog/algorithm_efficiency.png">
</p>
  - <span style="color:red">어떤 알고리즘을 사용해야 하는 걸까?</span>
    - 동일한 결과를 낸다면, 가장 빠르고 가벼운 알고리즘이 제일 좋음
  - 그렇다면, 어떤 알고리즘이 좋은지 어떻게 판별할 수 있을까?
    - <span style="color:red">A1:</span> 컴퓨터에서 각각의 알고리즘을 실제로 수행한 후 수행 시간 측정해보자
    - <span style="color:blue">A2:</span> Algorithm C 가 O(1)의 시간과 공간을 사용하므로 Algorithm C를 써야함

## Time & Space Costs

- **어떠한 자료구조/알고리즘을 쓰는지에 따라 성능에 차이**
  - Time: 수 초 또는 수 일의 시간이 걸려 수행
  - Space: 작은 또는 매우 많은 메모리를 사용

- **알고리즘의 시간/공간 비용의 정리**
  - 알고리즘이 사용하는 자원(time/space)의 양

- **알고리즘의 효율성 측정 = 시간/공간 비용 측정!**
  - 실험적(empirical)방법과 이론적(theoretical)방법이 있음

|Resource|Time|Space|
| :---: | :---: | :---: |
|Empirical|Wall-clock time|Memory usage|
|Theoretical|Time complexity|Space complexity|

## 효율성 측정 방법

- **실험적 측정**
  - 예) 프로그램의 수행 시간을 측정(입력 &rarr; 출력)
  - 예) 최대로 사용한 메모리 양 측정(VmPeak 검사)
<p align="center">
<img src="/assets/img/blog/empirical_cost.png">
</p>
  - <span style="color:blue">장점</span>: 쉽게 측정 가능 & 직관적으로 파악
  - <span style="color:red">단점</span>
    - 수행 환경(HW, OS, PL, ...)과 구현 방법에 따라 측정 결과값이 달라짐
    - 입력의 크기가 커질 때 성능이 어떻게 변화하는지 파악하기 힘듦
      - 각각의 입력에 대해 실험 해야함

- **이론적 측정**
  - 시간/공간 복잡도 분석(complexity analysis)
    - <span style="color:blue">시간 복잡도</span>: 기본 연산들의 횟수를 기반으로 추정 (예, 덧셈/곱셈 횟수)
    - <span style="color:red">공간 복잡도</span>: 저장되는 데이터의 양을 기반으로 추정 (예, 배열에 저장되는 아이템의 수)
  - 일반적으로 알고리즘 복잡도는 입력 데이터 크기 n과 관련 (함수로 표현)
    - T(n): time complexity (function) for given n input data
    - S(n): space complexity (function) for given n input data
      - 보통, 주로 쓰이는 자료구조들의 공간 복잡도는 입력 데이터 크기에 비례
  - 자료구조의 각 연산의 실행 시간을 분석하는 것이 중요하므로 시간 복잡도에 대해 주로 논의

## 기본 연산

- **기본 연산은 그 수행 시간이 입력의 크기와 상관 없이 실행되는 연산을 의미**
  - Add/subtraction (+ or -) & division/multiplication (* or /)
    - For a + b or a * b, its # of operations is constant (i.e., 1)
    > 덧셈(+)이나 곱셈(*)의 경우, 연산 횟수는 일정 (즉, 1회)
  - Assignment (= or &larr;)
    - For c = 10, its # of operations is constant (i.e., 1)
    - For c &larr; a + b, its # of operations is constant (i.e., 2)
  - Comparison (< or >)
    - For c > b, its # of operations is constant (i.e., 1)

## 복잡도 분석의 예

- **문제: n을 n번 더하기**
<p align="center">
<img src="/assets/img/blog/complexity_analysis_ex.png">
</p>
  - 각 알고리즘이 수행되는 기본 연산의 횟수 계산
    - 간결함을 위해 for loop내에서 쓰이는 연산(예, range)은 생략

||Algorithm A|Algorithm B|Algorithm C|
| :---: | :---: | :---: | :---: |
|Assignments|n+1|$$ n^2 + 1 $$|1|
|Additions|n|$$ n^2 $$||
|Multiplication|||1|
|---|---|---|---|
|Total|2n+1|$$ 2n^2 + 1 $$|2|

## Performance Tendency (성능 경향)

- **입력 크기 n에 따른 각 알고리즘의 성능 경향**
<p align="center">
<img src="/assets/img/blog/performence_tendency.png">
</p>

## Best, Average & Worst Cases

- **복잡도는 <span style="color:blue">입력 집합</span>에 따라 다르게 될 수 있음**
  - 최선의 경우(best case): 수행 시간이 가장 빠르게 되는 입력 집합
    - 일반적인 성능으로서 의미가 없는 경우가 많음
  - 평균적인 경우(average case): 평균적인 수행 시간을 띄는 입력 집합
    - 가장 정확한 성능 지표를 띄지만 일반적으로 계산하기 어려움
  - <span style="color:red">최악의 경우(worst case):</span> 수행 시간이 가장 느리게 되는 입력집합
    - 모든 입력에 대한 성능 보장 가능
    > 적어도 <span style="color:blue">최악의 경우에 대해 복잡도 분석을 수행</span>해야 함

## 예시) 순차탐색의 최선 & 최악의 경우

- **순차 탐색 문제**
<p align="center">
<img src="/assets/img/blog/sequential_search.png">
</p>
  - 최선의 경우: T(n) = 1
    - 예: key가 A의 처음에 있는 경우
  - 최악의 경우: T(n) = n
    - 예: key가 A의 마지막에 있는/아예 없는 경우

## 순차탐색의 평균의 경우

  - 평균의 경우: T(n) = (n+1)/2
    - 모든 가능한 경우에 대한 기대값; key가 임의의 위치에 있을 확률이 균등하게 $$ \frac{1}{n} $$이라 가정

    $$
    \frac{1}{n} * 1 + \frac{1}{n} * 2 + ... + \frac{1}{n} * i + ... + \frac{1}{n} * n = \frac{1}{n}\sum_{i=1}^{n} i = \frac{1}{n} * \frac{n(n+1)}{2} = \frac{n+1}{2}
    $$

    <span style="color:blue">$$\frac{1}{n}$$: P(the key is at index i)</span>

    <span style="color:red">$$i$$: # of operations searching for index i</span>

## Motivation

- **다음 중 더 빠른 알고리즘은 무엇일까?**
  - Algorithm A: # of operations in $$2^n$$, i.e., $$T_{A}(n) = 2^n$$
  - Algorithm B: # of operations in $$n^{10}$$, i.e., $$T_{B}(n) = n^{10}$$

||n=10|n=60|n=100|
| :---: | :---: | :---: | :---: |
|Algorithm A|$$2^{10} = 1024$$|$$2^{60} \approx 1.15 * 10^{18}$$|$$2^{100} \approx 10^{30}$$|
|Algorithm B|$$10^{10}$$|$$60^{10} \approx 6.05 * 10^{17}$$|$$100^{10} \approx 10^{20}$$|
|Faster?|Algorithm A|Algorithm B|Algorithm B|

  - 입력 크기 n이 점점 커지게 되면 "<span style="color:red">결국에는</span>" Algorithm B가 더 빠름

- **점근적 분석(Asympotic analysis)**
  - 입력의 크기가 <span style="color:blue">매우 커지게 되었을 때</span> 알고리즘의 성능을 파악하고자 함

## 점근적 복잡도 분석

- **입력 크기 n이 굉장히 커질 때 복잡도 함수 T(n)이 어떻게 변하는지 분석하는 것**
  - <span style="color:blue">Asympotic</span>: n이 $$\infty$$에 점점 다가가는(점근)것을 의미 (i.e., $$n \to \infty$$)
  - n이 $$\infty$$에 점근할 때, 함수가 변화하는 모습을 함수의 <span style="color:red;">점근적 행동(asympotic/tail behavior)</span>라고 함

<p align="center">
<img src="/assets/img/blog/asympotic_complexity_analysis.png">
</p>

## 왜 $$\infty$$를 고려해야 할까?

- **여러 항으로 이루어진 복잡도의 점근적 행동은 어떻게 될까?**
  - Example: $$T(n) = n^2 + n + 1$$

    - n = 1 $$T(n) = 1 + 1 + 1 = 3$$ (33.3% for $$n^2$$)
    - n = 10 $$T(n) = 100 + 10 + 1 = 111$$ (90% for $$n^2$$)
    - n = 100 $$T(n) = 10000 + 100 + 1 = 10101$$ (99% for $$n^2$$)
    - n = 1000 $$T(n) = 1000000 + 1000 + 1 = 1001001$$ (99.9% for $$n^2$$)
  - <span style="color:blue">즉, n이 커질 수록 ($$n \to \infty$$) T(n)은 $$n^2$$에 비례하게 됨</span>
    - 일반적으로 다항 함수에서는 최고차 항에 비례하여 이를 <span style="color:red">dominant factor</span>라고 함

- **$$5n^2, 10m^2, 100n^2$$과 같이 계수가 다른 경우는?**
  - 계수가 상수라면 n이 무한하게 커질 때 계수보다는 항의 영향력이 압도적
  - 결국에는 $$n^2$$의 tail behavior와 같은 양상을 띔

## Asymptotic Bounds

- **임의의 복잡도 함수의 점근적 행동을 간단하게 표현하는 방법**
  - Big-O (O, upper bound)

<p align="center">
<img src="/assets/img/blog/big_o.png">
</p>

## Big-O Notation

- **Definition**

<p align="center">
<img src="/assets/img/blog/big_o_definition.png">
</p>

  - 충분히 큰 입력 크기 n에 대해, <span style="color:blue">cf(n)</span>보다 작거나 같은 함수들의 집합

<p align="center">
<img src="/assets/img/blog/big_o_definition2.png">
</p>

- **Interpretation of T(n) = O(f(n))**
  - 알고리즘은 <span style="color:blue">최선</span>/<span style="color:green">평균</span>/<span style="color:red">최악</span>의 경우에 O(f(n))의 시간 복잡도를 가진다
  - [해석] 입력의 크기가 충분히 클 때, 해당 알고리즘은 <span style="color:blue">최선</span>/<span style="color:green">평균</span>/<span style="color:red">최악</span>의 경우에 대해 <span style="color:blue"><u>항상 cf(n)보다 적은 연산으로 수행</u></span>된다

- **문제 풀 때 유의점**
  - 정의를 사용한 증명을 할 때 c와 n0의 구체적인 값을 제시해야 함
  - c와 n0은 양수(0이 되면 안됨)

<p align="center">
<img src="/assets/img/blog/big_o_caution.png">
</p>

## Big-O Examples

- **Claim) T(n) = $$ 5n^2 $$ = O($$ n^2 $$)**
  - Proof) 직관적으로 c=6 & n0=1으로 선택하고 정의에 맞는지 보임
    - n >= n0 = 1인 모든 n에 대해, T(n) = $$ 5n^2 $$ <= $$ 6n^2 $$이 성립하므로 T(n) = O($$ n^2 $$)이다
      - 여기에서 c=6과 n0=1는 여러 가능한 정답 중 하나임(c=7&n0=1해도 성립함)

- **Claim) T(n) = 4 = O(1)**
  - Proof) c=10 & n0=1이라고 하면, n >= n0 = 1인 모든 n에 대해, T(n) = 4 <= c*1 = 10 성립
    - 이러한 경우에 <span style="color:red">상수 시간 (복잡도)</span>을 가진다고 함

- **Claim) T(n) = $$ 3n^2 + 100 = O(n^2) $$**
  - Proof1)
    - 먼저, c=13이라고 가정하면, $$ 3n^2 + 100 <= 13n^2 $$ &larr;&rarr; $$ 100 <= 10n^2 $$ &larr;&rarr; $$ 10 <= n^2 $$
    - 즉, $$ n >= \sqrt{10} \approx 3.162$$ 이면 위 부등식이 만족 &rarr; n0=4로 선택
    - 따라서, n >= 4에 대해 $$ 3n^2 + 100 <= 13n^2 $$이 성립
  - Proof2)
    - $$ 3n^2 + 100 <= 3n^2 + 100n^2 = 103n^2 $$ &rarr; c=103 & n0=1로 선택
    - $$ 3n^2 + 100 <= 103n^2 $$ &larr;&rarr; $$ 100 <= 100n^2 $$ &larr;&rarr; $$ 1 <= n^2 $$
    - 즉, $$ n >= 1 $$이면 위 부등식이 만족 &rarr; n0=1로 선택

- **Claim) T(n) = 5n+3 = O($$n^2$$)**
  - c=1 라고 하면, n>=n0 = 6에 대해, 5n+3 <= $$ n^2 $$이 성립
- 위와 같이, Big-O 기호는 <span style="color:blue">엄격한(strict)</span>또는 <span style="color:red">느슨한(loose)</span> 상한(upper bound)이 될 수 있음
  - 어떤 기준 (base) 함수 f(n)가 사용되었느냐에 따라 다름
  - Example: T(n) = 5n + 3
    - T(n) = {<span style="color:blue">O($$ n $$)</span>, <span style="color:red">O($$ n^2 $$), O($$ n^3 $$), ...</span>}
  - 어떤 문제에서 "가능한 tight하게 Big-O로 추천하시오"라고 하면, <span style="color:blue">T(n) = O(n)</span>라고 써야 함

- **아래와 같은 함수들의 점근적 행동을 간단하게 표현할 수 있을까?**
  - $$ T(n) = n^2 $$
  - $$ T(n) = n^2 + n + 1 $$
  - $$ T(n) = 3n^2 - 2n + 100 $$
  - $$ T(n) = 100n^2 $$

- **위 시간 복잡도 모두 $$O(n^2)$$으로 표현**
  - n이 무한히 커지면 계수나 추가적인 항이 다르더라도 <span style="color:red">결국 $$n^2$$과 같은 점근적 행동을 보임 </span>
  - 즉, 위 함수 모두 <span style="color:blue">점근적으로 같은 성능을 가진다고 분류</span>할 수 있음!

## 알고리즘의 점근적 복잡도 분석

- **Big-O 기호를 사용한 점근적 복잡도 분석 절차**
  - Step1. <span style="color:red">최악의 경우</span>에 대해 <span style="color:blue">시간/공간 복잡도 분석</span>
    - 일반적으로 최악의 경우에 대해 추정하거나 상황에 따라 최선/평균에 대해서도 분석함
  - Step2. 위 복잡도에 대해 <span style="color:blue">Big-O 기호로 가능한 tight하게 표현</span>
    - 최악의 경우에 대한 성능의 상한이기 때문에 알고리즘의 성능이 이보다 나빠지지 않을 것이라고 기대할 수 있음

- **예시) 순차탐색 알고리즘**
  - Step1. 최악의 경우의 시간 복잡도는 T(n) = n
    - 최악의 경우: 찾고자 하는 key가 배열 A의 마지막에 있는/아예 없는 경우
  - Step2. Big-O로 T(n) = O(n)
    - 즉, 순차탐색 알고리즘은 <span style="color:blue">최악의 경우 O(n)의 시간 복잡도</span>를 가짐

- **로그 복잡도 예시**
<p align="center">
<img src="/assets/img/blog/log_complexity.png">
</p>

  - 시간 복잡도 T(n) = Ck
    - 각 반복에서 상수번(C)의 연산이 수행되므로 결과적으로 반복횟수 k에 의해 결정

|# loops|1|2|3|...|k|<span style="color:white; background-color:red;">k+1</span>|
| :---: | :---: | :---: | :---: | :---: | :---: | :---: |
|i|$$ 1 = 2^0 $$|$$ 2 = 2^1 $$|$$ 4 = 2^2 $$|...|$$ 2^{k-1} $$|<span style="color:white; background-color:red;">$$ 2^k $$</span>|

  - $$ 2^k >= n$$인 상황에서 반복이 종료 됨
    - $$ k >= log_2 n $$의 범위에서 k = $$ log_2 n $$이면 반복이 충분히 종료된다고 볼 수 있음
  - $$ T(n) = Ck = Clog_2 n <= Clog_2 n + C = O(log_2 n) $$

## What You Need To Know

- **알고리즘의 기술 방법**
  - [추상적]<span style="color:blue">자연어</span>-<span style="color:red">의사코드</span>-특정 프로그래밍 언어[구체적]

- **알고리즘의 효율성**
  - 알고리즘의 효율이란? 효율을 측정하는 방법과 각 방법의 장단점은?

- **복잡도 분석**
  - 입력의 크기를 고려해야 하는 이유는? 복잡도 추정 방법은?
  - 왜 최악의 경우를 고려해야 하는가?

- **점근적 복잡도 분석**
  - 입력의 크기가 매우 커지게 되었을 때, 알고리즘의 성능을 간단하고 일관된 방법(Big-O 기호)으로 표현하는 방법은?