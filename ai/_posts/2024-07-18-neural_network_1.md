---
layout: post
title: Neural Networks & Backpropagation
description: |
  
categories: 인공지능(AI)
sitemap: false
hide_last_modified: true
---

# Neural Networks & Backpropagation

## Perceptron

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/perceptron.png">
</p>

 - 다수의 값을 입력받아 하나의 값으로 출력하는 알고리즘이다. 

 - 생물학적으로 뉴런은 다수의 신호를 받아 하나의 신호로 출력한다. 이러한 생물학적 뉴런을 모델링한 것이 퍼셉트론이다.

## A Perceptron

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/perceptron_1.png">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/perceptron_2.png">
</p>

 - Takes input values.
 - Each of them is multiplied with a weight, and summed.
 - If the result is above some threshold $$ \theta $$, it fires (outputs 1).
 - Otherwise, outputs 0.

 > 입력 값을 받는다.<br>각각의 입력 값은 가중치와 곱해진 후 합산된다.<br> 
 결과가 임계값 $$ \theta $$ 보다 크면 활성화된다(1을 출력).<br> 그렇지 않으면 0을 출력한다.

### Example: $$ \theta $$ = 0.5

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/perceptron_3.png">
</p>

 - Possible <span style="color:red">$$w_1$$</span> and <span style="color:red">$$w_2$$</span>:
    - (0.2, 0.35)
    - (0.4, 0.2)
    - ...

> 위와 같이 AND Gate를 구현하기 위해서는 두 입력과 가중치의 곱의 합이 0.5보다 크면 1을 출력하도록 설정하면 된다.