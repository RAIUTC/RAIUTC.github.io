---
layout: post
title: Queue (3) & Link
description: |
  이 글은 너비 우선 탐색(BFS)을 활용한 미로 탐색 알고리즘과 포인터에 대한 기초적인 개념을 다룹니다. 
  BFS를 통해 최단 경로를 찾는 방법을 소개하며, 포인터에 대한 리뷰를 통해 동적 할당과 자료의 연결에 대한 장점과 구현에 관한 내용을 간결하게 설명합니다.
categories: 자료구조
sitemap: false
hide_last_modified: true
---

# Queue (3) & Link

## 미로 탐색 문제

- **문제 정의**
  - **입력**: 2차원 평면상의 미로(2차원 배열)
    - 행의 수 n, 열의 수 m
    - 출발점: s, 도착점: t, 벽: 1, 통로: 0
  - **출력**: 성공 or 실패
    - 성공: s에서 t로 도달 할 수 있음
    - 실패: s에서 t로 도달 할 수 없음
  - **제약조건**:
    - 사람은 &uarr;, &larr;, &darr;, &rarr;로만 움직일 수 있음
    - 벽으로는 갈 수 없음 (통로를 통해서만 움직일 수 있음)

<p align="center">
<img src="/assets/img/blog/maze_solving_prob.png">
</p>

## 너비 우선 탐색 (BFS)

- **너비 우선 탐색의 아이디어**
  - 시작점에서 인접한 모든 위치들을 <span style="color:blue">먼저 방문</span>
  - 다음 방문한 점을 시작점으로 다시 너비 우선 탐색
    - 순서대로 탐색하기 위해 **큐**를 활용
  - 방문하지 않은 점이 없을 때까지 반복

<p align="center">
<img src="/assets/img/blog/bfs_idea.png">
</p>

## 너비 우선 탐색 의사코드

<p align="center">
<img src="/assets/img/blog/bfs_pseudo_code.png">
</p>

## 너비 우선 탐색 예제

<p align="center">
<img src="/assets/img/blog/bfs_ex.png">
</p>

## 시간 복잡도 분석

- **너비 우선 탐색의 시간 복잡도 $$T(n,m)$$**
  - while loop의 반복 횟수에 의해 결정됨
    - 매 반복에서의 연산들은 상수 시간 C(or $$O(1)$$)이 소요됨
    - 한 번 방문했던 통로는 다시 가지 않기 때문에, 최악의 경우 queue에 들어왔다가 나가는 아이템의 수는 통로의 수 P와 같음 &rarr; 즉, P번 만큼 while loop이 반복됨
    - 따라서, $$ㅅT(n,m) = CP <= Cnm = O(nm)$$

<p align="center">
<img src="/assets/img/blog/bfs_time_complexity_analysis.png">
</p>

## 포인터 개념

- **포인터: 다른 변수의 메모리 주소를 값으로 가지는 변수**

<p align="center">
<img src="/assets/img/blog/pointer_concepts.png">
</p>

## Why Pointers?

- **포인터를 통해 연결된 표현(Linked Representation)을 구현하기 위함**
  - 각 노드에는 <span style="color:red">데이터</span>와 <span style="color:red">다음 노드의 주소를 가리키는 포인터</span> 포함
  - 포인터를 활용하여 다음에 올 데이터를 <span style="color:red">동적으로 할당</span>해서 연결할 수 있음

<p align="center">
<img src="/assets/img/blog/pointer.png">
</p>

## 포인터 선언

- **포인터의 선언 및 초기화**
  - 포인터 선언: <span style="color:red">data_type</span><span style="color:blue">*</span> <span style="color:green">pointer<span>;
  - 변수의 주소 대입: <span style="color:green">pointer</span> = <span sytle="color:blue">&</span><span style="color:purple">variable</span>;
    - variable은 int형
    - pointer는 사용하기 전에 위와 같이 초기화를 해주어야 함

<p align="center">
<img src="/assets/img/blog/pointer_declaration.png">
</p>

## 포인터 관련 연산자 활용

- **& 연산자: 변수의 메모리 주소를 반환**
  - <span style="color:blue">int</span> i = 10; <span style="color:blue">int*</span> p = &i;

- *** 연산자**
  - 1) 포인터가 가리키는 곳의 내용을 반환
    - printf("%d", *p); // p가 가리키고 있는 i의 값 10출력
  - 2) 포인터가 가리키는 곳에 값을 할당
    - *p = 20; // p가 가리키고 있는 i에 20을 씀

<p align="center">
<img src="/assets/img/blog/pointer_related_operation.png">
</p>

## 포인터와 객체

- **클래스 객체 멤버의 접근**
  - 객체 변수: "."연산자를 통해 접근
  - 객체 포인터: "->"연산자를 통해 접근

<p align="center">
<img src="/assets/img/blog/pointer_and_object.png">
</p>

## 자기참조 클래스 (or 구조체)

- **자기참조 클래스 (self-referential class)**
  - 멤버 변수 중에서 자기 자신과 동일한 클래스 객체를 가리키는 포인터를 가지는 클래스(구조체)
  - 동적으로 객체를 생성해 이들을 포인터로 연결하게 해줌
  - 리스트, 트리 등을 구성할 때 많이 쓰임

<p align="center">
<img src="/assets/img/blog/self_referential_class.png">
</p>

