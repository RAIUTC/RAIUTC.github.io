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

### 다섯 번째 이미지 출력하기

- MNIST 다섯 번째 샘플을 맷플롯립(Matplotlib) 라이브러리를 사용해서 확인

~~~python
import matplotlib.pyplot as plt

digit = train_images[4]
plt.imshow(digit, cmap=plt.cm.binary)
plt.show()
~~~

![200x200](/assets/img/blog/mnist_5th_data.png "데이터셋에 있는 다섯 번째 샘플")

### 넘파이로 텐서 조작하기

~~~python
digit = train_images[4]
~~~

- 위와 같은 형식으로 첫 번째 축을 따라 특정 숫자 이미지를 선택
- **슬라이싱(slicing)**: 배열에 있는 특정 원소들을 선택하는 것

~~~python
my_slice = train_images[10:100]       #11번째 28*28 이미지부터 100번째 이미지까지를 my_slice 변수에 할당하라.
my_slice.shape
~~~

- 위 코드는 11번째에서 100번째까지 숫자를 선택하여 (90,28,28)크기의 배열을 만듦

~~~python
my_slice = train_images[10:100, :, :]
my_slice.shape

my_slice = train_images[10:100, 0:28, 0:28]
my_slice.shape
~~~

- 동일한 코드이고 :(콜론)은 전체 인덱스를 선택한다

~~~python
my_slice = train_images[:, 14:, 14:]
~~~

- 위 코드와 같이 배열의 축을 따라 특정 인덱스 사이도 선택할 수 있음
- 위 코드는 이미지의 오른쪽 아래 14*14 픽셀을 선택

~~~python
my_slice = train_images[:, 7:-7, 7:-7]
~~~

- 위 코드와 같이 음수 인덱스도 사용할 수 있음
- 음수는 현재 축의 **끝에서** 상대적인 위치를 나타냄
- 위 코드는 정중앙에 위치한 14*14 픽셀을 선택

### 배치 데이터

- 일반적으로 딥러닝에서 사용하는 모든 데이터 텐서의 첫 번째 축(0번째 축)은 **샘플 축(sample axis)**
- 딥러닝 모델은 한 번에 전체 데이터셋을 처리하지 않고, 대신 데이터를 작은 배치(batch)로 나눈다

~~~python
batch = train_images[:128]
~~~

- MNIST 숫자 데이터에서 크기가 128인 배치 하나

~~~python
batch = train_images[128:256]
~~~

- 그 다음 배치

~~~python
n = 3
batch = train_images[128 * n:128 * (n + 1)]
~~~

- n번째 배치
- 배치 데이터를 다룰 때 첫 번째 축(0번 축)을 **배치 축(batch axis)**또는 **배치 차원(batch dimension)**이라고 한다

### 텐서의 실제 사례

- 딥레닝에 사용할 데이터는 대부분 다음 중 하나에 속할 것
  - **벡터 데이터**: (samples, features) 크기의 랭크-2 텐서. 각 샘플은 수치 속성(특성(features))으로 구성된 벡터
  - **시계열 데이터 또는 시퀀스(sequence) 데이터**: (samples, timesteps, features) 크기의 랭크-3 텐서. 각 샘플은 특성 벡터의 (길이가 timesteps인) 시퀀스
  - **이미지**: (sample, height, width, channels) 또는 (samples, channels, height, width)크기의 랭크 -4 텐서. 각 샘플은 픽셀의 2D 격자고 각 픽셀은 수치 값(채널(channel))의 벡터
  - **동영상**: (samples, frames, height, width, channels) 또는 (samples, frames, channels, height, width)크기의 랭크-5 텐서. 각 샘플은 이미지의 (길이가 frames인) 시퀀스

#### 벡터 데이터

- 배치 데이터는 랭크-2 텐서로 인코딩
- 첫 번째 축은 **샘플 축**이고, 두 번째 축은 **특성 축(feature axis)**

#### 시계열 데이터 또는 시퀀스 데이터

- 데이터에서 시간이 (또는 연속된 순서가) 중요할 때는 시간 축을 포함하여 랭크-3 텐서로 저장

