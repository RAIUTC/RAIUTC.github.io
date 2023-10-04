---
layout: post
title: 신경망의 수학적 구성 요소
description: |
  1 신경망의 첫  만남 <br>
  2 신경망을 위한 데이터 표현 <br>
  3 신경망의 톱니바퀴: 텐서 연산 <br>
  4 신경망의 엔진: 그레이디언트 기반 최적화 <br>
  5 첫 번째 예제 다시 살펴보기 <br>
  6 요약 <br>
sitemap: false
hide_last_modified: true
---
## 2장 신경망의 수학적 구성 요소
**이 글은 [케라스 창시자에게 배우는 딥러닝]책을 학습하며 내용을 정리한 글입니다.**

## 2.1 신경망의 첫 만남
**첫 번째 예제: 흑백 손글씨 숫자 이미지(28px*28px)를 10개의 범주(0~9까지)로 분류하는 것**

- MNIST 데이터셋 사용
- 6만 개의 훈련 이미지(train data), 1만 개의 테스트 이미지(test data)로 구성

![400x200](/assets/img/blog/mnist_dataset.jpg "MNIST 샘플 이미지")

> 용어정리

> **클래스(class)**: 분류(Classification) 문제의 **범주(category)**<br>
> **샘플(sample)**: 데이터 포인트<br>
> **레이블(label)**: 특정 샘플의 클래스

### 케라스에서 MNIST 데이터셋 적재하기
- MNIST 데이터셋은 넘파이(NumPy)배열 형태로 케라스에 이미 포함되어있다.
~~~python
from tensorflow.keras.datasets import mnist
(train_images, train_labels), (test_images, test_labels) = mnist.load_data()
~~~
- **훈련 세트(training set)**: train_images, train_labels
- **테스트 세트(test set)**: test_images, test_labels

* 훈련 데이터

![600x400](/assets/img/blog/mnist_train_dataset_shape.png "훈련 데이터")

* 테스트 데이터

![600x400](/assets/img/blog/mnist_test_dataset_shape.png "테스트 데이터")

### 작업 순서
1. train_images와 train_labels를 네트워크에 주입
2. 네트워크는 이미지에 알맞는 레이블을 연관시키도록 학습
3. 마지막으로 네트워크를 통해 test_images에 대한 예측 수행
4. 이 예측이 test_labels와 맞는지 확인

### 신경망 구조
~~~python
from tensorflow import keras
from tensorflow.keras import layers

model = keras.Sequential([
    layers.Dense(512, activation="relu"),
    layers.Dense(10, activation="softmax")
])
~~~
- 신경망의 핵심 구성 요소는 **층(layer)**이다
- 층은 데이터를 위한 필터(filter)로 생각할 수 있다
- 어떤 데이터가 들어가면 더 유용한 형태로 출력한다
- 층은 주어진 문제에 더 의미 있는 **표현(representation)**을 입력된 데이터로부터 추출한다
- 대부분의 딥러닝은 간단한 층을 연결하여 구성되어 있고, 점진적으로 데이터를 정제하는 형태를 띠고 있다
- 이 예에서는 조밀하게 연결된 (또는 **완전 연결(fully connected)**된) 신경망 층인 Dense 층 2개가 연속되어 있다
- 두 번째(즉, 마지막) 층은 10개의 확률 점수가 들어 있는 배열(모두 더하면 1)을 반환하는 **소프트맥스(softmax)** 분류 층이다. 각 점수는 숫자 이미지가 10개의 숫자 클래스 중 하나에 속할 확률이다.

- 신경망이 훈련 준비를 마치기 위해서 컴파일 단계에 포함될 세 가지가 더 필요
  - **옵티마이저(optimizer)**: 성능을 향상시키기 위해 입력된 데이터를 기반으로 모델을 업데이트하는 매커니즘
  - **손실 함수(loss function)**: 훈련 데이터에서 모델의 성능을 측정하는 방법으로 예측 값과 레이블 값 사이의 오차를 측정하는 방법
  - **훈련과 테스트 과정을 모니터링할 지표**: 여기선 정확도(정확히 분류된 이미지의 비율)

### 컴파일 단계
~~~python
model.compile(optimizer="rmsprop", # 옵티마이저: 성능을 향상시키기 위해 입력된 데이터를 기반으로 모델을 업데이트하는 매커니즘
              loss="sparse_categorical_crossentropy", # 훈련 데이터에서 모델의 성능을 측정하는 방법
              metrics=["accuracy"]) # 정확도(정확히 분류된 이미지의 비율
~~~

### 이미지 데이터 준비하기
- 훈련을 시작하기 전에 데이터를 모델에 맞는 크기로 바꾸고 모든 값을 0과 1 사이로 스케일을 조정(인공지능 모델은 숫자값에 민감하게 반응하기 때문)
- 앞서 우리의 훈련 이미지는 [0,255] 사이의 값인 unit8 타입의 (60000,28,28)크기를 가진 배열
- 이 데이터를 0과 1 사이의 값을 가지는 float32 타입의 (60000,28 * 28) 크기인 배열로 바꿈
~~~python
train_images = train_images.reshape((60000, 28 * 28))
train_images = train_images.astype("float32") / 255
test_images = test_images.reshape((10000, 28 * 28))
test_images = test_images.astype("float32") / 255
~~~

### 모델 훈련하기
- 케라스에서는 모델의 fit() 메서드를 호출하여 훈련 데이터에 모델을 학습
~~~python
model.fit(train_images, train_labels, epochs=5, batch_size=128)
~~~
![600x400](/assets/img/blog/mnist_train_model.png "모델 훈련하기")

