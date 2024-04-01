---
layout: post
title: Priority Queue (1)
description: |
  이진 힙을 기반으로 한 우선순위 큐의 개념과 주요 연산에 대한 설명을 포함한 자료구조 개념 정리입니다. 이진 힙은 완전 이진 트리로 구성되며, insert와 remove 연산을 통해 우선순위 큐를 유지합니다. 이를 통해 우선순위에 따라 데이터를 효율적으로 관리할 수 있습니다.
categories: 자료구조
sitemap: false
hide_last_modified: true
---

# Priority Queue (1)

## 우선순위 큐의 개념과 ADT

### 우선순위 (Priority)

- **실생활/컴퓨터에서 우선순위의 개념**
  - 도로에서 차량의 우선순위
    - 구급차/소방차와 같은 긴급 차량은 일반 차량보다 높은 우선순위
  - 네트워크 패킷의 우선순위
    - 네트워크 관리 패킷은 일반 패킷보다 높은 우선순위

<p align="center">
<img src="/assets/img/blog/concept_of_priority.png">
</p>

### 우선순위 큐 (Priority Queue)

- **우선순위 큐 (Priority Queue, PQ)**
  - 우선순위의 개념을 큐에 적용한 자료구조
    - 우선순위를 가진 데이터를 저장하여 우선순위가 높은 데이터가 먼저 나가게 됨

|**자료구조**|**pop되는 요소**|
|:---:|:---:|
|**스택**|가장 마지막에 들어온 데이터|
|**큐**|가장 먼저 들어온 데이터|
|**우선순위 큐**|가장 우선순위가 높은 데이터|

  - 가장 일반적인 큐 (PQ로 스택이나 큐 구현 가능)
    - **스택**: 가장 늦게 들어온 데이터를 가장 높은 우선순위로 삼는다
    - **큐**: 먼저 들어온 데이터를 가장 높은 우선순위로 삼는다

### 우선순위 큐의 응용

- **우선순위대로 처리해야 하는 모든 분야에 활용**
  - 시뮬레이션
  - 네트워크 트래픽 제어
  - OS 작업 스케줄링
  - Dijkstra's algorithm
    - finding single source shortest paths in graphs

<p align="center">
<img src="/assets/img/blog/application_of_priority_queue.png">
</p>

### 우선순위 큐의 ADT

- **데이터**
  - 우선순위를 가진 요소들의 모음
    - item = <key, vale, priority> //formal
    - item = <priority> // simple - key = value = priority

- **주요 연산**
  - insert(item): 우선순위 큐에 item을 추가
  - remove(): 우선순위가 가장 높은 요소를 삭제하고 반환
  - find(): 우선순위가 가장 높은 요소를 삭제하지 않고 반환

- **우선순위 큐의 종류**
  - 최소 우선순위 큐: 우선순위가 작을 수록 우선순위가 높음
  - 최대 우선순위 큐: 우선순위가 클 수록 우선순위가 높음

### 우선순위 큐의 구현 방법

- **배열을 이용해서 구현**
  - 정렬되지 않은 배열
    - insert: 제일 마지막에 원소 삽입 $$ O(1) $$
    - remove: 모든 원소를 살펴 제일 우선순위가 높은 데이터 삭제 $$ O(n) $$
  - 정렬된 배열 (우선순위가 높은 원소가 tail 쪽에 위치)
    - insert: 정렬을 유지하기 위해 삽입 위치 탐색 $$ O(n) $$
    - remove: 제일 마지막 원소 삭제 $$ O(1) $$
  
<p align="center">
<img src="/assets/img/blog/implementation_of_priority_queue.png">
</p>

- **연결 리스트를 이용해서 구현**
  - 정렬되지 않은 리스트
    - insert: 첫 번째 노드로 삽입 $$ O(1) $$
    - remove: 모든 원소를 살펴 제일 우선순위가 높은 데이터 삭제 $$ O(n) $$
  - 정렬된 리스트 (우선순위가 높은 원소가 head 쪽에 위치)
    - insert: 정렬을 유지하기 위해 삽입 위치 탐색 $$ O(n) $$
    - remove: 첫 번째 원소 삭제 $$ O(1) $$
  
<p align="center">
<img src="/assets/img/blog/implementation_of_priority_queue_linked_list.png">
</p>

- **우선순위 큐의 insert와 remove를 동시에 더 효율적으로 할 수 있는 방법은 없을까?**
  - 힙 (heap)

