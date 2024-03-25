---
layout: post
title: Binary Search Tree (1)
description: |
  이진 탐색 트리는 왼쪽과 오른쪽 서브트리의 특성을 통해 정렬된 데이터를 관리합니다. 주요 연산으로는 탐색, 삽입, 삭제가 있으며, 이를 통해 데이터를 효율적으로 관리할 수 있습니다.
categories: 자료구조
sitemap: false
hide_last_modified: true
---

# Binary Search Tree (1)

## 탐색 (Search)

- **탐색: 특정 자료구조내에 저장된 정보를 찾아내는 일**
  - 방대하게 저장된 데이터에서 원하는 정보를 <span style="color:blue">효율적으로</span> 찾아내는 것은 중요
  - 예) 구글 검색, 전화번호부에서 전화번호 찾기, 사전에서 단어 검색, 인터넷 쇼핑몰에서 원하는 물건 찾기

<p align="center">
<img src="/assets/img/blog/search.png">
</p>

## 효율적인 탐색

- **n개의 아이템을 가지는 1차원 배열에서 원하는 값을 찾기 위한 가장 간단한 방법은? &rarr; 순차 탐색**
  - 최악의 경우 $$ O(n) $$의 시간 복잡도 요구

- **Insert/remove/search 등을 $$ O(n) $$보다 더 빠르게 할 수 있는 방법은 없을까?**
  - <span style="color:blue">이진 탐색 트리 (탐색을 위해 특화된 이진 트리)</span>
  - 다른 여러가지 방법 및 자료구조는 탐색 파트에서 더 공부

## 용어 정리

- **Key & Value**
  - 트리에서 노드는 key와 value를 가짐
    - Key는 해당 노드를 다른 노드와 구분 짓게 하는 식별자 (identifier)를 의미
    - Value는 key에 대응되는 데이터 값을 의미
      - Value가 별도로 없다면 key만 사용
  - 트리에서 search를 할 때는 key를 기준으로 찾음

<p align="center">
<img src="/assets/img/blog/key_value.png">
</p>

## 이진 탐색 트리 정의

- **이진 탐색 트리 (Binary Search Tree, BST)**
  - 모든 노드는 유이한 key를 가짐 (중복 버전은 논외)
    - Key들 끼리는 비교가 가능하고 순서가 있음
  - 왼쪽 서브트리의 key들은 루트의 key보다 <span style="color:red">작음</span>
  - 오른쪽 서브트리의 key들은 루트의 key보다 <span style="color:blue">큼</span>
  - 왼쪽 및 오른쪽 서브트리는 재귀적으로 **이진 탐색 트리**여야 함

<p align="center">
<img src="/assets/img/blog/bst.png">
</p>

## 이진 탐색 트리의 ADT

- **데이터**
  - 이진 탐색 트리 (BST)의 정의를 만족하는 이진 트리

- **주요 연산**
  - search(key): key를 가지는 노드 (or value)를 찾아 반환
  - insert(key, value): 이진 탐색 트리의 특성을 유지하면서 주어진 key와 value를 가지는 노드를 삽입
    - 이미 트리에 해당 key를 가지는 노드가 있다면 주어진 value로 업데이트
  - remove(key): 이진 탐색 트리의 특성을 유지하면서 key를 가지는 노드를 트리에서 삭제

## Search in BST

- **Cases for search in BST**
  - Case 1) 탐색 키 (querying key)와 현재 노드의 key가 같은 경우
    - 원하는 값을 찾은 것으로 현재 노드 (or value)를 반환
  - Case 2) 탐색 키가 현재 노드의 key보다 작은 경우
    - 왼쪽 서브트리를 기준으로 다시 search 수행
  - Case 3) 탐색 키가 현재 노드의 key보다 큰 경우
    - 오른쪽 서브트리를 기준으로 다시 search 수행

<p align="center">
<img src="/assets/img/blog/search_bst.png">
</p>

## Pseudocode for Search (recursive)

~~~
def search(node, key): # key is asked by a user
  if node == NULL or key == node's key:
    return node
  else if key < node's key:
    return search(node->left, key)
  else: # key > node's key
    return search(node->right, key)
~~~

<p align="center">
<img src="/assets/img/blog/search_bst_pseudocode.png">
</p>

## Pseudocode for Search (iterative)

~~~
def search_iter(node, key): # key is asked by a user
  cur_node = node
  while cur_node != NULL:
    if key == cur_node's key:
      return cur_node
    else if key < cur_node's key:
      cur_node = cur_node->left
    else: # key > cur_node's key
      cur_node = cur_node->right
  return cur_node
~~~

<p align="center">
<img src="/assets/img/blog/search_bst_pseudocode_iter.png">
</p>

## Insert in BST

- **이진 탐색 트리에 원소를 삽입하기 위해서는 먼저 탐색을 수행**
  - 탐색에 실패한 위치가 바로 새로운 노드를 삽입하는 위치
  - 동일한 key를 가지는 경우 주어진 value로 update

<p align="center">
<img src="/assets/img/blog/insert_bst.png">
</p>

## Pseudocode for Insert (recursive)

~~~
def insert(node, key, value):
  if key == node's key:
    update the node's value by value & return
  else if key < node's key:
    if node->left == NULL:
      node->left <- Node(key, value, NULL, NULL)
    else:
      insert(node->left, key, value)
  else: # key > node's key
    if node->right == NULL:
      node->right <- Node(key, value, NULL, NULL)
    else:
      insert(node->right, key, value)
