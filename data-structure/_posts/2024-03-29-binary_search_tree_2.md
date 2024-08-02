---
layout: post
title: Binary Search Tree (2)
description: |
  이진 탐색 트리의 시간 복잡도는 연산에 따라 O(h)이며, 자가 균형 이진 탐색 트리는 삽입 또는 삭제 시 트리의 균형을 자동으로 조절하여 효율적인 데이터 관리를 지원합니다.
categories: 자료구조
sitemap: false
hide_last_modified: true
---

# Binary Search Tree (2)

## 이진 탐색 트리 (Remind)

- **이진 탐색 트리 (Binary Search Tree, BST)**
  - 탐색을 위해 특화된 이진 트리
    - insert, remove, search 등을 효율적으로 하기 위함
  - 모든 노드는 유일한 key를 가지며 루트를 기준으로 왼쪽/오른쪽 서브 트리가 구분됨

<p align="center">
<img src="/assets/img/blog/bst_2.png">
</p>

## 이진 탐색 트리의 ADT

- **데이터**
  - 이진 탐색 트리 (BST)의 정의를 만족하는 이진 트리

- **주요 연산**
  - search(key): key를 가지는 노드(or value)를 찾아 반환
  - insert(key, value): 이진 탐색 트리의 특성을 유지하면서 주어진 key와 value를 가지는 노드를 삽입
    - 이미 트리에 해당 key를 가지는 노드가 있다면 주어진 value로 업데이트
  - remove(key): 이진 탐색 트리의 특성을 유지하면서 key를 가지는 노드를 트리에서 삭제

## 이진 탐색 트리 클래스 설계

<p align="center">
<img src="/assets/img/blog/bst_class.png">
</p>

## BinaryNode Class

~~~cpp
class BinaryNode{
  friend class BinarySearchTree;
private:
  int key;
  int value;
  BinaryNode* left;
  BinaryNode* right;
public:
  BinaryNode(int key = 0,
             int value = 0,
             BinaryNode* left = nullptr,
             BinaryNode* right = nullptr) {
    this->key = key;
    this->value = value;
    this->left = left;
    this->right = right;
  }

  //getters and setters for key, value, left, right

  bool isLeaf(){
    return this->left == nullptr && this->right == nullptr;
  }

  bool hasTwoChildren(){
    return this->left != nullptr && this->right != nullptr;
  }

  bool hasOneChild(){
    bool hasOnlyLeft = this->left != nullptr && this->right == nullptr;
    bool hasOnlyRight = this->left == nullptr && this->right != nullptr;
    return hasOnlyLeft || hasOnlyRight;
  }
};
~~~

## BinaryTree Class

~~~cpp
class BinaryTree{
protected:
  BinaryNode* root;
public:
  BinaryTree(){ this->root = nullptr; }

  ~BinaryTree(){
    removeNodes(this->root);
  }

  bool empty(){ return this->root == nullptr; }

  // see the previous codes for other operations
  // - preorder, inorder, postorder, levelorder
  // - getCount, getLeafCount, getHeight
  // - removeNodes
};
~~~

## BinarySearchTree Class

~~~cpp
class BinarySearchTree : public BinaryTree{
public:
  // if search succeeds, return the node's value
  int search(int key) {
    ...
  }

  void insert(int key, int value) {
    ...
  }

  void remove(int key) {
    ...
  }
};
~~~

## Search in BST

- **Cases for search in BST**
  - Case 1) 탐색 키 (querying key)와 현재 노드의 key가 같은 경우
    - 원하는 값을 찾은 것으로 현재 노드 (or value)를 반환
  - Case 2) 탐색 키가 현재 노드의 key보다 작은 경우
    - 왼쪽 서브트리를 기준으로 다시 search 수행
  - Case 3) 탐색 키가 현재 노드의 key보다 큰 경우
    - 오른쪽 서브트리를 기준으로 다시 search 수행

<p align="center">
<img src="/assets/img/blog/bst_search.png">
</p>

## BinarySearchTree - Search

~~~cpp
public:
  int search(int key){
    BinaryNode* node = search(this->root, key);
    if(node == nullptr) throw "error: out-of-key";
    return node->value;
  }

private:
  BinaryNode* search(BinaryNode* node, int key){
    if(node == nullptr || key == node->key)
      return node;
    else if(key < node->key)
      return search(node->left, key);
    else
      return search(node->right, key);
  }
