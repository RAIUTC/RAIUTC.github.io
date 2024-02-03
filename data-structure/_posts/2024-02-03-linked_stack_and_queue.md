---
layout: post
title: Linked Stack & Queue
description: |
  이 글은 포인터를 활용하여 스택(Stack)과 큐(Queue)를 LinkedStack 및 LinkedQueue로 구현하는 방법을 다룹니다. 
  주요 연산의 시간 복잡도는 O(1)로 효율적입니다. 
  포인터 기반 구현의 장점으로는 동적 데이터 추가가 가능하며, 특히 큐의 경우 더 간결한 구현이 가능합니다. 
  그러나 동적 할당 및 해제와 같은 포인터 처리에 대한 추가 작업과 저장 공간의 증가가 단점으로 소개됩니다.
categories: 자료구조
sitemap: false
hide_last_modified: true
---

# Linked Stack & Queue

## 스택 구현 방식

- **배열 vs 연결 리스트**
  - ArrayStack: 배열에 데이터를 담고 top(int형 변수)로 상단의 인덱스를 저장함
  - LinkedStack: Node들을 연결해 데이터를 담고 top(Node 포인터)로 상단을 가리킴

<p align="center">
<img src="/assets/img/blog/array_stack_vs_linked_stack.png">
</p>

## 스택 주요 연산: Push

- **Case 1) Stack이 비어있는 경우**
  - Step 1. top이 새로운 노드를 가리키게 함

- **Case 2) Stack이 비어있지 않은 경우**
  - Step 1. 새로운 노드 p가 top이 가리키는 노드를 가리키게 함
  - Step 2. top이 새로운 노드를 가리키게 함

<p align="center">
<img src="/assets/img/blog/linked_stack_operation_push.png">
</p>

## 스택 주요 연산: Pop

- **Case 1) Stack이 비어있는 경우**
  - Step 1. pop할 노드가 없으므로 error 처리한다

- **Case 2) Stack이 비어있지 않은 경우**
  - Step 1. 임시 포인터 p가 top이 가리키는 노드를 가리키게 한다
  - Step 2. top이 그 다음 노드를 가리키게 한다 (top = p -> link;)
  - Step 3. p가 가리키고 있는 노드의 데이터를 반환(return)하고 동적해제 한다

<p align="center">
<img src="/assets/img/blog/linked_stack_operation_pop.png">
</p>

## LinkedStack의 구현

- **학생 정보를 담는 stack class를 연결된 표현으로 구현**
  - Student class의 객체를 데이터로 저장
  - 주요 연산: push & pop

~~~cpp
class Student {
private:
  int id;
  string name;
  string dept;
public:
  Student(int id, const string& name, const string& dept){
    this->id = id;
    this->name = name;
    this->dept = dept;
  }
  void display(){
    cout << "id: " << id << "\t" << "name: " << name << "\t";
    cout << "dept: " << dept << endl;
  }
};
~~~

- **(Linked) Node Class**

~~~cpp
class Node{
private:
  Student data;
  Node* link;
public:
  Node(const Student& in_data) : data(in_data) {
    this -> link = nullptr;
  }
  Node* get_link(){
    return this->link;
  }
  void set_link(Node* p){
    this->link = p;
  }
  Student get_data(){
    return data;
  }
};
~~~

- **LinkedStack Class**

<p align="center">
<img src="/assets/img/blog/linked_stack_operation_push.png">
</p>

~~~cpp
class LinkedStack{
private:
  Node* top;
public:
  LinkedStack(){
    this->top = nullptr;
  }
  bool empty(){
    return this->top == nullptr;
  }
  void push(const Student& data){
    if(this->empty())
      this->top = new Node(data);
    else{
      Node* p = new Node(data);
      p->set_link(this->top);
      this->top = p;
    }
  }
  Student pop(){
    if(this->empty()){
      throw "error: stack is empty";
    }else{
      Node* p = this->top;                // step 1
      this->top = this->top->get_link();  // step 2
      Student data = p->get_data();       // step 3
      if(p != nullptr) delete p;          // step 3
      return data;
    }
  }
~~~

<p align="center">
<img src="/assets/img/blog/linked_stack_operation_pop.png">
</p>

~~~cpp
  ~LinkedStack(){
    while(!this->empty()){
      this->pop();
    }
  }
  void display(){
    for(Node* p = top; p != nullptr; p = p->get_link())
      p->get_data().display();
  }
};
~~~

<p align="center">
<img src="/assets/img/blog/linked_stack_class.png">
</p>

## LinkedStack의 사용

~~~cpp
int main() {
  LinkedStack stack;
  stack.push(Student(201513007, "Sara", "CSE"));
  stack.push(Student(201512351, "Jin", "Law"));
  stack.push(Student(201528339, "Kei", "Music"));

  cout << "[LinkedStack]" << endl;
  stack.display();
  cout << endl;

  Student top = stack.pop();
  cout << "[Popped Item]" << endl;
  top.display();
  cout << endl;

  cout << "[LinkedStack]" << endl;
  stack.display();
  cout << endl;

  return 0;
}
~~~

