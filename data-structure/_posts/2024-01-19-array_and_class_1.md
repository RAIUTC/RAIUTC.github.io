---
layout: post
title: Array & Class(1)
description: |
  이 글에서는 배열과 구조체의 기초적인 사용법부터 함수 매개변수로 전달할 때의 유의점, 그리고 구조체를 활용한 Call by value와 Call by reference의 차이점을 다룹니다.
  또한, 객체지향 프로그래밍의 핵심 개념인 추상화, 캡슐화, 상속, 다형성에 대해서도 살펴봅니다.
  이를 통해 자료구조와 객체지향 프로그래밍의 핵심 원리를 손쉽게 이해할 수 있습니다.
categories: 자료구조
sitemap: false
hide_last_modified: true
---

# Array & Class(1)

## 배열(Array)

- **같은 자료형의 변수를 여러 개를 만들어 관리해야하는 경우에 사용**
  - 여러 개의 변수 선언: <span style="color:skyblue">int</span> A0, A1 A2, A3, ..., A5;
  - 하나의 배열 선언: <span style="color:skyblue">int</span> A[6];

<p align="center">
<img src="/assets/img/blog/array.png">
</p>

## 배열을 쓰는 이유

- **반복 코드(for-loop)등에서 배열을 사용하면 효율적인 프로그래밍이 가능**
  - 예) 최대값을 구하는 프로그램

<p align="center">
<img src="/assets/img/blog/find_max_program.png">
</p>

  - 만약 배열이 없다면? &rarr; 반복문 사용의 의미가 없음

## 1차원 배열

- **1차원 배열의 선언(create)**
  - <span style="color:skyblue">자료형</span> <span style="color:red">배열이름</span>[<span style="color:skyblue">배열의 크기</span>];
  - <span style="color:skyblue">int</span> <span style="color:red">A</span>[<span style="color:skyblue">6</span>];
  - int A[6] = {1, 2, 3, 4, 5, 6};

- **배열의 값 반환(retrieve)**
  - <span style="color:red">배열이름</span>[index];
  - std::cout << <span style="color:red">A</span>[3];

- **배열의 값 저장(sore)**
  - <span style="color:red">배열이름</span>[index] = 값;
  - <span style="color:red">A</span>[3] = 10;

<p align="center">
<img src="/assets/img/blog/one_dim_array.png">
</p>

## 문자열: 특별한 1차원 배열

- **C++에서 문자열 처리**
  - #include <string>
  - <span style="color:skyblue">string</span> s = "game over";

<p align="center">
<img src="/assets/img/blog/string_array.png">
</p>

  - string class에서는 다루기 편하게 다양한 연산들이 정의되어 있음
    - s.size(): string s의 길이 반환(length도 동일한 역할)
    - ==: 문자열 비교(s1 == s2, 같으면 true, 다르면 false)
    - +=: 문자열 추가(s1 += s2, s1의 뒤에 s2를 append함)

## 2차원 배열
- **2차원 배열의 선언**
  - 자료형 배열이름[행의_크기][열의_크기];

<p align="center">
<img src="/assets/img/blog/two_dim_array_code.png">
</p>

<p align="center">
<img src="/assets/img/blog/two_dim_array.png">
<img src="/assets/img/blog/two_dim_array_memory_store.png">
</p>

## 함수의 매개변수 전달

- **함수에 값을 전달할 때**
  - 일반변수: **값**이 복사되어 전달(call by value)
  - 배열: 배열의 시작 **주소**를 전달(call by reference) 

- **Call by value**
  - Actual parameters의 값이 formal parameters로 **복사**
  - 각각은 메모리의 다른 곳에 저장

<p align="center">
<img src="/assets/img/blog/call_by_value_code.png">
</p>

- **Call by reference(using pointer)**
  - Actual/formal parameters가 똑같은 메모리 공간을 참조
  - Formal parameters의 변화가 actual parameters에도 반영
    - C/C++에서는 pointer를 통해 call by reference가 수행 가능
    - C++에서는 참조자(reference &)를 통해서도 수행 가능

<p align="center">
<img src="/assets/img/blog/call_by_reference_code.png">
</p>

## 함수의 매개변수로서의 배열

- **함수에 배열을 전달할 때는 배열의 시작 주소를 전달**
  - 함수에서 formal parameter의 형태: <span style="color:skyblue">자료형</span> 배열이름<span style="color:red">[]</span>
    - void function(int a[], int n) // 배열의 크기도 같이 전달
    - Call by reference로 동작하게 됨

<p align="center">
<img src="/assets/img/blog/call_by_reference_array.png">
</p>

## 배열에서의 주의사항

- **<span style="color:skyblue">매개 변수로 배열의 길이도 전달해야 함</span>**
  - C/C++에서는 배열 시작 주소만으로는 배열의 길이를 알 수 없음

<p align="center">
<img src="/assets/img/blog/have_to_pass_array_length.png">
</p>