~~~

## Insert in BST

- **이진 탐색 트리에 원소를 삽입하기 위해서는 먼저 탐색을 수행**
  - 탐색에 실패한 위치가 바로 새로운 노드를 삽입하는 위치
  - 동일한 key를 가지는 경우 주어진 value로 update

<p align="center">
<img src="/assets/img/blog/bst_insert.png">
</p>

## BinarySearchTree - Insert

~~~cpp
public:
  void insert(int key, int value){
    if(empty()) this->root = new BinaryNode(key, value);
    else insert(this->root, key, value);
  }
private:
  void insert(BinaryNode* node, int key, int value){
    if(key == node->key) node->value = value;
    else if(key < node->key){
      if(node->left == nullptr)
        node->left = new BinaryNode(key, value);
      else insert(node->left, key, value);
    }else{
      if(node->right == nullptr)
        node->right = new BinaryNode(key, value);
      else insert(node->right, key, value);
    }
  }
~~~

## Remove in BST

- **Cases for remove in BST**
  - 먼저 삭제하려는 노드를 search를 통해 찾음
  - Case 1) 삭제하려는 노드가 리프 노드인 경우
  - Case 2) 삭제하려는 노드가 왼쪽 또는 오른쪽 서브트리 중 하나만 자식으로 가지고 있는 경우
  - Case 3) 삭제하려는 노드가 두 개의 서브트리를 모두 가지고 있는 경우

<p align="center">
<img src="/assets/img/blog/bst_remove.png">
</p>

## Pseudocode of Remove (recursive)

~~~
def remove(node, parent, key):
  if node == NULL:
    return # Since there is no node with key
  if key < node's key:
    remove(node->left, node, key)
  else if key > node's key:
    remove(node->right, node, key)
  else: # key == node's key
    if node has both left & right children:
      successor = leftmost(node->right)
      replace node with successor & remove successor
    else if node has only a left child:
      replace node in its parent with node->left
    else if node has only a right child:
      replace node in its parent with node->right
    else: # no node has a child
      replace node in its parent with NULL
~~~

## BinarySearchTree - Remove

~~~cpp
public:
  void remove(int key) {
    BinaryNode* node = remove(this->root, nullptr, key);
    if(node == nullptr) throw "error: out-of-key";
    delete node;
  }
private:
  BinaryNode* remove(BinaryNode* node, BinaryNode* parent, int key){
    if(node == nullptr) return nullptr;
    if(key < node->key) return remove(node->left, node, key);
    else if(key > node->key) return remove(node->right, node, key);
    else{ // key == node->key
      if(node->hasTwoChildren()){
        // do something for case 3
      }else if(node->hasOneChild()){
        // do something for case 2
      }else if(node->isLeaf()){
        // do something for case 1
      }
    }
  }
~~~

## Remove - Case 1

~~~cpp
// case 1: node to be removed is a leaf
else if(node->isLeaf()){
  if(node == this->root) this->root = nullptr;
  else{
    if(parent->left == node) parent->left = nullptr;
    else parent->right = nullptr;
  }
  return node;
}
~~~

<p align="center">
<img src="/assets/img/blog/bst_remove_case1.png">
<img src="/assets/img/blog/bst_remove_case1_2.png">
</p>

## Remove - Case 2

~~~cpp
// case 2: node has only one child
else if(node->hasOneChild()){
  BinaryNode* child = (node->left != nullptr) ? node->left : node->right;
  if(node == this->root) this->root = child;
  else{
    if(parent->left == node) parent->left = child;
    else parent->right = child;
  }
  return node;
}
~~~

<p align="center">
<img src="/assets/img/blog/bst_remove_case2.png">
<img src="/assets/img/blog/bst_remove_case2_2.png">
</p>

## Remove - Case 3

~~~cpp
// case 3: node has two children
if(node->hasTwoChildren()){
  BinaryNode* succ = leftmost(node->right);
  node->key = succ->key;
  node->value = succ->value;
  // remove the successor
  succ = this->remove(node->right, node, succ->key);
  return succ;
}
~~~

<p align="center">
<img src="/assets/img/blog/bst_remove_case3.png">
<img src="/assets/img/blog/bst_remove_case3_2.png">
</p>