![400x200](/assets/img/blog/sequence_data.jpg "랭크-3 시계열 데이터 텐서")

#### 이미지 데이터

- 전형적으로 높이, 너비, 컬러 채널의 3차원으로 이루어짐
- 256*256 크기의 흑백 이미지에 대한 128개의 배치는 (128, 256, 256, 1) 크기의 텐서에 저장될 수 있음
- 컬러 이미지에 대한 128개의 배치라면 (128, 256, 256, 3) 크기의 텐서에 저장될 수 있음

![200x200](/assets/img/blog/image_tensor.jpg "이미지 데이터 텐서(채널 우선 표기)")

- 이미지 텐서의 크기를 지정하는 방식은 **채널 마지막(channel-last)**(텐서플로에서 사용하는) 방식과 많이 사용하지 않는 **채널 우선(channel-first)** 방식
- 케라스 API는 두 형식을 모두 지원

#### 비디오 데이터

- 현실에서 랭크-5 텐서가 필요한 몇 안 되는 데이터 중 하나
- 하나의 비디오는 프레임의 연속이고 각 프레임은 하나의 컬러 이미지
- (samples, frames, height, width, color_depth)의 랭크-5 텐서로 저장될 수 있음

## 2.3 신경망의 톱니바퀴: 텐서 연산

- 컴퓨터 프로그램을 이진수의 입력을 처리하는 몇 개의 이항 연산(AND, OR, NOR 등)으로 표현할 수 있는 것처럼, 심층 신경망이 학습한 모든 변환을 수치 텐서에 적용하는 몇 종류의 **텐서 연산(tensor operation)**으로 나타낼 수 있음

~~~python
keras.layers.Dense(512, activation="relu")
~~~

- 위처럼 전 예제에서 Dense 층을 쌓아서 모델을 만들었음
- 이 층은 행렬을 입력으로 받고 입력 텐서의 새로운 표현인 또 다른 행렬을 반환하는 함수처럼 해석할 수 있음
- 구체적으로 이 함수는 다음과 같다.

output = relu(dot(W, input) + b)    (W는 행렬, b는 벡터)

- 여기엔 3개의 텐서 연산이 존재
  - 입력 텐서와 텐서 W 사이의 점곱(dot)
  - 점곱으로 만들어진 행렬과 벡터 b 사이의 덧셈(+)
  - relu(렐루) 연산. reul(x) = max(x, 0) (0보다 작으면 0을 반환)

### 원소별 연산

- relu 함수와 덧셈은 **원소별 연산(element-wise operation)**
- 이 연산은 텐서에 있는 각 원소에 독립적으로 사용

~~~python
def naive_relu(x):
    assert len(x.shape) == 2
    x = x.copy()
    for i in range(x.shape[0]):
        for j in range(x.shape[1]):
            x[i, j] = max(x[i, j], 0)
    return x
~~~

- 파이썬으로 단순한 원소별 연산을 구현한다면 위처럼 for 반복문을 사용

~~~python
def naive_add(x, y):
    assert len(x.shape) == 2
    assert x.shape == y.shape
    x = x.copy()
    for i in range(x.shape[0]):
        for j in range(x.shape[1]):
            x[i, j] += y[i, j]
    return x
~~~

- 덧셈도 동일, 같은 원리로 원소별 곱셈, 뺄셈 등을 할 수 있음
- 넘파이는 **BLAS(Basic Linear Algebra Subprogram)**를 통해 연산들을 처리할 수 있음
~~~python
import numpy as np

z = x + y # 원소별 덧셈
z = np.maximum(z, 0.) # 원소별 렐루 함수
~~~

- 넘파이는 위 코드를 엄청난 속도로 처리한다

~~~python
import time

x = np.random.random((20, 100))
y = np.random.random((20, 100))

t0 = time.time()
for _ in range(1000):
    z = x + y
    z = np.maximum(z, 0.)
print("걸린 시간: {0:.2f} s".format(time.time() - t0))
~~~

~~~python
t0 = time.time()
for _ in range(1000):
    z = naive_add(x, y)
    z = naive_relu(z)
