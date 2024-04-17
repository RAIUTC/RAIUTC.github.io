---
layout: post
title: Variable & List
description: |
  이 블로그 글은 Python에서 변수와 리스트에 대한 기초적인 내용을 다루고 있습니다. 변수와 메모리, 기본 자료형부터 리스트의 다양한 활용 방법까지 설명되어 있습니다. 코드 예시와 함께 데이터 형 변환, 리스트 연산, 그리고 이차원 리스트까지 다루고 있어 Python 초보자에게 유용한 정보를 제공합니다.
categories: 인공지능(AI)
sitemap: false
hide_last_modified: true
---

# 인공지능(AI)기초 다지기 Python[Variable & List]

## variable & memory

### 변수의 개요

- 가장 기초적인 프로그래밍 문법 개념
- **데이터(값)**을 저장하기 위한 메모리 공간의 프로그래밍상 이름

~~~python
a = 5
b = 3
a + b
~~~

professor = "Sungchul Choi"의 의미는? &rarr; Professor라는 <span style="color:blue">변수</span>에 "Sungchul Choi"라는 <span style="color:blue">값</span>을 넣으라는 의미

프로그래밍에서는 변수는 <span style="color:blue">값을 저장하는 장소</span> 변수는 <span style="color:blue">메모리 주소</span>를 가지고 있고 변수에 들어가는 <span style="color:blue">값</span>은 <span style="color:blue">메모리 주소</span>에 할당됨

### 메모리와 변수

- 변수 - 프로그램에서 사용하기 위한 특정한 값을 저장하는 공간
- 선언 되는 순간 <span style="color:blue">메모리 특정영역에 물리적인 공간</span>이 할당됨
- 변수에는 값이 할당되고 해당 값은 메모리에 저장됨
- A = 8의 의미는 "A는 8이다"가 아닌 A라는 이름을 가진 메모리 주소에 8을 저장하라 임

### 변수 이름 작명법

- 알파벳, 숫자, 언더스코어(_)로 선언 가능
> data = 0, _a12 = 2, _gg = 'afdf'
- 변수명은 <span style="color:blue">의미 있는 단어로 표기</span>하는 것이 좋다
> professor_name = 'Sungchul Choi'
- 변수명은 <span style="color:blue">대소문자가 구분</span>된다.
> ABC와 Abc는 같지 않다
- 특별한 의미가 있는 <span style="color:blue">예약어(reserved word)는 쓰지 않는다.</span>
> for, if, else 등

## bssic operations

### 기본 자료형 (primitive data types)

- data type: 파이썬이 처리할 수 있는 데이터 유형

<p align="center">
<img src="/assets/img/blog/data_type.png">
</p>

> 데이터 유형마다 크기가 다름

### 자료형 사용 예시

<p align="center">
<img src="/assets/img/blog/data_type_example.png">
</p>

### Dynamic Typing
> 코드 실행시점에 데이터의 Type을 결정하는 방법

<p align="center">
<img src="/assets/img/blog/dynamic_typing.png">
</p>

### 연산자(Operator)와 피연산자(Operand)

- +, -, *, / 같은 기호들을 연산자라고 칭함
- 연산자에 의해 계산이 되는 숫자들은 피연산자라 칭함
- <span style="color:blue">"3 + 2"에서 3과 2는 피연산자, +는 연산자임</span>
- 수식에서 연산자의 역할은 수학에서 연산자와 동일
- <span style="color:blue">연산의 순서는 수학에서 연산 순서와 같음</span>
- 문자간에도 + 연산이 가능함 &rarr; concatenate
> "a" + "b" = "ab"

### 제곱승과 나머지 구하기

"\**"는 **제곱승** 계산 연산자

<p align="center">
<img src="/assets/img/blog/square.png">
</p>

"%"는 나머지를 구하는 연산자

<p align="center">
<img src="/assets/img/blog/remainder.png">
</p>

### 증감 또는 감소 연산

a += 1 는 a = a + 1과 같은 의미로 증가연산 (-=)

<p align="center">
<img src="/assets/img/blog/increase.png">
</p>

만약 a=1일 때 a = 1 + 1로 a에 다시 2가 할당(assign)됨<br>
즉 좌변에 a는 할당 받는 변수 (variable)<br>
우변에 a는 기존 a의 값 (value)

### 데이터 형 변환: 정수형 $$\Leftrightarrow$$ 실수형

float()와 int() 함수를 사용하여 데이터의 형 변환 가능

<p align="center">
<img src="/assets/img/blog/data_type_conversion.png">
</p>

- **실수형에서 정수형으로 형 변환 시 소수점 이하 내림**

<p align="center">
<img src="/assets/img/blog/data_type_conversion2.png">
</p>

### 데이터 형 변환: 숫자 $$ \Leftrightarrow $$ 문자열

- 문자열로 선언된 값도 int(), float()함수로 형 변환 가능

<p align="center">
<img src="/assets/img/blog/data_type_conversion3.png">
</p>

- a와 b를 실수형으로 덧셈하고, 문자열로 연결하려면? &rarr; 형을 맞춰라

<p align="center">
<img src="/assets/img/blog/data_type_conversion4.png">
</p>

### 데이터 형 확인하기

- **type()**함수는 변수의 데이터 형을 확인하는 함수

<p align="center">
<img src="/assets/img/blog/data_type_check.png">
</p>

## list

### List 또는 Array

- 시퀀스 자료형, 여러 데이터들의 집합
- int, float같은 다양한 데이터 타입 포함

<p align="center">
<img src="/assets/img/blog/list.png">
</p>

### 인덱싱(Indexing)

- list에 있는 값들은 <span style="color:blue">주소(offset)</span>를 가짐
> 주소를 사용해 할당된 값을 호출

<p align="center">
<img src="/assets/img/blog/indexing.png">
<img src="/assets/img/blog/indexing2.png">
</p>

### 슬라이싱 (Slicing)

- list의 값들을 잘라서 쓰는 것이 슬라이싱
- list의 주소 값을 기반으로 부분 값을 반환

<p align="center">
<img src="/assets/img/blog/slicing.png">
</p>

### 리스트의 연산

- concatenation, is_in, 연산 함수들

<p align="center">
<img src="/assets/img/blog/list_operation.png">
</p>

### 리스트의 연산 - 추가와 삭제

- append, extend, insert, remove, del등 활용

<p align="center">
<img src="/assets/img/blog/list_operation2.png">
</p>

### Python 리스트만의 특징

- **다양한 Data Type이 하나에 List에 들어감**

<p align="center">
<img src="/assets/img/blog/list_operation3.png">
<img src="/assets/img/blog/list_operation4.png">
</p>

### 리스트 메모리 저장 방식

- 파이썬은 해당 리스트 변수에는 리스트 주소값이 저장됨

<p align="center">
<img src="/assets/img/blog/list_memory.png">
<img src="/assets/img/blog/list_memory2.png">
</p>

> b = a\[:\] # copy

### 패킹과 언패킹

- 패킹: 한 변수에 여러 개의 데이터를 넣는 것
- 언패킹: 한 변수의 데이터를 각각의 변수로 반환

<p align="center">
<img src="/assets/img/blog/packing.png">
</p>

### 이차원 리스트

- 리스트 안에 리스트를 만들어 행렬(Matrix) 생성

<p align="center">
<img src="/assets/img/blog/2d_list.png">
</p>

- 이차원 리스트를 복사하는 방법?
> 2dim에선 copy 방법이 다름 &rarr; copy.deepcopy() 사용