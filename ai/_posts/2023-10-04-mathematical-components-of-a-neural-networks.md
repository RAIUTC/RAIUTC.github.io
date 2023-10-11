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

![150x100](/assets/img/blog/local_minimum_global_minimum.jpg "지역 최솟값(local minimum)과 전역 최솟값(global minimum)")

- 위 그림에서 볼 수 있듯이 어떤 파라미터 값에서는 지역 최솟값에 도달
- 지역 최솟값 지점 근처에서는 왼쪽으로 이동해도 손실이 증가하고, 오른쪽으로 이동해도 손실이 증가
- 대상 파라미터가 작은 학습률을 가진 SGD로 최적화되었다면 최적화 과정이 전역 최솟값으로 향하지 못하고 이 지역 최솟값에 갇히게 될 것

- 모멘텀을 사용하여 이 문제를 피할 수 있음
- 실전에서 현재 그레이디언트 값뿐만 아니라 이전에 업데이트한 파라미터에 기초하여 파라미터 w를 업데이트

~~~python
past_velocity = 0.
momentum = 0.1  # 모멘텀 상수
while loss > 0.01:  # 최적화 반복 루프
    w, loss, gradient = get_current_parameters()
    velocity = momentum * past_velocity - learning_rate * gradient
    w = w + momentum * velocity - learning_rate * gradient
    past_velocity = velocity
    update_parameters(w)
~~~

- 위 코드는 단순한 구현 예

### 도함수 연결: 역전파 알고리즘

#### 연쇄 법칙

- 역전파는 (덧셈, 렐루, 텐서 곱셈 같은) 간단한 연산의 도함수를 사용해서 이런 기초적인 연산을 조합한 복잡한 연산의 그레이디언트를 쉽게 계산하는 방법
- 결정적으로 신경망은 서로 연결된 많은 텐서 연산으로 구성
- 이런 많은 텐서 연산은 간단하고 해당 도함수가 알려져 있음

- 미적분의 **연쇄 법칙(chain rule)**을 사용하면 이렇게 연결된 함수의 도함수를 구할수 있음
- 두 함수 f와 g가 있고, 두 함수를 연결한 fg가 있다고 가정
- fg(x) == f(g(x))
~~~python
def fg(x):
    x1 = g(x)
    y = f(xl)
    return y
~~~

- 연쇄 법칙을 사용하면 grad(y,x) == grad(y,x1) * grad(x1, x)가 됨
- f와 g의 도함수를 알고 있다면 fg의 도함수를 계산할 수 있음

~~~python
def fghj(x):
    x1 = j(x)
    x2 = h(x1)
    x3 = g(x2)
    y = f(x3)
    return y

grad(y, x) == (grad(y, x3) * grad(x3, x2) * grad(x2, x1) * grad(x1, x))
~~~
- 신경망의 그레이디언트 값을 계산하는데 이 연쇄 법칙을 적용하는 것이 **역전파** 알고리즘

#### 계산 그래프를 활용한 자동 미분

> 첫 번째로 만든 모델의 그래프 표현

![100x200](/assets/img/blog/calculate_graph_expression_with_2_layer.jpg "2개의 층으로 구성된 모델의 계산 그래프 표현")

![100x200](/assets/img/blog/calculate_graph_expression_with_2_layer2.jpg "2개의 층으로 구성된 모델의 계산 그래프 표현")

- 계산 그래프를 사용하면 계산을 데이터로 다룰 수 있기 때문에 컴퓨터 과학 분야에서 매우 성공적인 추상화 방법
- 계산 가능한 표현은 기계가 인식할 수 있는 데이터 구조로 인코딩되어 다른 프로그램의 입력이나 출력으로 사용할 수 있음

**역전파를 이해하기 위해 간단한 계산 그래프를 살펴보자**

![100x200](/assets/img/blog/simple_calculate_graph.jpg "간단한 계산 그래프 예")

- 하나의 선형 층만 있고 모든 변수는 스칼라
- 2개의 스칼라 변수 w와 b, 스칼라 입력 x를 받아 몇 개의 연산을 적용하여 출력 y를 만듦
- 마지막으로 절댓값 오차 손실 함수 loss_val = abs(y_true - y)를 적용
- loss_val을 최소화하도록 w와 b를 업데이트하기 위해 grad(loss_val, b)와 grad(loss_val, w)를 계산