print("걸린 시간: {0:.2f} s".format(time.time() - t0))
~~~

![400x600](/assets/img/blog/numpy_running_time_compare.png)

- 실행속도 결과를 비교하면 엄청난 속도차이가 난다
- 이와 비슷하게 텐서플로 코드를 GPU에서 실행할 때 GPU칩 구조를 최대로 활용할 수 있는 완전히 벡터화된 CUDA 구현을 통해 원소별(element-wise) 연산이 실행

### 브로드캐스팅

- 단순한 덧셈 구현인 native_add는 동일한 크기의 랭크-2텐서만 지원
- 실행 가능하다면 작은 텐서가 큰 텐서의 크기에 맞추어 **브로드캐스팅(broadcasting)**

#### 브로드캐스팅의 두 단계

1. 큰 텐서의 ndim에 맞도록 작은 텐서에 (브로드캐스팅 축이라고 부르는) 축이 추가
2. 작은 텐서가 새 축을 따라서 큰 텐서의 크기에 맞도록 반복

~~~python
import numpy as np

X = np.random.random((32, 10)) # 크기가 (32,10)인 랜덤한 행렬
y = np.random.random((10,)) # 크기가 (10, )인 랜덤한 벡터
~~~
- X의 크기는 (32,10), y의 크기는 (10,)

~~~python
y = np.expand_dims(y, axis=0) # 이제 y의 크기는 (1,10)
~~~
- y에 비어 있는 첫 번째 축을 추가하여 크기를 (1,10)으로 만듦

~~~python
Y = np.concatenate([y] * 32, axis=0) # 축 0을 따라 y를 32번 반복하여 크기가 (32,10)인 Y를 얻는다
~~~
- y를 추가된 축에 32번 반복하여 추가해 크기가 (32,10)인 Y를 생성
- 이제 X와 Y의 크기가 같아 더할 수 있다.

- 새로운 텐서가 만들어지면 매우 비효율적이므로 어떤 랭크-2 텐서도 만들어지지 않고 반복된 연산은 완전히 가상적으로 메모리 수준이 아니라 알고리즘 수준에서 일어남

### 텐서 곱셈

- **텐서 곱셈(tensor product)** 또는 점곱(dot product)
- 넘파이에서 텐서 곱셈은 np.dot 함수를 사용하여 수행
~~~python
x = np.random.random((32,))
y = np.random.random((32,))
z = np.dot(x, y)
~~~
~~~python
def naive_vector_dot(x, y):
    assert len(x.shape) == 1  # x와 y는 넘파이 벡터
    assert len(y.shape) == 1
    assert x.shape[0] == y.shape[0]
    z = 0.
    for i in range(x.shape[0]):
        z += x[i] * y[i]
    return z
~~~
- 두 벡터의 점곱은 스칼라가 되므로 원소 개수가 같은 벡터끼리 점곱이 가능

- 행렬과 벡터 사이의 점곱
~~~python
def naive_matrix_vector_dot(x, y):
    assert len(x.shape) == 2  # x는 넘파이 행렬
    assert len(y.shape) == 1  # y는 넘파이 벡터
    assert x.shape[1] == y.shape[0] # x의 두 번째 차원이 y에 첫 번째 차원과 같아야 한다
    z = np.zeros(x.shape[0])        # 이 연산은 x의 행과 같은 크기의 0이 채워진 벡터를 만든다.
    for i in range(x.shape[0]):
        for j in range(x.shape[1]):
            z[i] += x[i, j] * y[j]
    return z
~~~
- y와 x의 행 사이에서 점곱이 일어나므로 벡터가 반환

- 두 텐서 중 하나라도 ndim이 1보다 크면 dot 연산에 교환 법칙이 성립되지 않음
- 다시 말해 dot(x,y)와 dot(y,x)가 같지 않음