~~~cpp
BinaryNode* leftmost(BinaryNode* node){
  while(node->left != nullptr)
    node = node->left;
  return node;
}
~~~

<p align="center">
<img src="/assets/img/blog/bst_remove_case3_3.png">
</p>

## 이진 탐색 트리 연산의 시간 복잡도

- **Search 연산의 시간 복잡도**
  - 최선의 경우는 루트에 탐색키가 있는 경우로 $$ O(1) $$
  - 최악의 경우는 탐색키가 트리의 가장 깊은 리프노드에 있는 경우
    - 이 경우 트리의 높이 만큼 이동하게 됨 (즉, $$ O(h) $$번 이동)
    - 따라서, Search 연산의 시간 복잡도는 $$ O(h) $$
  
- **Insert/remove 연산의 시간 복잡도**
  - Insert/remove도 search를 수행하므로 최악의 경우 $$ O(h) $$ 소요
    - 탐색 후 노드를 삽입하는 과정은 $$ O(1) $$
    - 탐색 후 노드를 삭제하는 과정은 Case 1, 2는 $$ O(1) $$가 걸리고 Case 3는 후계자 관련 작업으로 $$ O(h) $$가 걸림

- **BST가 n개의 노드를 가지고 있다는 가정**
  - 최선의 경우 각 연산은 $$ O(1) $$
    - **Search**: 루트에 탐색키가 있는 경우로
    - **Insert**: degenerate tree에서 root의 포인터 중 비어 있는 곳에 삽입되는 경우
    - **Remove**: degenerate tree에서 root를 삭제하는 경우
  - 최악의 경우 각 연산은 $$ O(n) $$
    - 이 때 트리의 모양은 degenerate tree로 높이는 h = n = 1이 되므로 search/insert/remove는 $$ O(n) $$의 시간을 가지게 됨

<p align="center">
<img src="/assets/img/blog/bst_time_complexity.png">
</p>

- **평균적인 경우의 시간복잡도?**
  - 비어있는 BST에 랜덤한 n개의 key가 임의의 순서로 insert 된다고 했을때, 최종적인 BST는 평균적으로 균형 잡힌 트리 (balanced tree)가 됨
    - 균형 잡힌 트리의 정의
      - |왼쪽 서브트리 높이 - 오른쪽 서브트리 높이| <= 1
      - 왼쪽/오른쪽 서브트리가 재귀적으로 균형 잡혀야 함
    - 균형 잡힌 트리는 $$O(log n) $$의 높이를 가지게 됨(예, complete binary tree)
  - 따라서 평균적인 경우에 대해 BST의 주요 연산들을 $$ O(log n) $$ 시간 복잡도를 가짐
    - 이 경우 순차 탐색 보다 빠른 시간을 가짐
    - 엄밀한 증명은 out-of-scope

## Self-Balancing BST의 개념

- **BST는 평균적인 경우에는 $$ O(log n)이지만 입력에 따라 $$ O(n) $$의 시간 복잡도를 가질 수 있음**
  - 입력의 구성이 degenerate tree가 되면 발생

- **최악의 경우에서 BST의 연산이 $$ O(log n)$$의 시간으로 동작하게 할 수 있을까?**
  - Self-Balancing BST는 최악의 경우에도 $$ O(log n) $$을 보장함
    - 예, AVL-Tree, red-black tree
    - 핵심 아이디어는 삽입/삭제에서 트리의 균형이 깨지게 될 때 균형을 맞춰주기

- <a href="https://commons.wikimedia.org/wiki/File:AVL_Tree_Example.gif">https://commons.wikimedia.org/wiki/File:AVL_Tree_Example.gif</a>

## What You Need To Know

- **이진 탐색 트리의 시간 복잡도**
  - 각 연산은 search를 수반하기 때문에 시간 복잡도는 $$ O(h) $$
  - BST가 n개의 노드를 가지고 있을 때
    - 최선의 경우 각 연산의 시간 복잡도는 $$ O(1) $$
    - 최악의 경우 각 연산의 시간 복잡도는 $$ O(n) $$
    - 평균적인 경우 각 연산의 시간 복잡도는 $$ O(log n) $$

- **Self-Balancing BST의 개념**
  - 삽입/삭제에서 트리의 균형이 깨지게 될 때 스스로 균형을 맞춤