![100x200](/assets/img/blog/running_forward_pass.jpg "정방향 패스 실행")

- 입력 x, 타깃 y_true, w, b에 해당하는 이 크래프의 '입력 노드(input node)'에 구체적인 값을 설정
- 이 값을 loss_val에 도달할 때까지 위에서 아래로 그래프의 모든 노드에 전파
- 이러한 과정이 정방향 패스(forward pass)

![200x150](/assets/img/blog/running_backward_pass.jpg "역방향 패스 실행")

- 그래프를 뒤집어 보자
- A에서 B로 가는 그래프의 모든 에지(edge)에 대해 B에서 A로 가는 반대 에지를 만듦
- A가 바뀔 때 B가 얼마나 변하는지 물음
- 즉, grad(B,A)는 반대 방향에서 만든 에지에 이 값을 표시
- 이 역방향 그래프가 역방향 패스를 나타냄

- 다음과 같은 값을 얻을 수 있음
    - grad(loss_val, x2) = 1 &rarr; x2가 epsilon만큼 변할 때 loss_val = abs(4 - x2)가 같은 양만큼 변하기 때문임
    - grad(x2, x1) = 1 &rarr; x1이 epsilon만큼 변할 때 x2 = x1 + b = x1 + 1이 같은 양만큼 변하기 때문임
    - grad(x2, b) = 1 &rarr; b가 epsilon만큼 변할 때 x2 = x1 + b = 6 + b가 같은 양만큼 변하기 때문임
    - grad(x1, w) = 2 &rarr; w가 epsilon만큼 변할 때 x1 = x * w = 2 * w는 2 * epsilon만큼 변하기 때문임

- 연쇄 법칙이 역방향 그래프에 대해 알려 주는 것은 노드가 연결된 경로를 따라 각 에지의 도함수를 곱하면 어떤 노드에 대한 다른 노드의 도함수를 얻을 수 있다는 것
> 예를 들어 grad(loss_val, w) = grad(loss_val, x2) * grad(x2, x1) * grad(x1, w)

![200x150](/assets/img/blog/route_loss_val_to_w_in_backward_pass.jpg "역방향 그래프에서 loss_val부터 w까지의 경로")

- 이 그래프에 연쇄 법칙을 적용하여 원하는 값을 구할 수 있음
    - grad(loss_val, w) = 1 * 1 * 2 = 2
    - grad(loss_val, b) = 1 * 1 = 1

- 역방향 그래프에서 관심 대상인 두 노드 a와 b를 연결하는 경로가 여러 개라면 모든 경로의 도함수를 더해서 grad(a,b)를 얻을 수 있음

- 역전파는 연쇄 법칙을 계산 그래프에 적용한 것 뿐
- 역전파는 최종 손실 값에서 시작하여 아래층에서 맨 위층까지 거꾸로 거슬러 올라가 각 파라미터가 손실 값에 기여한 정도를 계산
- 즉, 계산 그래프에서 각 노드의 손실 기여도를 역전파

- 요즘에는 텐서플로와 같이 **자동 미분(automatic differentiation)**이 가능한 최신 프레임워크를 사용해서 신경망을 구현
- 자동 미분은 방금 본 계산 그래프와 같은 형태로 구현
- 자동 미분은 정방향 패스를 작성하는 것 외에 다른 작업 없이 미분 가능한 텐서 연산의 어떤 조합에 대해서도 그레이디언트를 계산할 수 있음

#### 텐서플로의 그레이디언트 테이프

- 텐서플로의 강력한 자동 미분 기능을 활용할 수 있는 API는 GradientTape
- 이 API는 파이썬의 with 문과 함께 사용하여 해당 코드 블록 안의 모든 텐서 연산을 계산 그래프 형태로 기록
- 그다음 이 그래프를 사용해서 (tf.Variable 클래스의 인스턴스인) 변수 또는 변수 집합에 대한 어떤 출력의 그레이디언트도 계산할 수 있음
- tf.Variable은 변경 가능한(mutable) 상태를 담기 위한 특별한 종류의 텐서
- 예를 들어 신경망의 가중치는 항상 tf.Variable의 인스턴스

~~~python
import tensorflow as tf