~~~python
def naive_matrix_dot(x, y):
    assert len(x.shape) == 2  # x와 y는 넘파이 행렬
    assert len(y.shape) == 2
    assert x.shape[1] == y.shape[0]   # x의 두 번째 차원이 y의 첫 번째 차원과 같아야 한다
    z = np.zeros((x.shape[0], y.shape[1]))  # 0이 채워진 특정 크기의 벡터를 만듦
    for i in range(x.shape[0]):     # x의 행을 반복
        for j in range(y.shape[1]): # y의 열을 반복
            row_x = x[i, :]
            column_y = y[:, j]
            z[i, j] = naive_vector_dot(row_x, column_y)
    return z
~~~
- x.shape[1] == y.shape[0]일 때 두 행렬 x와 y의 점곱이 성립
- (x.shape[0], y.shape[1])크기의 행렬이 됨

![300x200](/assets/img/blog/matrix_dot.jpg "행렬 점곱 다이어그램")

- x의 행 벡터와 y의 열 벡터가 같은 크기여야 하므로 자동으로 x의 너비는 y의 높이와 동일해야 함
- 동일한 규칙을 따르면 다음과 같이 고차원 텐서 간의 점곱 가능
  - (a,b,c,d) ∙ (d,) -> (a,b,c)
  - (a,b,c,d) ∙ (d,e) -> (a,b,c,e)

### 텐서 크기 변환

- 모델에 주입할 숫자 데이터를 전처리할 때 사용
~~~python
train_images = train_images.reshape((60000, 28 * 28))
~~~

![100x200](/assets/img/blog/tensor_shape_transform.png)

- 자주 사용하는 특별한 크기 변환은 **전치(transposition)**
- 행과 열을 바꾸는 것을 의미

![200x100](/assets/img/blog/matrix_transpose.png)

### 텐서 연산의 기하학적 해석

A = [0.5, 1]
![100x100](/assets/img/blog/a_2d_space.jpg "화살표로 나타낸 2D 공간에 있는 포인트")

A = [0.5, 1] + B = [1, 0.25]

- 벡터 A에 벡터 B를 더하는 것은 점 A를 새로운 위치로 복사하는 동작
- 원래 점 A에서 새로운 위치까지 거리와 방향은 벡터 B에 의해 결정
- 동일한 벡터 덧셈을 평면에 있는 점 집합(하나의 객체)에 적용하면 새로운 위치에서 전체 객체의 복사본을 만들게 됨

![100x100](/assets/img/blog/add_vector.jpg "두 벡터의 덧셈에 대한 기하학적 해석")

- 일반적으로 이동(translation), 회전(rotation), 크기 변경(scaling), 기울이기(skewing) 등과 같은 기본적인 기하학적 연산은 텐서 연산으로 표현 가능

- **이동**: 한 점에 벡터를 더하면 고정된 방향으로 고정된 양만큰 이 점을 이동. 점 집합(2D 객체와 같이)에 적용하면 이를 '이동(translation)'이라고 부름

![200x100](/assets/img/blog/translation.jpg "벡터 덧셈으로 2D 이동")

- **회전**: 각도 theta만큼 2D 벡터를 반시계 방향 회전한 결과는 2x2 행렬 R = [[cos(theta), -sin(theta), cos(theta)]]와 점곱하여 얻을 수 있음

![200x100](/assets/img/blog/rotation.jpg "점곱으로 (반시계 방향) 2D 회전")

- **크기 변경**: 2x2 행렬 S = [[horizontal_factor, 0], [0, vertical_factor]]와 점곱하여 수직과 수평 방향으로 크기를 변경시킨 이미지를 얻을 수 있음

![200x100](/assets/img/blog/scailing.jpg "점곱으로 2D 크기 변경")

- **선형 변환(linear transform)**: 임의의 행렬과 점곱하면 선형 변환이 수행. 크기 변경과 회전은 선형 변환에 해당

- **아핀 변환(affine transform)**: 아핀 변환은 (어떤 행렬과 점곱하여 얻는)선형 변환과 (벡터를 더해 얻는)이동의 조합. Dense층에서 수행되는 y = W ∙ x + b 계산도 아핀 변환

![200x100](/assets/img/blog/affine_transform.jpg "평면의 아핀 변환")

