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

### A Perceptron

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

#### Example: $$ \theta $$ = 0.5

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/perceptron_3.png">
</p>

 - Possible <span style="color:red">$$w_1$$</span> and <span style="color:red">$$w_2$$</span>:
    - (0.2, 0.35)
    - (0.4, 0.2)
    - ...

> 위와 같이 AND Gate를 구현하기 위해서는 두 입력과 가중치의 곱의 합이 0.5보다 크면 1을 출력하도록 설정하면 된다.

#### Another Example:

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/perceptron_xor_example.png">
</p>

- Possible <span style="color:red">$$ w1 $$</span> and <span style="color:red">$$ w2 $$</span>:
> XOR Gate를 구현하기 위한 가중치가 존재하는가?

- XOR Gate는 single-layer perceptron으로 구현할 수 없다.

### Multiple Perceptrons

- A solution is using multiple perceptrons!
> XOR Gate를 구현하기 위해서는 여러 층을 쌓아 해결할 수 있다!

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/multiple_perceptrons.png">
</p>

- Softmax classifier is a special case of Perceptron!
> 소프트맥스 분류기는 퍼셉트론의 특수한 경우이다!

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/special_case_of_perceptron_softmax_classifier.png">
</p>

### Neural Network with a Single Layer

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/neural_network_with_a_single_layer.png">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/neural_network_with_a_single_layer_2.png">
</p>

$$ x \in \mathbb{R}^d $$
> x(input)은 d차원 벡터이다.

$$ W \in \mathbb{R}^{c\times d} $$
> W(가중치)는 c와 d의 곱의 차원을 가진 벡터이다.

$$ s \in \mathbb{R}^c $$
> s는 c차원 벡터이다.

### Multilayer Perceptron (MLP)

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/multilayer_perceptron.png">
</p>

$$ x \in \mathbb{R}^d $$ 
> x(input)은 d차원 벡터이다.

$$ W_1 \in \mathbb{R}^{h\times d} $$
> W_1(가중치)는 h와 d의 곱의 차원을 가진 벡터이다.

$$ W_2 \in \mathbb{R}^{c\times h} $$ 
> W_2(가중치)는 c와 h의 곱의 차원을 가진 벡터이다.

$$ s \in \mathbb{R}^c $$
> s는 c차원 벡터이다.

- Single-layer perceptron Equation: $$ f(x) = Wx $$

- Multilayer perceptron Equation: $$ f(x) = W_2 \cdot(W_1 \cdot x) $$
> 여기서 W_1과 W_2의 순서가 달라도 결과는 같게 된다. (결합법칙) 이를 이용해 W_1과 W_2를 먼저 곱한다면 single_layer perceptron으로도 표현할 수 있다.

<span style="color:red">**과연 multilayer perceptron이 single-layer perceptron과 같은가?**</span>

- 이는 우리가 역치함수(즉, Activation function)을 생각하지 않았기 때문이다.

- Multi-linear layers are still linear.
    - <span style="color:red">$$ W = W_2 \cdot W_1 $$</span>
> 역치함수가 없다면 여러 층을 쌓아도 여전히 선형적이다.

- How can we add non-linearity?
    - Activation functions!

$$ f(x) = a2(W_2 \cdot a1(W_1 \cdot x)) $$

> 여기서 a1과 a2는 Activation function이다. Activation function이 존재해야 여러 층을 쌓는 이유가 있으므로 존재가 중요하다.

## Activation Functions

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/activation_functions.png">
</p>

## An Example of Neural Network

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/an_example_of_neural_network.png">
</p>

## Computing Gradients

**What do we need for (Stochastic) Gradient Descent?**
- Gradient of the classification loss w.r.t **each parameter(weight)**
> 각 매개변수(가중치)에 대한 분류 손실의 기울기

$$ \frac{\partial{L}}{\partial{W_1}}, \frac{\partial{L}}{\partial{W_2}} $$

- Each gradient indicates **how much that particular weights contributed** to the incorrect prediction.
> 각각의 기울기는 해당 가중치가 잘못된 예측에 얼마나 기여했는지를 나타낸다.

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/computing_gradients.png">
</p>

$$ L = (\hat{y} - y)^2 $$

$$ \hat{y} = W_2 \cdot \sigma(W_1 \cdot x) $$

$$ \frac{\partial{L}}{\partial{W_2}} = \frac{\partial{L}}{\partial{\hat{y}}} \cdot \frac{\partial{\hat{y}}}{\partial{W_2}} = 2(\hat{y} - y)\cdot \sigma(W_1 \cdot x)$$

$$ \frac{\partial{L}}{\partial{W_1}} = \frac{\partial{L}}{\partial{\hat{y}}} \cdot \frac{\partial{\hat{y}}}{\partial{h}} \cdot \frac{\partial{h}}{\partial{W_1}} = 2(\hat{y} - y) \cdot W_2 \cdot h \cdot(1-h) \cdot x $$

> $$h = \sigma(W_1 \cdot x)$$

## Implementation: 2-layer MLP

~~~python
import numpy as np
from numpy.random import randn

# Network Definition
n, d, h, c = 64, 1000, 100, 10
x, y = randn(n,d), randn(n,c)
w1, w2 = randn(d, h), randn(h, c)
learning_rate = 1e-4

for t in range(1000):

    # Forward Pass
    h = 1 / (1 + np.exp(-x.dot(w1)))
    y_pred = h.dot(w2)
    loss = np.square(y_pred - y).sum()
    print(t, loss)

    # Calculate the analytical gradients
    grad_y_pred = 2.0 * (y_pred - y)
    grad_w2 = h.T.dot(grad_y_pred)
    grad_h = grad_y_pred.dot(w2.T)
    grad_w1 = x.T.dot(grad_h * h * (1 - h))

    # Gradient descent
    w1 -= learning_rate * grad_w1
    w2 -= learning_rate * grad_w2
~~~
<p align="center">
<a href="https://github.com/RAIUTC/ML-DL-Study/blob/main/two_layer_multiple_layer_perceptrons.ipynb" target="_blank">소스코드(Source Code)</a>
</p>