x = tf.Variable(0.) # 초깃값 0으로 스칼라 변수를 생성
with tf.GradientTape() as tape:   # GradientTape블록을 시작한다
    y = 2 * x + 3     # 이 블록 안에서 텐서 연산을 실행한다
grad_of_y_wrt_x = tape.gradient(y, x)   # tape를 사용해서 변수x에 대한 출력 y를 계산한다
~~~

~~~python
x = tf.Variable(tf.zeros((2, 2)))   # 크기가 (2,2)이고 초깃값이 모두 0인 변수를 생성
with tf.GradientTape() as tape: 
    y = 2 * x + 3
grad_of_y_wrt_x = tape.gradient(y, x)   # grad_of_y_wrt_x는(x와 크기가 같은)(2,2) 크기의 텐서로 x = [[0,0],[0,0]]일 때 y = 2 * x + 3의 곡률을 나타낸다
~~~

- GradientTape를 다차원 텐서와 함께 사용할 수 있음

~~~python
W = tf.Variable(tf.random.uniform((2, 2)))
b = tf.Variable(tf.zeros((2,)))
x = tf.random.uniform((2, 2))
with tf.GradientTape() as tape:
    y = tf.matmul(x, W) + b   # matmul은 텐서플로의 점곱 함수
grad_of_y_wrt_W_and_b = tape.gradient(y, [W, b])    # grad_of_y_wrt_W_and_b는 2개의 텐서를 담은 리스트이다. 각 텐서는 W,b와 크기가 같다
~~~

- 변수 리스트의 그레이디언트를 계산할 수도 있음

## 2.5 첫 번째 예제 다시 살펴보기

- 처음 구현한 모델은 층이 서로 연결되어 모델을 구성하고, 모델은 입력 데이터를 예측으로 매핑
- 그다음 손실 함수가 이 예측과 타깃을 비교하여 손실 값을 만듦
- 즉, 모델의 예측이 기대한 것에 얼마나 잘 맞는지 측정
- 옵티마이저는 이 손실 값을 사용하여 모델의 가중치를 업데이트

![150x100](/assets/img/blog/relation_between_model_layer_loss_function_optimizer.jpg "모델, 층, 손실 함수, 옵티마이저 사이의 관계")

- **입력 데이터**

~~~python
(train_images, train_labels), (test_images, test_labels) = mnist.load_data()
train_images = train_images.reshape((60000, 28 * 28))
train_images = train_images.astype("float32") / 255
test_images = test_images.reshape((10000, 28 * 28))
test_images = test_images.astype("float32") / 255
~~~

- 입력 이미지의 데이터 타입은 float32로, 훈련 데이터는 (60000, 784) 크기, 테스트 데이터는 (10000, 784)크기의 넘파이 배열로 저장

- **모델**

~~~python
model = keras.Sequential([
    layers.Dense(512, activation="relu"),
    layers.Dense(10, activation="softmax")
])
~~~

- 이 모델은 2개의 Dense층이 연결되어 있고 각 층은 가중치 텐서를 포함하여 입력 데이터에 대한 몇 개의 간단한 텐서 연산을 적용
- 층의 속성인 가중치 텐서는 모델이 정보를 저장하는 곳

- **컴파일 단계**

~~~python
model.compile(optimizer="rmsprop",
              loss="sparse_categorical_crossentropy",
              metrics=["accuracy"])
~~~

- sparse_categorical_crossentropy는 손실 함수
- 손실값은 가중치 텐서를 학습하기 위한 피드백 신호로 사용되며 훈련하는 동안 최소화
- 미니 배치 확률적 경사 하강법을 통해 손실이 감소
- 경사 하강법을 적용하는 구체적인 방식은 첫 번째 매개변수로 전달된 rmsprop 옵티마이저에 의해 결정

- **훈련 반복**

~~~python
model.fit(train_images, train_labels, epochs=5, batch_size=128)
~~~

- fit 메서드를 호출했을 때 다음과 같이 학습이 반복
- 모델이 128개 샘플 미니 배치로 훈련 데이터를 다섯 번 반복(전체 훈련 데이터에 수행되는 각 반복을 **에포크(epoch)**라고 함)
- (미적분이 연쇄 법칙에서 파생된 역전파 알고리즘을 사용하여) 각 배치에서 모델이 가중치에 대한 손실의 그레이디언트를 계산
- 그다음 이 배치에서 손실 값을 감소시키는 방향으로 가중치를 이동시킴
- 다섯 번의 에포크 동안 모델은 2,345번의 그레이디언트 업데이트를 수행할 것(에포크마다 469번)
- 최종적으로 원하는 성능을 가진 모델을 얻을 수 있을 것