- **relu 활성화 함수를 사용하는 Dense 층**: Affine2(affine1(x)) = W2 ∙ (W1 ∙ x + b1) + b2 = (W2 ∙ W1) ∙ x + (W2 ∙ b1 + b2) 이는 선형 변환 부분이 행렬 W2 ∙ W1이고, 이동 부분이 벡터 W2 ∙ b1 + b2인 하나의 아핀 변환. 결국 활성화 함수 없이 Dense 층으로만 구성된 다층 신경망은 하나의 Dense 층과 같음. 이것이 relu 같은 활성화 함수가 필요한 이유. 활성화 함수 덕분에 Dense 층을 중첩하여 매우 복잡하고 비선형적인 기하학적 변형을 구현하여 심층 신경망에 매우 풍부한 가설 공간을 제공할 수 있음

![200x100](/assets/img/blog/relu_affine_transform.jpg "relu 활성화 함수를 적용한 아핀 변환")

## 2.4 신경망의 엔진: 그레이디언트 기반 최적화

~~~python
output = relu(dot(W, input) + b)
~~~
- 이 식에서 텐서 W와 b는 층의 속성처럼 볼 수 있음
- 이러한 속성을 **가중치(Weight)** 또는 **훈련되는 파라미터(trainable parameter)**라고 부름
- 이런 가중치에는 훈련 데이터를 모델에 노출시켜 학습된 정보가 있다

- 초기에는 가중치 행렬이 작은 난수로 채워져 있음(**무작위 초기화(random initialization)** 단계라고 부름). 이 단계에서는 의미 없는 표현이 만들어짐
- 그다음에는 피드백 신호에 기초하여 가중치가 점진적으로 조정
- 이런 점진적인 조정 또는 **훈련(training)**이 머신 러닝 학습의 핵심

- **훈련 반복 루프(training loop)** 단계 (다음 단계를 반복)
  1. 훈련 샘플 x와 이에 상응하는 타깃 y_true의 배치를 추출
  2. x를 사용하여 모델을 실행하고(정방향 패스(forward pass) 단계), 예측 y_pred를 구함
  3. y_pred와 y_true의 차이를 측정하여 이 배체이 대한 모델의 손실을 계산
  4. 배치에 대한 손실이 조금 감소되도록 모델의 모든 가중치를 업데이트

- 모델의 모든 가중치를 업데이트 하는 방법중 가장 쉬운 방법은 가중치 행렬의 원소를 모두 고정하고 관심 있는 하나만 다른 값을 적용하는것
- 이 값을 수정했을 때 손실이 감소한다면 감소하는 방향으로 수정 증가한다면 반대 방향으로 수정
- 이런 식으로 모델의 모든 가중치에 반복
- 이런 접근 방식은 모든 가중치 행렬의 원소마다 두 번의 (비용이 큰) 정방향 패스를 계산해야 하므로 엄청나게 비효율적

### 경사 하강법(gradient descent)

- 모델에 사용하는 (dot이나 + 같은) 모든 함수는 입력을 매끄럽고 연속적인 방식으로 변환
- 예를 들어 z = x + y에서 y를 조금 변경하면 z가 조금 변경
- y의 변경 방향을 알고 있다면 z의 변경 방향을 추측할 수 있음
- 수학적으로 이를 **미분 가능(differentiable)**하다고 말함
- 이런 함수를 연결하여 만든 함수도 여전히 미분 가능
- 이는 모델의 가중치를 조금 변경하면 손실 값이 예측 가능한 방향으로 조금 바뀜

- **그레이디언트(gradient)**라는 수학 연산을 사용하여 모델 가중치를 여러 방향으로 이동했을 때 손실이 얼마나 변하는지 설명할 수 있음
- 이 그레이디언트를 계산하면 이를 사용하여 손실이 감소하는 방향으로 전체 가중치를 한 번에 이동시킬 수 있음

![150x100](/assets/img/blog/smooth_function.jpg "연속적이고 매끄러운 함수")
- 위 그림처럼 함수가 연속적이므로 x를 조금 바꾸면 y가 조금만 변경될 것