|구현 방법|insert|remove|
|:---:|:---:|:---:|
|순서없는 배열|$$ O(1) $$|$$ O(n) $$|
|순서없는 연결 리스트|$$ O(1) $$|$$ O(n) $$|
|정렬된 배열|$$ O(n) $$|$$ O(1) $$|
|정렬된 연결 리스트|$$ O(n) $$|$$ O(1) $$|
|힙|$$ O(\log n) $$|$$ O(\log n) $$|

### 우선순위 큐의 종류

- 우선순위 큐는 그 활용도가 광범위 해서 목적 및 구현 방법에 따라 다양한 variants가 존재
  - 교과서에서는 가장 간단한 버전인 binary heap을 공부

<p align="center">
<img src="/assets/img/blog/variants_of_priority_queue.png">
</p>

<a href="https://en.wikipedia.org/wiki/Heap_(data_structure)">https://en.wikipedia.org/wiki/Heap_(data_structure)</a>

## 이진 힙(binary heap)을 기반으로 한 우선순위 큐 연산

### Heap

- **실생활에서 heap은 더미라고 불림**

- **자료구조에서 heap은 heap property를 만족하는 "완전 이진 트리"를 말함 (binary heap)**
  - <span style="color:red">**조건 1)** Heap property?</span>
  - <span style="color:red">**조건 2)** 완전이진트리 (Complete binary tree)?</span>

<p align="center">
<img src="/assets/img/blog/heap.png">
</p>

### Heap Property

- **Max Heap Property (최대 우선순위 큐)**
  - 부모 노드의 priority는 자식 노드의 priority 보다 크거나 같아야 함
    - 중복되는 priority 허용

$$ priority(parent) >= priority(child) $$

- **Min Heap Property (최소 우선순위 큐)**
  - 부모 노드의 priority는 자식 노드의 priority 보다 작거나 같아야 함
    - 중복되는 priority 허용

$$ priority(parent) <= priority(child) $$

### Types of Heap

- **Max/Min Heap**
  - Max (Min) Heap은 최대 (최소) 우선순위큐를 위한 완전이진트리
  - 본 강의에서는 Max Heap을 중점적으로 다룸

<p align="center">
<img src="/assets/img/blog/types_of_heap.png">
</p>

### Complete Binary Tree

- **완전 이진 트리**
  - 높이가 $$ h $$일 때 레벨 1부터 $$ h - 1 $$까지는 노드가 모두 채워짐
  - 마지막 레벨 $$ h $$에서는 노드가 왼쪽에서 오른쪽으로 순서대로 채워짐

<p align="center">
<img src="/assets/img/blog/complete_binary_tree_2.png">
</p>

  - **Heap을 완전 이진 트리로 유지했을 때 장점**
    - Heap의 높이를 최소로 만들 수 있음 (height of complete tree: $$ log n $$)
    - 트리내 노드가 순서대로 차기 때문에 배열로 구현할 때 중간에 빈 공간이 없음

- **완전 이진 트리**
  - 일반적으로 중간에 비어 있는 요소가 없기 때문에 배열로 구현
  - 구현을 간단하게 하기 위해서 **root의 index를 1로 할당**
    - 0번 째 index는 사용하지 않음 (교재버전)

<p align="center">
<img src="/assets/img/blog/complete_binary_tree_1.png">
</p>

### Definition of Binary Heap

- **Binary Heap**
  - Heap property를 만족하는 **완전 이진 트리**
  - Max heap: max heap property 만족, 최대 우선순위 큐
  - Min heap: min heap property 만족, 최소 우선순위 큐
  - 일반적으로 배열로 구현하며 여기서는 priority만 저장

- **Operations**
  - **find():** 우선순위가 가장 높은 요소를 삭제하지 않고 반환
    - Root node에 있는 값을 리턴하면 됨
  - **insert(item):** 우선순위 큐에 항목 item = <priority>을 추가
  - **remove():** 우선순위 큐로부터 가장 우선순위가 높은 요소를 삭제하고 반환

### Insert in Binary Heap

- **Insert**
  - Item x = \<priority\>를 heap에 insert

<p align="center">
<img src="/assets/img/blog/insert_in_binary_heap.png">
</p>

- **<span style="color:blue">Up-heap operation</span>**
  - **Step 1.** Heap의 제일 마지막에 입력 항목을 추가
    - The bottom level of the heap at the leftmost open space
  - **Step 2.** 부모와 추가된 항목의 우선순위를 비교
    - 부모와 자식이 올바른 순서로 존재하면 stop
    - 아니면 부모와 자식 노드를 swap하고 Step 2반복
  - 멈출 때 까지 상위 레벨로 올라가는 형상이기 때문에 up-heap이라고 함 (bubble-up, heapify-up)