### 텐서플로를 사용하여 첫 번째 예제를 밑마탁부터 다시 구현하기

#### 단순한 Dense 클래스

output = activation(dot(W, input) + b)

- Dense층이 구현하는 입력 변환
- W와 b는 모델 파라미터, activation은 각 원소에 적용되는 함수(일반적으로 relu이지만 마지막 층에는 softmax를 사용)

~~~python
import tensorflow as tf

class NaiveDense:
    def __init__(self, input_size, output_size, activation):

        self.activation = activation

        w_shape = (input_size, output_size)   # 랜덤한 값으로 초기화된(input_size, output_size)크기의 행렬 W를 만든다
        w_initial_value = tf.random.uniform(w_shape, minval=0, maxval=1e-1)
        self.W = tf.Variable(w_initial_value)

        b_shape = (output_size,)    # 0으로 초기화된 (output_size,)크기의 벡터 b를 만든다
        b_initial_value = tf.zeros(b_shape)
        self.b = tf.Variable(b_initial_value)

    def __call__(self, inputs):   # 정방향 패스를 수행
        return self.activation(tf.matmul(inputs, self.W) + self.b)

    @property
    def weights(self):    # 층의 가중치를 추출하기 위한 메서드
        return [self.W, self.b]
~~~

#### 단순한 Sequential 클래스

~~~python
class NaiveSequential:
    def __init__(self, layers):
        self.layers = layers

    def __call__(self, inputs):
        x = inputs
        for layer in self.layers:
           x = layer(x)
        return x

    @property
    def weights(self):
       weights = []
       for layer in self.layers:
           weights += layer.weights
       return weights
~~~

~~~python
model = NaiveSequential([
    NaiveDense(input_size=28 * 28, output_size=512, activation=tf.nn.relu),
    NaiveDense(input_size=512, output_size=10, activation=tf.nn.softmax)
])
assert len(model.weights) == 4
~~~

- NativeDense 클래스와 NativeSequential 클래스를 사용하여 케라스와 유사한 모델을 만들 수 있다

#### 배치 제너레이터

~~~python
import math

class BatchGenerator:
    def __init__(self, images, labels, batch_size=128):
        assert len(images) == len(labels)
        self.index = 0
        self.images = images
        self.labels = labels
        self.batch_size = batch_size
        self.num_batches = math.ceil(len(images) / batch_size)

    def next(self):
        images = self.images[self.index : self.index + self.batch_size]
        labels = self.labels[self.index : self.index + self.batch_size]
        self.index += self.batch_size
        return images, labels
~~~

#### 훈련 스텝 실행하기

- 한 배치 데이터에서 모델을 실행하고 가중치를 업데이트 하는 일
- 이를 위해 다음이 필요함
    1. 배치에 있는 이미지에 대한 모델의 예측을 계산
    2. 실제 레이블을 사용하여 이 예측의 손실 값을 계산
    3. 모델 가중치에 대한 손실의 그레이디언트를 계산
    4. 이 그레이디언트의 반대 방향으로 가중치를 조금 이동

~~~python
def one_training_step(model, images_batch, labels_batch):

    # 정방향 패스를 실행한다.(GradientTape 블록 안에서 모델의 예측을 계산한다)  
    with tf.GradientTape() as tape:                     
        predictions = model(images_batch)
        per_sample_losses = tf.keras.losses.sparse_categorical_crossentropy(
            labels_batch, predictions)
        average_loss = tf.reduce_mean(per_sample_losses)

    gradients = tape.gradient(average_loss, model.weights)    # 가중치에 대한 손실의 그레이디언트를 계산한다. gradients리스트의 각 항목은 model.weights리스트에 있는 가중치에 매칭된다.
    update_weights(gradients, model.weights)    # 이 그레이디언트를 사용하여 가중치를 업데이트한다
    return average_loss
~~~

~~~python
learning_rate = 1e-3

def update_weights(gradients, weights):
    for g, w in zip(gradients, weights):
        w.assign_sub(g * learning_rate)   # 텐서플로 변수의 assign_sub 메서드는 -=과 동일