![150x100](/assets/img/blog/epsilon_x_epsilon_y.jpg "연속적인 함수에서는 x를 조금 바꾸면 y가 조금만 변경된다")
- 위 그림과 같이 x를 작은 값 epsilon_x만큼 증가시켰을 때 y가 epsilon_y만큼 바뀐다고 말할 수 있다
- 이 함수가 매끈하므로 epsilon_x가 충분히 작다면 어떤 포인트 p에서 기울기 a의 선형 함수로 f를 근사할 수 있음
- epsilon_y는 a * epsilon_x가 됨
> f(x + epsilon_x) = y + a * epsilon_x

- 이 선형적인 근사는 x가 p에 충분히 가까울 때 유효

- 이 기울기를 p에서 f의 **도함수(derivative)**라고 함
- 이는 a가 음수일 때 p에서 양수 x만큼 조금 이동하면 f(x)가 감소한다는 것을 의미
- a가 양수일 때는 음수 x만큼 조금 이동하면 f(x)가 감소
- a의 절댓값(도함수의 크기)은 이런 증가나 감소가 얼마나 빠르게 일어날지 알려줌

![150x100](/assets/img/blog/derivative_of_p_to_f.jpg "p에서 f의 도함수")

### 텐서 연산의 도함수: 그레이디언트

- 텐서 연산(또는 텐서 함수)의 도함수를 **그레이디언트(gradient)**라고 부름
- 입력 파라미터가 바뀔 때 함수의 출력이 어떻게 바뀌는지 결정

#### 머신 러닝 기반의 예

- 입력 벡터, x(데이터셋에 있는 샘플)
- 행렬, W(모델의 가중치)
- 타깃, y_true(모델이 예측해야 할 값)
- 손실 함수, loss(현재의 예측과 y_true 간의 차이를 측정하기 위해 사용)

- W를 사용하여 예측 y_pred를 계산하고, 그다음 예측 y_pred와 타깃 y_true사이의 손실을 계산

y_pred = dot(W, x) ∙∙∙ 모델 가중치 W를 사용하여 x에 대한 예측을 만든다. <br>
loss_value = loss(y_pred, y_true) ∙∙∙ 예측이 얼마나 벗어났는지 추정한다.

- 고정된 입력 x와 y_true가 있을 때 (모델의 가중치) W 값을 손실 값에 매핑하는 함수로 해석할 수 있음

loss_value = f(W) ∙∙∙f는 W가 변화할 때 손실 값이 형성하는 곡선(또는 다차원 표면)을 설명

- 현재의 W 값을 W0라고 해 보자
- 점 W0에서 f의 도함수는 W와 크기가 같은 텐서 grad(loss_value, W0)
- 이 텐서의 각 원소 grad(loss_value, W0)[i,j]는 W0[i,j]를 수정했을 때 loss_value가 바뀌는 방향과 크기를 나타냄
- 텐서 grad(loss_value, W0) 가 W0에서 함수 f(W) = loss_value의 그레이디언트

#### 편도함수

- (입력으로 행렬 W를 받는) 텐서 연산 grad(f(W), W)는 스칼라 함수 grad_ij(f(W), w_ij)의 조합으로 표현할 수 있음
- 이 스칼라 함수는 W의 다른 모든 가중치가 일정하다고 가정할 때 가중치 W[i,j]에 대한 loss_value = f(W)의 도함수를 반환
- 이 때 grad_ij를 W[i,j]에 대한 f의 **편도함수(partial derivative)**라고 부름

- grad(loss_value, W0)는 W0에서 loss_value = f(x)가 가장 가파르게 상승하는 방향과 이 방향의 기울기를 나타내는 텐서로 해석할 수 있음
- 편도함수는 f의 특정 방향 기울기를 나타냄
- 그렇기 때문에 함수 f(x)에 대해서는 도함수의 반대 방향으로 x를 조금 움직이면 f(x)의 값을 감소시킬 수 있음
- 텐서의 함수 f(W)의 입장에서는 그레이디언트의 반대 방향으로 W를 움직이면 loss_value = f(W)의 값을 줄일 수 있음
- grad(loss_value, W0)는 W0에 아주 가까이 있을 때 기울기를 근사할 것이므로 W0에서 너무 크게 벗어나지 않기 위해 스케일링 비율 step이 필요

