---
layout: post
title: Priority Queue (2)
description: |
  
categories: 자료구조
sitemap: false
hide_last_modified: true
---

# Priority Queue (2)

## Binary Heap class 구현

### Max Heap

- **Max heap property를 만족하는 완전이진트리**
  - find(): 우선순위가 가장 높은 요소를 삭제하지 않고 반환
  - insert(item): 우선순위 큐에 item=\<priority\>을 추가
  - remove(): 가장 우선순위가 높은 요소를 삭제하고 반환

<p align="center">
<img src="/assets/img/blog/max_heap.png">
</p>

### MaxHeap Class

~~~cpp
class MaxHeap{
private:
  static const int root_index = 1;
  static const int HEAP_SIZE = 200;
  int nodes[HEAP_SIZE];
  int size;
  int LEFT(int i) { return i * 2; }
  int RIGHT(int i) {return i * 2 + 1; }
  int PARENT(int i) { return i / 2; }
public:
  MaxHeap() : size(0) { }

  bool empty() { return this->size == 0; }

  bool full() { return this->size == HEAP_SIZE - 1; }

  int find(){
    if(empty()) throw "error: heap is empty";
    return nodes[root_index];
  }
};
~~~

### MaxHeap Class: insert

~~~cpp
public:
  void MaxHeap::insert(int priority){
    if(full()) throw "error: heap is full";

    size++;
    int i = size;
    nodes[i] = priority;

    up_heap(i);
  }