~~~

- '가중치 업데이트'단계의 목적은 이 배치의 손실을 감소시키기 위한 방향으로 가중치를 '조금' 이동하는 것
- 이동의 크기는 '학습률'에 의해 결정
- update_weights 함수를 구현하는 가장 간단한 방법은 각 가중치에서 gradient * learning_rate를 빼는 것

- 실제로는 이런 가중치 업데이트 단계를 수동으로 구현하는 경우는 거의 없고 케라스의 Optimizer 인스턴스를 이용

~~~python
from tensorflow.keras import optimizers

optimizer = optimizers.SGD(learning_rate=1e-3)

def update_weights(gradients, weights):
    optimizer.apply_gradients(zip(gradients, weights))
~~~

#### 전체 훈련 루프

~~~python
def fit(model, images, labels, epochs, batch_size=128):
    for epoch_counter in range(epochs):
        print(f"에포크 {epoch_counter}")
        batch_generator = BatchGenerator(images, labels)
        for batch_counter in range(batch_generator.num_batches):
            images_batch, labels_batch = batch_generator.next()
            loss = one_training_step(model, images_batch, labels_batch)
            if batch_counter % 100 == 0:
                print(f"{batch_counter}번째 배치 손실: {loss:.2f}")
~~~

- 함수를 테스트

~~~python
from tensorflow.keras.datasets import mnist
(train_images, train_labels), (test_images, test_labels) = mnist.load_data()

train_images = train_images.reshape((60000, 28 * 28))
train_images = train_images.astype("float32") / 255
test_images = test_images.reshape((10000, 28 * 28))
test_images = test_images.astype("float32") / 255

fit(model, train_images, train_labels, epochs=10, batch_size=128)
~~~

- 모델 평가

~~~python
predictions = model(test_images)
predictions = predictions.numpy()   # 텐서플로 텐서의 .numpy() 메서드를 호출하여 넘파이 배열로 바꾼다
predicted_labels = np.argmax(predictions, axis=1)
matches = predicted_labels == test_labels
print(f"정확도: {matches.mean():.2f}")
~~~

## 2.6 요약

- **텐서**는 현대 머신 러닝 시스템의 기초. 텐서는 dtype, ndim, shape 속성을 제공
- 텐서 연산(덧셈, 텐서 곱셈, 원소별 곱셈 등)을 통해 수치 텐서를 조작할 수 있음. 이런 연산을 기하학적 변형을 적용하는 것으로 이해할 수 있음. 일반적으로 딥러닝의 모든 것은 기하학적으로 해석할 수 있음
- 딥러닝 모델은 가중치 텐서를 매개변수로 받는 간단한 텐서 연산을 연결하여 구성
- 모델의 가중치는 모델이 학습한 '지식'을 저장하는 곳. **학습(learning)**은 훈련 데이터 샘플과 그에 상응하는 타깃이 주어졌을 때 손실 함수를 최소화하는 모델의 가중치 값을 찾는 것을 의미

- 데이터 샘플과 타깃의 배치를 랜덤하게 뽑고 이 배치에서 모델 파라미터에 대한 손실의 그레이디언트를 계산함으로써 학습이 진행. 모델의 파라미터는 그레이디언트의 반대 방향으로 조금씩(학습률에 의해 정의된 크기만큼) 움직임 이를 **미니 배치 경사 하강법**이라고 부름
- 전체 학습 과정은 신경망에 있는 모든 텐서 연산이 미분 가능하기 때문에 가능. 현재 파라미터와 배치 데이터를 그레이디언트 값에 매핑해 주는 그레이디언트 함수를 구성하기 위해 미분의 연쇄 법칙을 사용할 수 있음. 이를 역전파라고 부름
- 두 가지 핵심 개념은 **손실**과 **옵티마이저**. 이 두가지는 모델에 데이터를 주입하기 전에 정의되어야 함

- 손실은 훈련하는 동안 최소화해야 할 양이므로 해결하려는 문제의 성공을 측적하는 데 사용
- 옵티마이저는 손실에 대한 그레이디언트가 파라미터를 업데이트하는 정확한 방식을 정의
> 예를 들어 RMSProp 옵티마이저, 모멘텀을 사용한 SGD 등