### 확률적 경사 하강법

- 미분 가능한 함수가 주어지면 이론적으로 이 함수의 최솟값을 해석적으로 구할 수 있음
- 함수의 최솟값은 도함수가 0인 지점
- 우리가 할 일은 도함수가 0이 되는 지점을 모두 찾고 이 중에서 어떤 포인트의 합수 값이 가장 작은지 확인하는 것
- 신경망에 적용하면 가장 작은 손실 함수의 값을 만드는 가중치의 조합을 해석적으로 찾는 것을 의미
- 이는 W에 대한 식 grad(f(W), W) = 0을 풀면 해결
- 이 식은 N개의 변수로 이루어진 다항식(여기서 N은 모델의 가중치 개수)
- N의 개수가 많다면 해석적으로 이 값을 찾는 것은 매우 어려움
- 대신 랜덤한 배치 데이터에서 현재 손실 값을 토대로 하여 조금씩 파라미터를 수정하는 알고리즘을 사용할 수 있음

1. 훈련 샘플 배치 x와 이에 상응하는 타깃 y_true를 추출
2. x로 모델을 실행하고 예측 y_pred를 구함(이를 정방향 패스라고 부름)
3. 이 배치에서 y_pred와 y_true 사이의 오차를 측정하여 모델의 손실을 계산
4. 모델의 파라미터에 대한 손실 함수의 그레이디언트를 계산(이를 **역방향 패스(backward pass)**라고 부름)
5. 그레이디언트의 반대 방향으로 파라미터를 조금 이동시킴 
> W -= learning_rate * gradient처럼 하면 배치에 대한 손실이 조금 감소.<br>
> **학습률(learning_rate)**은 경사 하강법 과정의 속도를 조절하는 스칼라 값

- 이것이 바로 **미니 배치 확률적 경사 하강법(mini-batch stochastic gradient descent)(미니 배치 SGD)**
- **확률적**(stochastic)이란 단어는 각 배치 데이터가 무작위로 선택된다는 의미

![100x100](/assets/img/blog/SGD.jpg "SGD가 1D 손실 함수(1개의 학습 파라미터)의 값을 낮춘다")

- learning_rate 값을 적절히 고르는 것이 중요
- 이 값이 너무 작으면 곡선을 따라 내려가는 데 너무 많은 반복이 필요하고 지역 최솟값(local minimum)에 갇힐 수 있음
- learning_rate가 너무 크면 손실 함수 곡선에서 완전히 임의의 위치로 이동시킬 수 있음
- 미니 배치 SGD 알고리즘의 한 가지 변종은 반복마다 하나의 샘플과 하나의 타깃을 뽑는 것
- 이것이 SGD
- 극단적인 반대의 경우를 생각해 보면 가용한 모든 데이터를 사용하여 반복을 실행할 수 있음
- 이를 **배치 경사 하강법**이라고 함
- 더 정확하게 업데이트되지만 더 많은 비용이 듦
- 극단적인 두 가지 방법의 효율적인 절충안은 적절한 크기의 미니 배치를 사용하는 것

![200x100](/assets/img/blog/gradient_descent_decreases_loss_value.jpg "경사 하강법이 2D 손실 함수(2개의 학습 파라미터)의 값을 낮춘다")

- 업데이트할 다음 가중치를 계산할 때 현재 그레이디언트 값만 보지 않고 이전에 업데이트된 가중치를 여러 가지 다른 방식으로 고려하는 SGD 응용이 많이 있음
> SGD, Adagrad, RMSProp 등

- 이런 응용들을 모두 **최적화 방법(optimazaion method)** 또는 **옵티마이저**라고 부름
- 특히 여러 응용에서 사용하는 **모멘텀(momentum)** 개념은 아주 중요
- 모멘텀은 SGD에 있는 2개의 문제점인 수렴 속도와 지역 최솟값을 해결