- 훈련하는 동안 출력되는 2개의 정보: 모델의 손실, 정확도
- 훈련 데이터에 대해 0.988(98.8%)의 정확도를 금방 달성

### 모델을 사용하여 예측 만들기
~~~python
test_digits = test_images[0:10]
predictions = model.predict(test_digits)
predictions[0]
~~~
![400x200](/assets/img/blog/mnist_predict_result.png "모델을 사용하여 만든 예측")

- 출력된 배열에 있는 숫자는 숫자 이미지 test_digits[0]이 해당 클래스에 속할 확률에 해당
- test_digits[0] 숫자는 인덱스 7에서 가장 높은 확률 값(0.9989869으로 거의 1)을 얻었음
- 모델의 예측 결과는 7이 됨

![400x300](/assets/img/blog/mnist_predict_result2.png "모델을 사용하여 만든 예측2")

- 테스트 데이터의 레이블과 맞는지 확인

![200x100](/assets/img/blog/test_data.png "test data label")

### 새로운 데이터에서 모델 평가하기
~~~python
test_loss, test_acc = model.evaluate(test_images, test_labels)
print(f"테스트 정확도: {test_acc}")
~~~
![600x100](/assets/img/blog/evaluate_model_in_test_dataset.png "새로운 데이터에서 모델 평가하기")

- 테스트 세트의 정확도는 97.9%
- 훈련 세트 정확도(98.8%)보다는 약간 낮음
- 흔련 정확도와 테스트 정확도 사이의 차이는 **과대적합(overfitting)** 때문임
- 이는 머신 러닝 모델이 훈련 데이터보다 새로운 데이터에서 성능이 낮아지는 경향을 말한다

## 2.2 신경망을 위한 데이터 표현

- 이전 예제에서 **텐서(tensor)**라고 부르는 다차원 넘파이 배열에 데이터를 저장하는 것부터 시작했다
- 최근의 모든 머신 러닝 시스템은 일반적으로 텐서를 기본 데이터 구조로 사용한다
- 텐서는 임의의 차원 개수를 가지는 행렬의 일반화된 모습(텐서에서는 **차원(dimension)**을 종종 **축(axis)**이라고 부름)

### 스칼라(랭크-0 텐서)

- 하나의 숫자만 담고 있는 텐서를 **스칼라(scalar)**라고 부름
- ndim 속성을 사용하면 넘파이 배열의 축 개수를 확인할 수 있다
- 스칼라 텐서의 축 개수는 0(ndim == 0)
- 텐서의 축 개수를 **랭크(rank)**라고도 부름

![100x150](/assets/img/blog/scalar.png "스칼라 텐서")

### 벡터(랭크-1 텐서)

- 숫자의 배열을 **벡터(vector)**라고 부름
- 벡터는 딱 하나의 축을 가짐

![100x150](/assets/img/blog/vector.png "벡터")

- 이 벡터는 5개의 원소를 가지고 있으므로 5차원 벡터라고 부름
- 5D 벡터와 5D 텐서를 혼동하지 말자!
- **차원 수(dimensionality)**는 특정 축을 따라 놓인 원소의 개수(5D 벡터와 같은 경우)이거나 텐서의 축 개수(5D 텐서와 같은 경우)를 의미하므로 가끔 혼동하기 쉬움

### 행렬(랭크-2 텐서)

- 벡터의 배열은 **행렬(matrix)**이라고 부름
- 행렬에는 2개의 축이 있음(보통 **행(row)**과 **열(row)**이라고 부름)
- 행렬은 숫자가 채워진 사각 격자라고 생각할 수 있음

![200x100](/assets/img/blog/matrix.png "행렬")

- 첫 번째 축에 놓여 있는 원소를 **행**, 두 번째 축에 놓여 있는 원소를 **열**이라고 부름

### 랭크-3 텐서와 더 높은 랭크의 텐서

- 이런 행렬들을 하나의 새로운 배열로 합치면 숫자가 채워진 직육면체 형태로 해석할 수 있는 랭크-3텐서(또는 3D 텐서)가 만들어짐

![300x150](/assets/img/blog/rank_3_tensor.png "랭크-3 텐서")

- 랭크-3 텐서들을 하나의 배열로 합치면 랭크-4 텐서를 만드는 식으로 이어짐

### 핵심 속성

- **축의 개수(랭크)**: 예를 들어 랭크-3 텐서에서는 3개의 축이 있고, 행렬에서는 2개의 축이 있음. 넘파이나 텐서플로 같은 파이썬 라이브러리에서는 ndim 속성에 저장되어 있음
- **크기(shape)**: 텐서의 각 축을 따라 얼마나 많은 차원이 있는지를 나타낸 파이썬의 튜플(tuple). 예를 들어 앞에 나온 행렬의 크기는 (3,5)이고 랭크-3 텐서의 크기는 (3,3,5) 벡터의 크기는 (5,)처럼 1개의 원소로 이루어진 튜플. 스칼라는 ()처럼 크기가 없음
- **데이터 타입(파이썬 라이브러리에서는 보통 dtype이라고 부름)**: 텐서에 포함된 데이터의 타입. 예를 들어 텐서의 타입은 float16, float32, float64, unit8 등이 될 수 있음. 텐서플로에서는 string 텐서를 사용하기도 함

- MNIST 예제에서 사용했던 데이터 다시 들여다보기

![400x200](/assets/img/blog/mnist_dataset_shape.png)