## 정적 메모리

- **정적 메로리 할당**
  - 메모리의 크기는 프로그램이 시작하기 전에 결정
  - 실행 도중에 크기를 변경할 수 없다
    - 더 큰 입력이 들어온다면 처리하지 못함
    - 더 작은 입력이 들어온다면 메모리 공간 낭비

~~~cpp
int i;      // int형 변수 i를 정적으로 할당
int* p;     // 포인터 변수 p를 정적으로 할당
int A[10];  // 길이가 10인 배열을 정적으로 할당
~~~

- **프로그램 실행 중에는 배열의 크기를 변경할 수 없음!**

~~~cpp
int n = 10;
int B[n];   // 컴파일 오류
~~~

## 동적 메모리

- **동적 메모리 할당**
  - 실행 도중에 메모리를 할당 받는 것으로 필요한 만큼만 할당을 받고 반납함
  - 메모리를 효율적으로 필요한 만큼만 사용가능
  - 동적 메모리 관련 keyword
    - new: 메모리 할당
    - delete: 메모리 해제

- **포인터와 동적 메모리 할당**
  - 동적으로 할당된 메모리는 반드시 포인터에 저장

## 동적 메모리 할당/해제 방법

- **new 연산자**
  - data_type* pData = new data_type;
  - data_type* array = new data_type[size];
    - char* pc = new char[100]; // char형 100개의 메모리 할당
    - int* pi = new int; // int형 1개의 메모리 할당
    - Book* pb = new Book; // Book객체 1개의 메모리 할당

- **delete 연산자**
  - <span style="color:red">동적으로 할당한 메모리는 반드시 해제해야함!</span>
    - delete pData;
    - delete[] array;

## 동적 메모리 할당 예제

~~~cpp
int main()
{
  int x;                    // 정적으로 int 객체 할당
  int* py = new int;        // 동적으로 int 객체 할당
  x = 10;
  *py = 20;
  delete py;                // 동적으로 int 객체 제거
  py = NULL;

  int arrA[20];             // 정적으로 배열 할당
  int* arrB = new int[20];  // 동적으로 배열 할당
  arrA[3] = 10;             // 정적 배열의 사용
  arrB[3] = 20;             // 동적 배열의 사용
  delete[] arrB;            // 동적으로 배열 제거
  arrB = NULL;

  return 0;
}                           // 정적 객체(x, arrA) 자동 해제
~~~

## 포인터와 연결된 표현

- **Linked Representation**
  - 항목들을 노드(node)라고 하는 곳에 저장
  - 다음 노드를 가리키는 주소(포인터)도 같이 저장
    - 노드(node): <항목, 주소> 쌍
  - 노드는 데이터 필드와 링크 필드로 구성
    - 데이터 필드 - 리스트의 원소, 즉 데이터의 값을 저장하는 곳
    - 링크 필드 - 다음 노드의 주소 값을 저장하는 장소(포인터)
  - 메모리 안에서의 노드의 물리적 순서가 리스트의 논리적 순서와 일치할 필요 없음

<p align="center">
<img src="/assets/img/blog/linked_representation.png">
</p>

## 연결된 표현 장단점

- **장점**
  - 중간 부분에 아이템 삽입/삭제가 배열에 비해 용이함
  - 연속된 메모리 공간이 필요 없으며 크기 제한이 없음

- **단점**
  - 포인터를 다루기 때문에 포인터 처리 관련 세심한 구현을 요구함
  - 포인터 변수의 추가 저장 공간을 요구

<p align="center">
<img src="/assets/img/blog/linked_representation_insert_example.png">
</p>

## 연결된 표현(연결 리스트)의 구조

- **노드(LinkedNode)**

<p align="center">
<img src="/assets/img/blog/linked_node.png">
</p>

- **헤드 포인터(head pointer)**
  - 리스트의 첫 번째 노드를 가리키는 포인터 변수

<p align="center">
<img src="/assets/img/blog/head_pointer.png">
</p>

## 연결 리스트의 종류

- **단순 연결 리스트(singly linked list)**

<p align="center">
<img src="/assets/img/blog/head_pointer.png">
</p>

- **원형 연결 리스트(circular linked list)**

<p align="center">
<img src="/assets/img/blog/circular_linked_list.png">
</p>

- **이중 연결 리스트(doubly linked list)**

<p align="center">
<img src="/assets/img/blog/doubly_linked_list.png">
</p>

## 연결된 표현의 활용

- **연결 리스트**

- **연결 리스트로 구현한 스택**

- **연결 리스트로 구현한 큐**

<p align="center">
<img src="/assets/img/blog/utilization_of_linked_representation.png">
</p>

## What You Need To Know

- **미로탐색을 위한 BFS 알고리즘**
  - 시작점에서 인접한 모든 위치들을 <span style="color:blue">먼저 방문</span>하고 방문한 점을 다시 시작점으로 탐색 반복

- **포인터 리뷰**
  - 포인터 선언/연산자/객체/동적 할당/해제

- **포인터와 연결된 표현**
  - 포인터를 활용하면 자료를 연결된 형태로 표현 가능
  - 동적으로 자룔르 할당 가능하여 담을 수 있는 자료의 크기에 한계가 없음
  - 포인터를 저장할 추가 공간이 들고 정교한 구현이 요구됨