<p align="center">
<img src="/assets/img/blog/use_of_linked_stack.png">
</p>

## 큐 구현 방식

- **배열 vs 연결 리스트**
  - CircularQueue: 배열에 데이터를 담고 front/rear (int형 변수)로 전단/후단의 인덱스를 가리킴
  - LinkedQueue: Node들을 연결해 데이터를 담고 front/rear (Node 포인터)로 전단/후단을 가리킴

<p align="center">
<img src="/assets/img/blog/linked_queue_implementation.png">
</p>

## 큐 주요 연산: Enqueue

- **Case 1) Queue가 비어있는 경우**
  - Step 1. front/rear 포인터가 새로운 노드를 가리키게 한다.

- **Case 2) Queue가 비어있지 않은 경우**
  - Step 1. rear가 가리키는 마지막 노드가 새로운 노드를 가리키게 한다
    - rear -> link = p;
  - Step 2. rear가 새로운 노드를 가리키게 한다 (rear = p;)

<p align="center">
<img src="/assets/img/blog/ linked_queue_operation_enqueue.png">
</p>

## 큐 주요 연산: Dequeue

- **Case 1) Queue에 노드가 하나도 없는 경우: error처리**

- **Case 2) Queue에 노드가 하나만 있는 경우**
  - Step 1. front가 가리키는 노드의 데이터를 반환하고 해당 노드는 해제
  - Step 2. front와 rear는 nullptr로 둔다

<p align="center">
<img src="/assets/img/blog/linked_queue_operation_dequeue_case_two.png">
</p>

- **Case 3) Queue에 노드가 2개 이상인 경우**
  - Step 1. 임시 포인터 p를 front가 가리키는 노드를 가리키게 한다
  - Step 2. front가 그 다음 노드를 가리키게 한다
  - Step 3. p가 가리키는 노드의 데이터를 반환하고 해당 노드 해제

<p align="center">
<img src="/assets/img/blog/linked_queue_operation_dequeue_case_three.png">
</p>

## LinkedQueue의 구현

- **학생 정보를 담는 queue class를 연결된 표현으로 구현**
  - Student class의 instance를 데이터로 저장
  - 주요 연산: enqueue & dequeue

- **Student class와 Node class는 LinkedStack에서 사용했던 것과 동일**

- **LinkedQueue Class**

~~~cpp
class LinkedQueue{
private:
  Node* front;
  Node* rear;
public:
  LinkedQueue(){
    this->front = this->rear = nullptr;
  }
  bool empty(){
    return this->front == nullptr;
  }
  ~LinkedQueue(){
    while(!this->empty())
      this->dequeue();
  }
  void display(){
    for(Node* p = front; p != nullptr; p = p->get_link())
      p->get_data().display();
  }
  void enqueue(const Student& data){
    if(this->empty()){
      this->front = this->rear = new Node(data);
    }else{
      Node* p = new Node(data);
      this->rear->set_link(p);
      this->rear = p;
    }
  }
~~~

<p align="center">
<img src="/assets/img/blog/linked_queue_operation_enqueue_case_one_and_two_implementation.png">
</p>

~~~cpp
  Student dequeue(){
    if(this->empty()){                      // case 1
      throw "error: queue is empty";
    }else{                                  // case 2 & 3
      Node* p = this->front;
      this->front = this->front->get_link();
      Student data = p->get_data();
      if(p != nullptr) delete p;
      if(this->front == nullptr) 
        this->rear = nullptr;
      return data;
    }
  }
};
~~~

<p align="center">
<img src="/assets/img/blog/linked_queue_operation_dequeue_implementation_case_two_and_three.png">
</p>

## LinkedQueue의 사용

~~~cpp
int main() {
  LinkedQueue queue;
  queue.enqueue(Student(201513007, "Sara", "CSE"));
  queue.enqueue(Student(201512351, "Jin", "Law"));
  queue.enqueue(Student(201528339, "Kei", "Music"));

  cout << "[LinkedQueue]" << endl;
  queue.display();
  cout << endl;

  Student front = queue.dequeue();
  cout << "[Dequeued Item]" << endl;
  front.display();
  cout << endl;

  cout << "[LinkedQueue]" << endl;
  queue.display();
  cout << endl;

  return 0;
}
~~~

<p align="center">
<img src="/assets/img/blog/use_of_linked_queue.png">
</p>

## What You Need To Know

- **포인터를 활용하여 stack와 queue를 구현**
  - LinkedStack & LinkedQueue
  - 주요 연산의 시간 복잡도: $$O(1)$$

- **포인터를 기반으로 구현 했을 때 장단점**
  - **장점**
    - 정해진 크기 없이 데이터를 동적으로 추가 가능
    - 큐와 같은 경우 구현이 좀 더 간결함
  - **단점**
    - 포인터에 대한 처리 추가 필요 (동적 할당/해제)
    - 포인터를 저장하기 위한 추가 공간 필요