private:
  void Max_Heap::up_heap(int i){
    if(i != root_index){
      if(nodes[i] > nodes[PARENT(i)]){
        swap(nodes[i], nodes[PARENT(i)]);
        up_heap(PARENT(i));
    }
  }
~~~

### MaxHeap Class: remove

~~~cpp
public:
  int MaxHeap::remove(){
    if(empty()) throw "error: heap is empty";
    int highest = nodes[root_index];
    nodes[root_index] = nodes[size--];
    down_heap(root_index);
    return highest;
  }
private:
  void MaxHeap::down_heap(int i){
    int left = LEFT(i);
    int right = RIGHT(i);
    int largest = i;
    if(left <= size && nodes[left] > nodes[largest])
      largest = left;
    if(right <= size && nodes[right] > nodes[largest])
      largest = right;
    if(largest != i){
      swap(nodes[i], nodes[largest]);
      down_heap(largest);
    }
  }
~~~

## Other operations in Heap

### Other Operations in Heap

- **decrease-key(key, decrement)**
  - 입력 key를 가지는 노드의 priority를 decrement만큼 감소

- **increase-key(key, increment)**
  - 입력 key를 가지는 노드의 priority를 increment만큼 증가

- **여기서부터는 item은 \<key, priority\>로 구성된다고 가정**
  - key는 노드 별로 고유하다고 가정 (priority로 heap 연산 수행)
  - key의 범위는 1 <= key <= size 이라 가정

<p align="center">
<img src="/assets/img/blog/heap_operations.png">
</p>

### decrease-key

- **decrease-key(key, decrement)**
  - **Step 1.** key를 가지는 노드의 index를 찾음
  - **Step 2.** 해당 노드의 priority을 decrement만큼 감소
  - **Step 3.** 해당 index로부터 down-heap을 함

<p align="center">
<img src="/assets/img/blog/decrease_key.png">
<img src="/assets/img/blog/decrease_key_2.png">
<img src="/assets/img/blog/decrease_key_3.png">
</p>

### increase-key

- increase-key(key, increment)
  - **Step 1.** key를 가지는 노드의 index를 찾음
  - **Step 2.** 해당 노드의 priority을 increment만큼 더함
  - **Step 3.** 해당 index로부터 up-heap을 함

<p align="center">
<img src="/assets/img/blog/increase_key.png">
<img src="/assets/img/blog/increase_key_2.png">
<img src="/assets/img/blog/increase_key_3.png">
</p>

### Code for decrease/increase-key

~~~cpp
class Node{
  friend class MaxHeap;
  int key;
  int priority;
};
// MaxHeap의 nodes 배열은 Node 객체를 가지는 것으로 변경되었다 가정
// MaxHeap에 std::vector<int> indicies가 추가되어 key에 대응되는 index 관리
void MaxHeap::decrease_key(int key, int decrement){
  int i = indices[key];
  nodes[i].priority -= decrement;
  down_heap(i);
}
void MaxHeap::increase_key(int key, int increment){
  int i = indices[key];
  nodes[i].priority += increment;
  up_heap(i);
}
~~~

### Details for decrease/increase-key

- **Time complexity of decrease/increase-key**
  - 둘 다 최악의 경우 $$ O(\log n) $$의 시간 복잡도를 가짐
    - Step 1. key를 가지는 노드의 index를 찾음 &rarr; $$ O(1) $$
      - indices는 vector이므로 indices\[key\]는 $$ O(1) $$이 소요
    - Step 2. 해당 노드의 priority를 decrement/increment 만큼 뺌/더함 &rarr; $$ O(1) $$
    - Step 3. 해당 index로부터 down-heap/up-heap을 함 &rarr; $$ O(\log n) $$

- **Implementation details**
  - 노드가 추가/삭제 되거나 두 노드가 swap되면 indices\[key\]도 업데이트
    - insert/remove 함수에 indices\[key\] 관련 처리 추가
      - **insert**: indices\[key\] = size; &emsp; **remove**: indices\[key\] = 0; //dummy
    - swap 함수를 새로 구현해서 노드의 항목 swap 뿐 아니라 indices도 같이 swap

~~~python
def myswap(i, j):
  std::swap(indices[nodes[i].key], indices[nodes[j.key]])
  std::swap(nodes[i], nodes[k])
~~~

## Heap 응용: Heapsort

### Heap Sort

- **정렬 문제**
  - 입력: n의 크기를 가지는 배열 (순서는 섞여 있음)
  - 출력: 배열의 원소를 특정 순서로 정렬
    - 오름차순: 작은 값이 앞에 나와 뒤로 갈수록 커짐
    - 내림차순: 큰 값이 앞에 나와 뒤로 갈수록 작아짐

<p align="center">
<img src="/assets/img/blog/heapsort.png">
</p>

- **Heap sort: heap을 이용하여 정렬**
  - 먼저 정렬해야 할 n개의 요소들을 heap에 삽입 &rarr; $$ O(n\log n) $$ 시간
  - 한번에 하나씩 요소를 heap에서 삭제 후 출력 &rarr; $$ O(n\log n) $$ 시간
  - Max heap &rarr; 내림차순, Min heap &rarr; 오름차순

<p align="center">
<img src="/assets/img/blog/heapsort_2.png">
</p>

## STL 우선순위 큐 사용방법

### Priority Queue in STL

- **#include\<prioriry_queue\>**
  - 기본적으로 MaxHeap에 대응
    - priority_queue\<int\> Q;
  - MinHeap으로 하려면 아래와 같이 선언
    - priority_queue\<int, std::vector\<int\>, std::greater\<int\>\> Q;

- **Main operations**
  - push: insert 함수에 대응
  - pop: remove 함수에 대응 (반환은 없음)
  - top: find 함수에 대응

- **Reference**

<a href="https://en.cppreference.com\w\cpp\container\priority_queue">https://en.cppreference.com\w\cpp\container\priority_queue</a>

### Priority Queue in STL

~~~cpp
#include <functional>
#include <priority_queue>
#include <vector>

template<typename T>
void print_queue(T& q){
  while(!q.empty()){
    std::cout << q.top() << " ";
    q.pop();
  }
  std::cout << endl;
}

int main(){
  std::priority_queue<int> q;
  for(int n : {1, 8, 5, 6, 3, 4, 0, 9, 7, 2})
    q.push(n);
  print_queue(q);

  return 0;
}
~~~

### What You Need To Know

- **decrease/increase-key**
  - 입력 key를 가지는 노드의 priority를 decrement/increment만큼 감소/증가
    - **가정:** key는 unique하고 1 <= key <= size 범위여야 함
    - **Step 1.** key를 가지는 노드의 index를 찾음
    - **Step 2.** 해당 노드의 priority를 decrement/increment만큼 뺌/더함
    - **Step 3.** 해당 index로부터 down-heap/up-heap을 함
  - 시간 복잡도: $$ O(\log n) $$

- **Heao 응용**
  - Heap을 이용하여 입력 배열을 정렬할 수 있음
  - 시간 복잡도: $$ O(n\log n) $$