- **Priority가 15인 노드를 insert하는 경우 (up-heap)**
  - **Step 1.** Heap의 제일 마지막에 입력 항목을 추가
    - The bottom level of the heap at the leftmost open space
  - **Step 2.** 부모와 추가된 항목의 우선순위를 비교
    - 부모와 자식이 올바른 순서로 존재하면 stop
    - 아니면 부모와 자식 노드를 swap하고 Step 2반복

<p align="center">
<img src="/assets/img/blog/insert_in_binary_heap_1.png">
</p>

~~~python
def insert(priority):
  size <- size + z
  i <- size
  nodes[i] <- priority

  while i != 1 and nodes[i] > nodes[PARENT(i)]:
    // up-heap(i)
    swap nodes[i] and nodes [PARENT(i)]
    i <- PARENT(i)
~~~

<p align="center">
<img src="/assets/img/blog/insert_in_binary_heap_2.png">
</p>

### Remove in Heap

- **Remove**
  - 우선순위가 가장 높은 원소 삭제 = 루트 노드 삭제

- **Down-heap operation**
  - **Step 1.** 마지막 레벨의 가장 오른쪽에 있는 노드를 루트로 대체
  - **Step 2.** 루트를 시작으로 양쪽 자식과 우선순위 비교
    - 부모와 자식들이 올바른 순서로 존재하면 stop
    - 아니면 부모와 자식 노드를 swap하고 Step 2반복
      - Max-heap: 양쪽 자식 중 제일 큰 우선순위를 가지는 자식의 부모와 swap
      - Min-heap: 양쪽 자식 중 제일 작은 우선순위를 가지는 자식이 부모와 swap
  - 멈출 때 까지 하위 레벨로 내려가는 형상이기 때문에 down-heap이라고 함 (bubble-down, heapify-down)

- **Max Heap에서 remove를 한 경우**
  - **Step 1.** 마지막 레벨의 가장 오른쪽에 있는 노드를 루트로 대체
  - **Step 2.** 루트를 시작으로 자기 자식과 우선순위 비교
    - 부모와 자식이 올바른 순서로 존재하면 stop
    - 아니면 부모와 자식 노드를 swap하고 Step 2반복
      - Max-heap: 양쪽 자식 중 제일 큰 우선순위를 가지는 자식의 부모와 swap

<p align="center">
<img src="/assets/img/blog/remove_in_heap.png">
</p>

~~~python
def remove():
  highest <- nodes[1] // store root
  nodes[1] <- nodes[size] // step 1
  size <- size - 1
  down-heap(1) // step 2

  return highest

def down-heap(i):
  left <- LEFT(i)
  right <- RIGHT(i)
  largest <- i

  if left <= size and nodes[left] > nodes[largest]:
    largest <- left
  
  if right <= size and nodes[right] > nodes[largest]:
    largest <- right

  if largest != i:
    swap nodes[i] and nodes[largest]
    down-heap(largest)
~~~

### Remove Example

<p align="center">
<img src="/assets/img/blog/remove_example.png">
<img src="/assets/img/blog/remove_example_1.png">
<img src="/assets/img/blog/remove_example_2.png">
</p>

### Complexity of Heap

- **n을 heap에 저장되어 있는 아이템의 수라고 했을 때**

- **Time complexity of insert: $$ O(h) = O(\log n) $$**
  - Up-heap는 최대 높이 $$ h $$번 만큼 위로 올라가면서 연산 수행
  - Heap은 완전 이진 트리로 $$ O(\log n) $$의 높이를 가짐

- **Time complexity of remove: $$ O(h) = O(\log n) $$**
  - Down-heap는 최대 높이 $$ h $$번 만큼 아래로 내려가면서 연산 수행

### What You Need To Know

- **우선순위 큐와 이진 힙의 개념**
  - 우선순위의 개념을 큐에 적용한 자료구조
  - 이진 힙은 heap property를 만족하는 완전 이진 트리
    - Max heap property: priority(parent) >= priority(children)

- **이진 힙의 주요 연산**
  - Insert
    - 마지막에 노드 삽입 후 up-heap을 통해 heap 구조를 맞춤
  - Remove
    - 마지막 노드를 root로 대체 후 down-heap을 통해 heap 구조를 맞춤
  - 완전 이진 트리이기 때문에 각각 $$ O(\log n) $$ 시간 복잡도를 가짐