~~~

## Remove in BST

- **Cases for remove in BST**
  - 먼저 삭제하려는 노드를 search를 통해 찾음
  - Case 1) 삭제하려는 노드가 리프 노드인 경우
  - Case 2) 삭제하려는 노드가 왼쪽 또는 오른쪽 서브트리 중 하나만 자식으로 가지고 있는 경우
  - Case 3) 삭제하려는 노드가 두 개의 서브트리를 모두 가지고 있는 경우

<p align="center">
<img src="/assets/img/blog/remove_bst.png">
</p>

## Remove in BST - Case 1

- 삭제하려는 노드가 리프노드인 경우
  - Replace <span style="color:purple">node</span> in its <span style="color:orange">parent</span> with NULL
    - 부모노드에서 삭제할 노드로 가는 포인터에 대해 NULL 처리 후 해당 노드 해제
    - 만일, 삭제하려는 노드가 루트이고 리프인 경우 부모가 없기 때문에 삭제만 하면 됨

<p align="center">
<img src="/assets/img/blog/remove_bst_case1.png">
</p>

## Remove in BST - Case 2

- 삭제하려는 노드가 왼쪽 또는 오른쪽 서브트리 중 하나만 자식으로 가지고 있는 경우
  - Replace <span style="color:purple">node</span> in its <span style="color:orange">parent</span> with <span style="color:green">node->left</span> (or right)
    - 서브트리의 루트를 부모 노드에 붙여주고 해당 노드는 해제

<p align="center">
<img src="/assets/img/blog/remove_bst_case2.png">
</p>

    - 삭제하려는 노드가 전체 트리의 루트인 경우 서브트리의 루트를 전체 트리의 루트로 대체됨

<p align="center">
<img src="/assets/img/blog/remove_bst_case2_root.png">
</p>

## Remove in BST - Case 3

- **삭제하려는 노드가 두 개의 서브트리를 모두 가지고 있는 경우**
  - 삭제하려는 노드를 대체할 다른 노드를 찾아야함 - **후계자** (successor)
    - 후계자 기준: 삭제하려는 노드의 key가 가장 비슷하면 됨 (아래 둘 다 가능)
    - 후계자 1) 왼쪽 서브트리에서 제일 큰 key
    - <span style="color:blue">후계자 2) 오른쪽 서브트리에서 제일 작은 key (our choice)</span>

<p align="center">
<img src="/assets/img/blog/remove_bst_case3.png">
</p>

  - Replace <span style="color:purple">node</span> with <span style="color:skyblue">successor</span> & remove <span style="color:skyblue">successor</span>
    - 후계자 노드의 key & value를 삭제할 노드로 복사하고 후계자 노드를 삭제

<p align="center">
<img src="/assets/img/blog/remove_bst_case3_replace.png">
</p>

## Leftmost/Rightmost Node in BST

- **Q. 이진 탐색 트리에서 제일 작은 key 또는 제일 큰 key는 어떻게 찾을 수 있을까?**
  - 제일 작은 key를 가지는 노드: the leftmost node in the tree
    - 트리의 제일 왼쪽에 위치하며 왼쪽에는 더 이상 자식 노드가 없음
  - 제일 큰 key를 가지는 노드: the rightmost node in the tree
    - 트리의 제일 오른쪽에 위치하며 오른쪽에는 더 이상 자식 노드가 없음

<p align="center">
<img src="/assets/img/blog/leftmost_rightmost.png">
</p>

## Leftmost Node in BST

- **Claim. BST에서 leftmost node는 minimum key를 가짐**
  - Proof by contradiction
    - **가정**: Leftmost node가 minimum key를 가지지 않음
    - 그러면 트리의 leftmost를 제외한 어딘가에 minimum key를 가지는 node가 있음
    - 그렇게 되면 BST 정의에 어긋나게 되어 모순 (contradiction) 발생
      - Leftmost node의 key보다 minimum의 key가 작은데도 불구하고 leftmost node의 왼쪽이 아닌 다른 곳에 있기 때문에 BST의 구조가 깨짐
    - 따라서, 위 가정 "Leftmost node가 minimum key를 가지지 않는다"은 틀림
      &rarr; Leftmost node가 minimum key를 가짐

~~~
def leftmost(node):
  while node->left != NULL:
    node = node->left
  return node
~~~

## Pseudocode for Remove (recursive)

~~~
def remove(nodem parent, key):
  if node == NULL:
    return # since there is no node with key
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

## What You Need To Know

- **이진 탐색 트리의 정의**
  - 왼쪽 서브트리의 key들은 루트의 key보다 <span style="color:red">작음</span>
  - 오른쪽 서브트리의 key들은 루트의 key보다 <span style="color:blue">큼</span>
  - 왼쪽 및 오른쪽 서브트리는 재귀적으로 **이진 탐색 트리**여야 함

- **이진 탐색 트리의 주요 연산**
  - Search: 이진 탐색 트리의 정의 따라 분기를 타면서 탐색
  - Insert: search가 실패한 곳에 새로운 노드를 삽입
  - Remove: 먼저 search 후 BST의 구조가 유지될 수 있도록 삭제

<p align="center">
<img src="/assets/img/blog/bst_summary.png">
</p>