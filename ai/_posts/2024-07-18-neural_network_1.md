---
layout: post
title: Neural Networks & Backpropagation
description: |
  Explore the fundamentals of neural networks, including the perceptron model, multi-layer perceptrons, activation functions, and backpropagation. Understand how these elements work together to enable machine learning and artificial intelligence.
  > 인공신경망의 기초인 퍼셉트론 모델, 다층 퍼셉트론, 활성화 함수, 역전파 등을 탐색합니다. 이러한 요소들이 어떻게 함께 작동하여 기계 학습과 인공지능을 가능하게 하는지 이해합니다.
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

## Computing Gradients

Even more complex neural nets ...
> 더 복잡한 신경망 ...

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/computing_gradients_2.png">
</p>

- 위와 같이 더욱 복잡한 신경망들의 Gradients를 직접 계산하기는 어렵다.

## Computational Graph

- 우리가 만든 모델을 수식으로 표현할 수 있듯이 그래프로도 표현 가능한데 이를 **Computational Graph**라고 한다.

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/computational_graph.png">
</p>

## Backpropagation Example

$$ f(x, y, z) = (x + y)z $$

For example, suppose the input is

x = -2, y = 5, z = -4

### <span style="color:green">Forward Pass </span>

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/forward_pass.png">
</p>

### <span style="color:red">Backpropagation</span>

Partial derivative of $$ f $$ w.r.t. $$ z $$ is given by $$ \frac{\partial{f}}{\partial{z}} = \frac{\partial{qz}}{\partial{z}} = q $$
> $$ f $$의 $$ z $$에 대한 편미분은 $$ \frac{\partial{f}}{\partial{z}} = \frac{\partial{qz}}{\partial{z}} = q $$

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/backpropagation.png">
</p>

## Chain Rule

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/chain_rule.png">
</p>

## Another Example: Logistic Regression

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/another_example_logistic_regression.png">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/another_example_logistic_regression_2.png">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/another_example_logistic_regression_3.png">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/another_example_logistic_regression_4.png">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/another_example_logistic_regression_5.png">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/another_example_logistic_regression_6.png">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/another_example_logistic_regression_7.png">
</p>

- Backpropagation을 하는 이유? &rarr; **gradient를 구해 W들이 얼마나 틀렸는지 Update하기 위해**
- Logistic Regression에서 구하고 싶었던 <span style="color:red">Gradients</span>: <span style="color:red">$$ w_0, w_1, b $$ = -0.20, -0.40, 0.20</span>

## Patterns in Gradient Flow

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/patterns_in_gradient_flow.png">
</p>

## Gradient Implementation

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/gradient_implementation.png">
</p>

- Forward pass

~~~python
def f(w0, x0, w1, x1, b):
    s0 = w0 * x0
    s1 = w1 * x1
    s2 = s0 + s1
    s3 = s2 + b
    return 1.0 / (1.0 + np.exp(-s3)) # *-1 -> exp -> +1 -> 1/x
~~~

- Gradient computation

~~~python
grad_f = 1.0
grad_s3 = grad_f * (1 - f) * f
grad_b = grad_s3
grad_s2 = grad_s3
grad_s0 = grad_s2
grad_s1 = grad_s2
grad_w1 = grad_s1 * x1
grad_x1 = grad_s1 * w1
grad_w0 = grad_s0 * x0
grad_x0 = grad_s0 * w0
~~~

<p align="center">
<a href="https://github.com/RAIUTC/ML-DL-Study/blob/main/gradient_implementation.ipynb" target="_blank">소스코드(Source Code)</a>
</p>

## Vector Derivatives
> 벡터 미분

- **Scalar** to **scalar**: if $$ x $$ is slightly changes, how much will $$ y $$ change?
> **스칼라**에서 **스칼라**로: $$ x $$가 약간 변경되면 $$ y $$가 얼마나 변경되나?

$$ x \in \mathbb{R}^d, y \in \mathbb{R}, \frac{\partial{y}}{\partial{x}} \in \mathbb{R}$$

- **Vector** to **scalar**: if each element $$ x_i $$ in $$ x $$ slightly changes, how much will $$ y $$ change?
> **벡터**에서 **스칼라**로: $$ x $$의 각 요소 $$ x_i $$가 약간 변경되면 $$ y $$가 얼마나 변경되나?

$$ x \in \mathbb{R}^n, y \in \mathbb{R}, \frac{\partial{y}}{\partial{x}} \in \mathbb{R}^n, (\frac{\partial{y}}{\partial{x}})_i = \frac{\partial{y}}{\partial{x_i}}$$

- **Vector** to **vector**: if each element $$ x_i $$, in $$ x $$ slightly changes, how much will each element $$ y_i $$ in $$ y $$ change?
> **벡터**에서 **벡터**로: $$ x $$의 각 요소 $$ x_i $$가 약간 변경되면 $$ y $$의 각 요소 $$ y_i $$가 얼마나 변경되나?

$$ x \in \mathbb{R}^n, y \in \mathbb{R}^m, \frac{\partial{y}}{\partial{x}} \in \mathbb{R}^{m \times n}, (\frac{\partial{y}}{\partial{x}})_{ij} = \frac{\partial{y_i}}{\partial{x_j}}$$

## Backpropagation with Vectors

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/backpropagation_with_vectors.png">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/backpropagation_with_vectors_2.png">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/backpropagation_with_vectors_3.png">
</p>

### Example: Backpropagation with Vectors

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/backpropagation_with_vectors_example.png">
</p>

## Backpropagation with Matrices

<p align="center">
<img src="/assets/img/blog/ai/2024-07-18-neural_network_1/backpropagation_with_matrices.png">
</p>

## Remind Questions

### 1. Linear Classifier로 학습할 수 없는 데이터셋 같은 경우는 어떠한 방법으로 학습할 수 있을까?(두 가지 방법)

- 1. non linear한 decision boundary를 가진 데이터를 linear decision boundary를 가질 수 있도록 (e.g.g, high dimensional space로 mapping(SVM &rarr; Kernel)) 변환해 linearly separate하도록 만드는 것
- 2. **Perceptron을 여러 층으로 쌓는것. linear layer를 여러 층으로 쌓으면 여전히 linear하지만 non-linearity를 부여하는 활성화 함수(activation function(e.g.g., ReLU, Sigmoid))를 적용해 해결.**

### 2. Backpropagation을 할 때 각 노드에서 어떠한 일이 일어나는가?

- Forward pass가 진행되어 예측값을 계산하고, 이를 가지고 Loss를 계산해 맨 뒤부터 Loss값을 계산한 Upstream Gradient를 계산한다. 그 값을 받아 Local Gradient(Local Function 자체를 미분했을 때 나오는 값)가 곱해지며 Backward pass를 진행한다. 각 노드별로 input, output은 여러개일 수 있다.

### 3-1. input으로 20차원의 값을 받고 Output으로 10차원의 값이 나가는 node가 있다. 이 노드의 Upstream Gradient는 몇 차원일까?

- **10차원. Output의 차원과 같다.**

### 3-2. Local Gradient는?

- 20 * 10 = 200차원. **(input dim * output dim)**

### 3-3. DownStram Gradient는?

- **20차원. Input의 차원과 같다.**