- **<span style="color:skyblue">2차원 이상의 다차원 배열의 매개 변수 전달에 조심</span>**
  - <span style="color:skyblue">int</span> findMaxPixel(<span style="color:skyblue">int</span> a[]<span style="color:red">[5]</span>, <span style="color:skyblue">int</span> h, <span style="color:skyblue">int</span> w) 
  - 문제점: 열의 크기가 5인 2차원 배열만 받을 수 있음
  - 해결책: 동적할당(이중 포인터, stl의 vector)

## 구조체

- **기존의 자료형들을 조합해 새로운 자료형을 만드는 방법**
- **배열과의 차이**
  - 구조체(structure): 타입이 다른 데이터를 하나로 묶음
  - 배열(array): 타입이 같은 데이터를 하나로 묶음

<p align="center">
<img src="/assets/img/blog/structure.png">
</p>

## C/C++에서 구조체의 정의와 선언

- **Student 구조체의 예시**

<p align="center">
<img src="/assets/img/blog/structure_definition.png">
</p>

  - 멤버 접근: 항목 연산자(membership operator) &rarr; '.'(dot)
    - a.id = 30830;
    - a.score = 92.3;
    - strcpy(a.name, "Joy");

## 구조체와 연산자

- **대입 연산자만 가능**

<p align="center">
<img src="/assets/img/blog/structure_assignment_operator.png">
</p>

- **다른 연산자는 사용불가**

<p align="center">
<img src="/assets/img/blog/not_allowed_structure_operator.png">
</p>

## 구조체와 함수

- **함수의 매개 변수나 반환형으로 사용할 수 있음**
  - 구조체 매개변수 전달은 기본적으로 Call by value로 동작함

<p align="center">
<img src="/assets/img/blog/structure_parameter_operate_as_call_by_value.png">
</p>

  - 구조체의 반환형 역시 Call by value로 동작함

<p align="center">
<img src="/assets/img/blog/structure_return_value_operate_call_by_value.png">
</p>

- **구조체 포인터를 전달하여 call by reference가능**
  - 구조체 포인터가 주어진 경우 멤버 접근 연산자로 <span style="color:skyblue">-></span>를 사용
  - call by value시 발생하는 copy cost를 피할 수 있음

<p align="center">
<img src="/assets/img/blog/structure_pointer.png">
</p>

## 객체지향이 나온 이유

- **객체지향 이전의 프로그래밍 방식**
  - 절차지향 프로그래밍(Procedural Programming)에서 하나의 큰 프로그램은 여러 작은 함수들(procedures)의 단계적 호출로 이루어짐
  - 데이터보다는 함수에 집중; **<span style="color:red">데이터의 관리가 힘듦</span>**
  - 프로그램의 규모가 커지면 함수들이 서로 얽혀 유지보수가 힘듦

<p align="center">
<img src="/assets/img/blog/procedural_programming.png">
</p>

## 객체지향 프로그래밍

- **객체지향 프로그래밍**
  - 함수보다는 **데이터/객체**를 중심으로 프로그램을 설계하는 방식
  - 하나의 객체는 속성(멤버변수)과 함수(메소드)로 구성

- **4 Pillars of OOP: OOP의 철학적 특징**
  - 추상화(Abstraction)
  - 캡슐화(Encapsulation)
  - 상속(Inheritance)
  - 다형성(Polymorphism)

- C++의 class는 위 4가지 특징을 구현할 수 있는 방법을 제공

## Abstraction
- **어떠한 것을 설명할 때 간단한 단어로 핵심을 표현**
  - 무엇이 중요한지 불필요한지 가려내어 핵심적인 것을 추려냄
  - 상속과 관련
    - 공통된/일반적일수록 상위 &larr;&rarr; 구체적/특수할 수록 하위에 위치
  - 캡슐화와 관련
    - 내부의 구현/상태는 감추고 외부 interface만 집중
    - interface가 고정되면 내부 코드가 수정되어도 영향이 미미

<p align="center">
<img src="/assets/img/blog/abstraction.png">
</p>

## Encapsulation

- **관련된 속성(멤버변수)와 함수(메소드)를 하나의 객체 안으로 묶는 기법**
  - 외부로부터 알 필요가 없는 구체적인 사항은 감춤

<p align="center">
<img src="/assets/img/blog/encapsulation.png">
</p>

## Inheritance
- **공통된 속성이나 메소드를 상위로 묶는 기법**
  - 중복되는 코드를 줄일 수 있음

<p align="center">
<img src="/assets/img/blog/inheritence.png">
</p>

## Polymorphism
- **Poly(many) + Morphism(form)**
  - 하나의 object가 여러가지의 형태를 가질 수 있게 하는 기능
    - 코드를 간결하게 표현 가능

<p align="center">
<img src="/assets/img/blog/polymorphism.png">
</p>

## What You Need To Know

- **배열**
  - 1차원/2차원 배열 선언/사용법
  - 함수의 매개변수로 전달 할 때 유의점
    - 배열은 배열의 시작 주소를 넘겨줌(Call by reference)
    - 배열의 길이도 같이 넘겨줘야 함

- **구조체**
  - 구조체의 개념과 사용법
  - 구조체를 함수의 매개변수로 넘겨줄 때는 call by value
  - 구조체 포인터를 이용하여 call by reference

- **객체지향 프로그래밍**
  - 4pillars: 추상화/캡슐화/상속/다형성