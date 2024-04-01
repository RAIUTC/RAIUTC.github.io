---
layout: post
title: Red-black Tree
description: |
  
categories: 자료구조
sitemap: false
hide_last_modified: true
---

# Red-black Tree

## Self-balancing BST - Red-black tree

### Binary Search Tree

- **<span style="color:blue">Binary tree satisfying BST properties</span>**
> BST 속성을 만족하는 이진 트리
  - Keys in the left sub-tree < the key of the root.
  > 왼쪽 서브 트리의 키는 루트의 키보다 작습니다.
  - Keys in the right sub-tree >. the key of the root.
  > 오른쪽 서브 트리의 키는 루트의 키보다 큽니다.
  - Both left & right sub trees are BST recursively.
  > 왼쪽과 오른쪽 서브 트리 모두 재귀적으로 BST 속성을 만족합니다.

<p align="center">
<img src="/assets/img/blog/bst_3.png">
</p>

### Limitation of BST

- **<span style="color:blue">BST shows $$ O(n) $$ time for worst case!</span>**
> BST는 최악의 경우에도 $$ O(n) $$ 시간을 소요됩니다!
  - Because the tree becomes **<span style="color:red">unbalanced</span>**, & its height is $$ O(n) $$.
  > 트리가 불균형 상태가 되어 높이가 $$ O(n) $$이 되기 때문입니다.
    - e.g., when sorted keys are inserted sequentially
    > 예: 순차적으로 정렬된 키가 삽입될 때
  - For the best & average cases, it's height is $$ O(log n) $$ because the tree becomes **<span style="color:blue">balanced</span>**.
  > 최선 및 평균 경우에는 트리가 균형상태가 되어 높이가 $$ O(log n) $$이 됩니다.
  - Thus, the operations of unbalanced BST are inefficient compared to those of balanced BST.
  > 따라서 불균형한 BST의 연산은 균형잡힌 BST의 연산에 비해 비효율적입니다.

- **<span style="color:red">How can we make the BST balanced even for a worst case?</span>**
> 최악의 경우에도 BST를 균형잡힌 상태로 만들 수 있는 방법은 무엇일까요?

### Self-Balancing BST

- **<span style="color:blue">Automatically preserve the balance of BST after insert & remove operations</span>**
> 삽입 및 삭제 연산 이후에도 BST의 균형을 자동으로 유지합니다
  - i.e., the tree's height is always $$ O(log n) $$ for a worsk case
  > 즉, 최악의 경우에도 트리의 높이가 항상 $$ O(log n) $$입니다.

- **<span style="color:blue">Representative self-balancing BST</span>**
> 대표적인 자기 균형 이진 탐색 트리
  - AVL tree
  - **<span style="color:red">Red-black tree</span>**
    - It supports faster inssertion and removal than AVL.
    > AVL보다 더 빠른 삽입 및 삭제를 지원합니다.
    - It is more memory-efficient than AVL.
    > AVL보다 메모리 사용 효율이 더 높습니다.
    - Used in std::map in C++'s STL.
    > C++의 STL에서 std::map에 사용됩니다.

### Red-Black Tree

- **<span style="color:blue">Definition</span>**
  - Each node is colored by either "**<span style="color:red">RED</span>**" or "**BLACK**".
  > 각 노드는 빨간색 또는 검은색으로 색칠됩니다.
    - Represented as one bit (e.g., 0 or 1).
    > 하나의 비트로 표시됩니다(예: 0 또는 1).
    - Used to ensure that the tree remains balanced during operations.
    > 연산 중에 트리가 균형을 유지하도록 보장하기 위해 사용됩니다.

- **<span style="color:blue">Red-black tree properties</span>**
> 레드 블랙 트리 속성
  - P1) the root node should be **BLACK**.
  > 루트 노드는 검은색이어햐 합니다.
  - P2) All leaf (NIL) nodes are considered as **BLACK**.
  > 모든 리프 노드는 검은색으로 간주됩니다.
  - P3) if a node is **<span style="color:red">RED</span>**, then both its children must be **BLACK**.
  > 만약 노드가 빨간색이면, 그 자식들은 모두 검은색이어야 합니다.
  - P4) Every path from a given node to any of its descendant NIL leaves goes through the same number of **BLACK** nodes.
  > 주어진 노드에서 해당하는 모든 자손 리프까지의 경로는 동일한 수의 검은색 노드를 통과합니다.

### Example of Red-Black Tree

<p align="center">
<img src="/assets/img/blog/red_black_tree_1.png">
</p>

### Red-Black Tree's Operations

- **<span style="color:blue">For search, red-black tree uses BST's search</span>**
> 탐색을 위해서는, 레드-블랙 트리는 이진 탐색 트리의 탐색을 사용합니다.
  - Because this operation does not modify the tree.
  > 이 연산은 트리를 수정하지 않기 때문입니다.

- **<span style="color:blue">For insert and remove operations,</span>**
> 삽입 및 삭제 연산에 대해,
  - RBT first performs the insert or remove operation of BST.
  > RBT는 먼저 BST의 삽입 또는 삭제 연산을 수행합니다.
    - As result, the modified tree's balance can be broken.
    > 결과적으로 수정된 트리의 균형이 깨질 수 있습니다.
  - Then, RBT **properly re-arranges the modified tree** so that it satisfies the red-black tree properties.
  > 그런 다음, RBT는 수정된 트리를 적절하게 재배치하여 RBT 속성을 만족하도록 합니다.
    - Using **<span style="color:blue">re-coloring</span>** and **<span style="color:red">rotations</span>**.
    > 재색칠과 회전을 사용합니다.
  - See Appendix for pseudocode of insert and remove.
  > 삽입 및 삭제의 의사코드는 부록을 참조하세요.

## Insert of RBT

### Insert of RBT

- **<span style="color:blue">Step 1)</span> insert a <span style="color:red">RED</span> node into the tree using BST's insert operation**
> 이진 탐색 트리의 삽입 연산을 사용하여 트리에 빨간색 노드를 삽입합니다.

- **<span style="color:blue">Step 2)</span> re-arrange the modified tree <span style="color:red">case-by-case</span>**
> 수정된 트리를 경우별로 재배치합니다.

- **<span style="color:blue">Note that</span>**
> 주의할 점
  - The new node will be located at the bottom of the tree after BST's insertion.
  > 새로운 노드는 BST의 삽입 후 트리의 맨 아래에 위치하게 됩니다.
  - Let's do case study around the inserted location.
  > 삽입된 위치를 중심으로 경우의 수를 고려해 보겠습니다.

<p align="center">
<img src="/assets/img/blog/red_black_tree_2.png">
</p>

- **<span style="color:blue">Case study</span>**
  - No violation below the inserted node $$ x $$.
  > 삽입된 노드 $$ x $$ 아래에 위반 사항이 없습니다.
    - Because this node is **<span style="color:red">RED</span>** and had two NIL (**BLACK**) nodes
    > 왜냐하면 이 노드는 빨간색이며 두 개의 NIL(검정색)노드를 가지고 있기 때문입니다.
  - &rarr; Need to check if there are violations above the node.
  > 노드 위에 위반 사항이 있는지 확인해야 합니다.
    - Let $$ p $$ denote the parent of the inserted node.
    > $$ p $$가 삽입된 노드의 부모라고 가정합니다.
  - **<span style="color:blue">Case 1)</span>** $$ p $$ was **BLACK** &rarr; No violation.
  > $$ p $$가 검정색인 경우 -> 위반 사항이 없습니다.
  - **<span style="color:blue">Case 2)</span>** $$ p $$ was **<span style="color:red">RED</span>** &rarr; P3 is violated! How to handle this?
  > $$ p $$가 빨간색인 경우 -> P3가 위반됩니다! 이를 어떻게 처리할까요?

  <p align="center">
  <img src="/assets/img/blog/red_black_tree_3.png">
  <img src="/assets/img/blog/red_black_tree_4.png">
  </p>

- **<span style="color:blue">Case 2) when $$ p $$ was </span><span style="color:red">RED</span> \[detailed\]**
> $$ p $$가 빨간색인 경우 \[자세히\]
  - Before the insertion, the parent of $$ p $$ was **BLACK**.
  > 삽입 전에 $$ p $$의 부모는 검정색이었습니다.
    - Let $$ g $$ denote the grandparent $$ x $$.
    > $$ g $$를 삽입된 노드 $$ x $$의 할아버지로 지정합니다.
  - If $$ p $$ had a child, the sibling of $$ x $$ was also **BLACK**.
  > 만약 $$ p $$가 자식이 있다면, $$ x $$의 형제는 또한 검정색입니다.
  - The sibling of $$ p $$ is either **<span style="color:red">RED</span>** or **BLACK**.
  > $$ p $$의 형제는 빨간색 또는 검정색입니다.
    - Let $$ u $$ denote the uncle of $$ x $$.
    > $$ u $$를 $$ x $$의 삼촌으로 지정합니다.

- **<span style="color:blue">Cases for re-arrangement</span>**
  - **<span style="color:blue">Case 2-1)</span>** $$ u $$ was **<span style="color:red">RED</span>**
  - **<span style="color:blue">Case 2-2)</span>** $$ u $$ was **BLACK**

<p align="center">
<img src="/assets/img/blog/red_black_tree_5.png">
</p>

EOP: end-of-procedure

- **<span style="color:blue">Case 2-1)</span> $$ u $$ was <span style="color:red">RED</span>**
> $$ u $$가 빨간색인 경우
  - 1) Re-color $$ p $$ and $$ u $$ in **BLACK**, and $$ g $$ in **<span style="color:red">RED.</span>**
  > $$ p $$와 $$ u $$를 검정색으로, $$ g $$를 빨간색으로 재색칠합니다.
    - If $$ g $$ is the root, then recolor $$ g $$ in **BLACK**; \[EOP\]
    > $$ g $$가 루트인 경우, $$ g $$를 검정색으로 재색칠합니다; \[EOP\]
  - 2) Recursively handle a potential violation on $$ g $$
  > 잠재적인 위반 사항을 재귀적으로 처리합니다.
    - i.e., when the parent of $$ g $$ was <span style="color:red">RED</span>
    > 즉, $$ g $$의 부모가 빨간색인 경우

<p align="center">
<img src="/assets/img/blog/red_black_tree_6.png">
</p>

- **<span style="color:blue">Case 2-2)</span> $$ u $$ was BLACK**
  - **LR)** $$ p $$ is the **L**eft of $$ g $$ & $$ x $$ is the **R**ight of $$ p $$
  - **LL)** $$ p $$ is the **L**eft of $$ g $$ & $$ x $$ is the **L**eft of $$ p $$
  - **RL)** $$ p $$ is the **R**ight of $$ g $$ & $$ x $$ is the **L**eft of $$ p $$ (mirror of LR)
  - **RR)** $$ p $$ is the **R**ight of $$ g $$ & $$ x $$ is the **R**ight of $$ p $$ (mirror of LL)

<p align="center">
<img src="/assets/img/blog/red_black_tree_7.png">
</p>

- **<span style="color:blue">Case LR)</span> $$ p $$ is the left of $$ g $$ & $$ x $$ is the right of $$ p $$**
  - 1) Rotate the tree of $$ p $$ left
    - Note that $$ x > p $$
      - $$ p $$ becomes the left child of $$ x $$
      - The left sub-tree of $$ x $$ becomes the right child of $$ p $$
  - 2) Go to Case LL on $$ p $$

<p align="center">
<img src="/assets/img/blog/red_black_tree_8.png">
</p>

- **<span style="color:blue">Case LL)</span> $$ p $$ is the left of $$ g $$ & $$ x $$ is the left of $$ p $$**
  - 1) Rotate the tree of $$ g $$ right
    - Note that $$ g > s $$
      - $$ s $$ becoms the left child of $$ g $$
  - 2) Swap the color of $$ p $$ and $$ g $$ \[EOP\]

<p align="center">
<img src="/assets/img/blog/red_black_tree_9.png">
</p>

## Remove of RBT

### Remove of RBT

- **<span style="color:blue">Remove operation</span>**
  - Step 1) remove a node using BST's remove operation
  - Step 2) re-arrange the tree <span style="color:red">case-by-case</span>

- **<span style="color:blue">Cases for remove in BST</span>**
  - <span style="color:blue">Case NC)</span> target node had **N**ot a **C**hild
  - <span style="color:blue">Case OC)</span> target node had **O**ne (left\|right) **C**hild (sub-tree)
  - <span style="color:blue">Case TC)</span> target node had **T**wo **C**hildren (sub-trees)

<p align="center">
<img src="/assets/img/blog/red_black_tree_10.png">
</p>

- **<span style="color:blue">Case TC can be converted to Case NC or OC.</span>**
> Case TC는 Case NC 또는 OC로 변환될 수 있습니다.
  - Target node $$ d $$'s key is replaced with successor's key
  > 대상 노드 $$ d $$의 키는 후계자의 키로 대체됩니다.
    - The successor $$ m $$ is the minimum node of the right sub-tree of $$ d $$.
    > 후계자 $$ m $$은 $$ d $$의 오른쪽 서브 트리의 최소 노드입니다.
    - Only keys are swapped; thus, there is no violation in this step.
    > 키만 교환되므로 이 단계에서 위반 사항은 없습니다.
  - Next, the successor is removed.
  > 다음으로 후계자가 제거됩니다.
    - Note that the successor has at most one child &rarr; Case NC or OC.
    > 후계자는 최대 하나의 자식을 가지고 있음을 유의하십시오 &rarr; Case NC 또는 OC.

<p align="center">
<img src="/assets/img/blog/red_black_tree_11.png">
</p>

$$ d $$: the node to be deleted

$$ c $$: the child of $$ d $$

- **<span style="color:blue">Study for case NC or OC</span>**
  - **Case R)** $$ d $$ was **<span style="color:red">RED</span>** &rarr; No violation
  - **Case BR)** $$ d $$ was **BLACK** & $$ c $$ was **<span style="color:red">RED</span>** &rarr; No violation
    - By re-coloring $$ c $$ in **BLACK** after removing $$ d $$
  - **Case BB)** $$ d $$ was **BLACK** & $$ c $$ was **BLACK** &rarr; P4 is violated

<p align="center">
<img src="/assets/img/blog/red_black_tree_12.png">
</p>

- **<span style="color:blue">Need to handle Case BB after deleting $$ d $$</span>**
  - **<span style="color:blue">Case 1)</span>** $$ p $$ was **<span style="color:red">RED</span>** &rarr; $$ s $$ was **BLACK**
    - <span style="color:red">Case 1-1)</span> \[l,r\] = \[**B**,**B**\]
    - <span style="color:red">Case 1-2)</span> \[l,r\] = \[**<span style="color:red">R,R</span>**\] or \[**B**,**<span style="color:red">R</span>**\] &rarr; \[*,**<span style="color:red">R</span>**\]
    - Case 1-3) \[l,r\] = \[**<span style="color:red">R</span>**,**B**\]
  - **<span style="color:blue">Case 2)</span>** $$ p $$ was **BLACK**
    - Case 2-1) \[s,l,r\] = \[**B,B,B**\]
    - <span style="color:red">Case 2-2)</span> \[s,l,r\] = \[**B,<span style="color:red">R,R</span>**\] or \[**B,B,<span style="color:red">R</span>**\] &rarr; \[**B**,*,**<span style="color:red">R</span>**\]
    - Case 2-3) \[s,l,r\] = \[**B,<span style="color:red">R</span>,B**\]
    - Case 2-4) \[s,l,r\] = \[**<span style="color:red">R</span>,B,B**\]
  - **<span style="color:red">Only Case 1-1 and Case *-2 are discussed in this lecture</span>**
    - See Appendix for other cases!

- **<span style="color:blue">Case 1-1</span>**
  - Swap the color of $$ p $$ and $$ s $$.

<p align="center">
<img src="/assets/img/blog/red_black_tree_13.png">
</p>

Case 1-2) \[l,r\] = \[*, <span style="color:red">R</span>\]

Case 2-2) \[s,l,r\] = \[B,*, <span style="color:red">R</span>\]

- **<span style="color:blue">Case *-2 (Cases 1-2 and 2-2)</span>**
  - Rotate the tree of $$ p $$ left
  - Swap the color of $$ p $$ and $$ s $$ & color $$ r $$ in **BLACK**

<p align="center">
<img src="/assets/img/blog/red_black_tree_14.png">
</p>

## Analysis of RBT

### Analysis of RBT

- **<span style="color:blue">RBT with $$ n $$ internal nodes has $$ O(log n) $$ height at most</span>**
> $$ n $$개의 내부 노드를 가진 RBT는 최대 $$ O(log n) $$ 높이를 가집니다.
  - \[Fact\] <span style="color:red">Sub-tree of $$ bh(v) $$ has at least $$ 2^{bh(v)} - 1 $$ internal nodes</span>
  > $$ bh(v) $$의 서브트리는 적어도 $$ 2^{bh(v)} - 1 $$개의 내부 노드를 가집니다.
    - $$ bh(v) $$: # of black nodes on a path from $$ v $$ to a leaf node (not including $$ v $$)
    > $$ bh(v) $$: $$ v $$에서 리프 노드까지의 경로에 있는 검은색 노드의 수( $$ v $$는 포함하지 않음)
    - See Appendix for proof.

- **<span style="color:blue">Let's get the upper bound of the height $$ h $$ of the RBT.</span>**
> RBT의 높이 $$ h $$의 상한을 구해봅시다.
  - Let $$ P $$ denote a path from the root to the furthest leaf.
  > $$ P $$를 루트에서 가장 먼 리프까지의 경로라고 가정합니다.
  - At least, half of nodes on $$ P $$ must be **BLACK** (no two RED nodes in turn)
  > $$ P $$의 노드 중 적어도 절반은 검은색이어야 합니다(두 개의 빨간색 노드가 연속되지 않음)
  - Hence, $$ bh(root) $$ is at least $$ h/2 $$.
  > 따라서 $$ bh(root) $$는 적어도 $$ h/2 $$입니다.
  - RBT has $$ 2^{h/2} - 1 $$ internal nodes at least if $$ bh(root) = h/2 $$ by the fact.
  > 사실에 따라 $$ bh(root) = h/2 $$인 경우 RBT에는 적어도 $$ 2^{h/2} - 1 $$개의 내부 노드가 있습니다.

$$ 2^{h/2} - 1 <= n $$ &larr;&rarr; $$ h <= 2log_2(n+1) \in O(log n) $$

- **<span style="color:blue">Time complexity of RBT's operations</span>**
  - Search: $$ O(log n) $$ since RBT has $$ O(log n) $$ height at most
  > RBT의 탐색은 최대 $$ O(log n) $$ 높이를 가지므로 $$ O(log n) $$입니다.
    - RBT's search is equal to BST's search
    > RBT의 탐색은 BST의 탐색과 동일합니다.
  - Insert and remove: $$ O(log n) $$
  > 삽입 및 삭제: $$ O(log n) $$
    - Go down to the target node from root &rarr; $$ O(log n) $$.
    > 루트에서 대상 노드로 이동 &rarr; $$ O(log n) $$.
    - Re-coloring and rotating operations take constant time.
    > 재색칠 및 회전 연산은 상수 시간이 소요됩니다.
    - For some cases, neet to do these recursively toward root &rarr; $$ O(log n) $$.
    > 일부 경우에는 이러한 작업을 루트 방향으로 재귀적으로 수행해야 합니다 &rarr; $$ O(log n) $$.

- **<span style="color:blue">Space complexity of RBT</span>**
  - $$ O(n) $$ space
    - To store $$ n $$ nodes (key, value, pointers) + 1 bit for each node
    > $$ n $$개의 노드(키, 값, 포인터) + 각 노드에 1비트를 저장하기 위해

## Associative containers in STL

### Associative containers in STL
> STL의 연관 컨테이너

- **Data structures managing key-value data**
> 키-값 데이터를 관리하는 자료구조
  - <span style="color:blue">map</span> contains key-value pairs with unique keys
  > <span style="color:blue">map</span>은 고유한 키를 가진 키-값 쌍을 포함합니다.
  - <span style="color:blue">set</span> contains a set of unique keys
  > <span style="blue">set</span>은 고유한 키 집합을 포함합니다.
    - In multimap/multiset, multiple keys with equivalent values are allowed
    > multimap/multiset에서는 동등한 값의 여러 키가 허용됩니다.
  - They are implemented ar red-black trees
  > 이들은 레드-블랙 트리로 구현됩니다.

<p align="center">
<img src="/assets/img/blog/red_black_tree_15.png">
</p>

### Example Code of map

~~~cpp
#include <iostream>
#include <map>
#include <string>
#include <string_view>

void print_map(std::string_view comment, const std::map<std::string, int>& m)
{
  std::cout << comment;
  // iterate using C++17 facilities
  for (const auto& [key, value] : m)
    std::cout << '[' << key << "] = " << value << ";";

  std::cout << '\n';
}
int main()
{
  // Create a map of three (string, int) pairs
  std::map<std::string, int> m{\{"CPU", 10\}, \{"GPU", 15\}, \{"RAM", 20\}};

  print_map("1) Initial map: ", m);

  m["CPU"] = 25; // update an existing value
  m["SSD"] = 30; // insert a new value
  print_map("2) Updated map: ", m);

  // using operator[] with non-existent key always performs an insert
  std::cout << "3) m[UPS] = " << m["UPS"] << '\n';
  print_map("4) Updated map: ", m);

  m.erase("GPU"); 
  print_map("5) After erase: ", m);

  std::erase_if(m, [](const auto& pair){ return pair.second > 25; });
  print_map("6) After erase: ", m);
  std::cout << "7) m.size() = " << m.size() << '\n';

  m.clear();
  std::cout << std::boolalpha << "8) Map is empty: " << m.empty() << '\n';
}
~~~

### What You Need To Know

- **<span style="color:blue">Red-black tree (used in std::map)</span>**
> <span style="color:blue">레드-블랙 트리 (std::map에서 사용됨)</span>
  - **Why do we need red-black tree?**
  > 왜 레드-블랙 트리가 필요한가?
    - BST has $$ O(n) $$ height while RBT gurantees $$ O(log n) $$ height for a worst case
    > BST는 최악의 경우 $$ O(n) $$ 높이를 가지지만, RBT는 최악의 경우 $$ O(log n) $$ 높이를 보장합니다.
  - **Definition and properties of RBT**
  > RBT의 정의 및 속성
    - BST where eace node is colored by either **<span style="color:red">RED</span>** or **BLACK**
    > 각 노드가 빨간색 또는 검은색으로 색칠된 BST
      - P1) **BLACK** root node & P2) All **BLACK** leaf (or NIL) nodes
      > P1) 검은색 루트 노드 & P2) 모든 검은색 리프(또는 NIL) 노드
      - P3) No two consecutive **<span style="color:red">RED</span>** nodes & P4) Consistent black height
      > P3) 연속된 두 빨간색 노드가 없음 & P4) 일관된 검은색 높이
  - **Insert and remove operations of RBT**
  > RBT의 삽입 및 삭제 연산
    - Do BST's corresponding operation and re-arrange violated area using re-coloring and rotating case by case
    > BST의 해당 연산을 수행하고, 위반된 영역을 재색칠 및 회전하여 경우별로 재배치합니다.

### Appendix: Insert of RBT

- **<span style="color:blue">Case RL)</span> $$ p $$ is the right of $$ g $$ & $$ x $$ is the left of $$ p $$**
  - 1) Rotate the tree of $$ p $$ right
    - Note that $$ x < p $$
      - $$ p $$ becomes the right child of $$ x $$
      - The right sub-tree of $$ x $$ becomes the left child of $$ p $$
  - 2) Go to Case RR on $$ p $$

<p align="center">
<img src="/assets/img/blog/red_black_tree_16.png">
</p>

- **<span style="color:blue">Case RR)</span> $$ p $$ is the right of $$ g $$ & $$ x $$ is the right of $$ p $$**
  - 1) Rotate the tree of $$ g $$ left
    - Note that $$ g < s $$
      - s becomes the right child of $$ g $$
  - 2) Swap the color of $$ p $$ and $$ g $$ \[EOP\]

<p align="center">
<img src="/assets/img/blog/red_black_tree_17.png">
</p>

- **<span style="color:blue">Pseudocode of insert</span> ($$ x $$ is the newly inserted node)**
> 삽입의 의사코드 ($$ x $$는 새로 삽입된 노드입니다)
  - **Step 1)** Do BST's insert on $$ x $$ and make the color of $$ x $$ **<span style="color:red">RED</span>**
  > $$ x $$에 대해 BST의 삽입을 수행하고, $$ x $$의 색을 빨간색으로 만듭니다.
  - **Step 2)** If $$ x $$ is root, change the color of $$ x $$ to **BLACK** \[EOP\]
  > $$ x $$가 루트인 경우, $$ x $$의 색을 검정색으로 변경합니다 \[EOP\]
  - **Step 3)** Else if $$ x $$ isn't root & $$ x $$'s parent $$ p $$ is **<span style="color:red">RED</span>**
  > 그렇지 않고 $$ x $$가 루트가 아니며, $$ x $$의 부모 $$ p $$가 빨간색인 경우
    - <span style="color:blue">If Case 2-1:</span> # $$ x $$'s uncle $$ u $$ is <span style="color:red">RED</span>
    > $$ x $$의 삼촌 $$ u $$가 빨간색인 경우
      - Re-color $$ p $$ and $$ u $$ in black, and $$ g $$ in <span style="color:red">RED</span>
      > $$ p $$와 $$ u $$를 검정색으로, $$ g $$를 빨간색으로 재색칠합니다.
      - Recursively handle a potential violation on $$ g $$ ($$ x $$ &larr; $$ g $$ & repeat steps 2 & 3)
      > 잠재적인 위반 사항을 $$ g $$에서 재귀적으로 처리합니다 ($$ x $$ &larr; $$ g $$ & 단계 2 및 3을 반복합니다)
    - <span style="color:blue">Else if Case LR:</span> Do LR rotation on $$ p $$ & go to Case LL on $$ p $$
    > <span style="color:blue">Case LR:</span> $$ p $$에서 LR 회전을 수행하고, $$ p $$에서 Case LL로 이동합니다
    - <span style="color:blue">Else if Case LL:</span> Do LL rotation on $$ g $$ & swap the color of $$ p $$ and $$ g $$ \[EOP\]
    > <span style="color:blue">Case LL:</span> $$ g $$에서 LL 회전을 수행하고, $$ p $$와 $$ g $$의 색을 교환합니다 \[EOP\]
    - <span style="color:blue">Else if Case RL:</span> Do RL rotation on $$ p $$ & go to Case RR on $$ p $$
    > <span style="color:blue">Case RL:</span> $$ p $$에서 RL 회전을 수행하고, $$ p $$에서 Case RR로 이동합니다
    - <span style="color:blue">Else if Case RR:</span> Do RR rotation on $$ g $$ & swap the color of $$ p $$ and $$ g $$ \[EOP\]
    > <span style="color:blue">Case RR:</span> $$ g $$에서 RR 회전을 수행하고, $$ p $$와 $$ g $$의 색을 교환합니다 \[EOP\]

### Appendix: remove of RBT

- **<span style="color:blue">Case *-3 (Cases 1-3 and 2-3)</span>**
    - Case 1-3: \[l,r\] = \[**<span style="color:red">R</span>,B**\]
    - Case 2-3: \[s,l,r\] = \[**B,<span style="color:red">R</span>,B**\]
  - Rotate the tree of $$ s $$ right
  - Swap the color of $$ l $$ and $$ s $$ & go to Case *-2

<p align="center">
<img src="/assets/img/blog/red_black_tree_18.png">
</p>

- **<span style="color:blue">Case 2-1</span> (\[s,l,r\]=\[B,B,B\])**
  - Re-color $$ s $$ in **<span style="color:red">RED.</span>**
    - The paths via node $$ p $$ lack one black node now
    > 이제 노드 $$ p $$를 통한 경로에 하나의 검은색 노드가 부족합니다.
  - Recursively handle the problem on $$ p $$.
  > $$ p $$에서 문제를 재귀적으로 처리합니다.

<p align="center">
<img src="/assets/img/blog/red_black_tree_19.png">
</p>

- **<span style="color:blue">Case 2-4</span> (\[s,l,r\]=\[<span style="color:red">R</span>,B,B\])**
  - Rotating the tree of $$ p $$ left
  - Swap the color of $$ p $$ and $$ s $$ & go to Case 1

<p align="center">
<img src="/assets/img/blog/red_black_tree_20.png">
</p>

- **<span style="color:blue">Pseudocode of remove</span> ($$ d $$ is the node to be delete)**
  - **Step 1)** Do BST's remove on $$ d $$
  > $$ d $$에 대해 BST의 삭제를 수행합니다.
  - **Step 2)** If $$ d $$ is root, mark root NIL \[EOP\]
  > $$ d $$가 루트인 경우, 루트 NIL을 표시합니다 \[EOP\]
  - **Step 3)** Else if $$ d $$ isn't root & d is **BLACK** & $$ c $$ is **BLACK**
  > 그렇지 않고 $$ d $$가 루트가 아니며, $$ d $$가 **검정색**이고 $$ c $$가 **검정색**인 경우
    - <span style="color:blue">If Case 1-1</span>, then change the color of $$ p $$ and $$ s $$ \[EOP\]
    > <span style="color:blue">Case 1-1</span>이면, $$ p $$와 $$ s $$의 색을 변경합니다 \[EOP\]
    - <span style="color:blue">Else if Case *-2</span>
      - Rotate the tree of $$ p $$ left & swap the color of $$ p $$ and $$ s $$ & change $$ r $$ to **BLACK** \[EOP\]
      > $$ p $$의 트리를 왼쪽으로 회전하고, $$ p $$와 $$ s $$의 색을 교환하고, $$ r $$을 **검정색**으로 변경합니다 \[EOP\]
    - <span style="color:blue">Else if Case *-3</span>
      - Rotate the tree of $$ s $$ right & swap the color of $$ l $$ and $$ s $$ & go to Case *-2
      > $$ s $$의 트리를 오른쪽으로 회전하고, $$ l $$과 $$ s $$의 색을 교환하고, Case *-2로 이동합니다
    - <span style="color:blue">Else if Case 2-1</span>
      - Change $$ s $$ to **<span style="color:red">RED</span>** & recursively handle the problem on $$ p $$ (c &larr; p and go to Step 3) 
      > $$ s $$를 **빨간색**으로 변경하고, $$ p $$에서 문제를 재귀적으로 처리합니다 (c &larr; p 및 단계 3로 이동)
    - <span style="color:blue">Else if Case 2-4</span>
      - Rotating the tree of $$ p $$ left & swap the color of $$ p $$ and $$ s $$ & go to Case 1-*
      > $$ p $$의 트리를 왼쪽으로 회전하고, $$ p $$와 $$ s $$의 색을 교환하고, Case 1-*로 이동합니다

### Appendix: Proof

- **<span style="color:blue">Claim: a sub-tree of black height $$ bh(v) $$ in an RBT contains at least $$ 2^{bh(v)} - 1 $$ internal nodes.</span>**
> <span style="color:blue">주장: RBT의 검은색 높이 $$ bh(v) $$의 서브트리에는 적어도 $$ 2^{bh(v)} - 1 $$개의 내부 노드가 포함됩니다.</span>
  - **<span style="color:red">Base cases</span>** (height($$ v $$) = 0)
    - If height($$ v $$) is 0, then $$ v $$ is a leaf.
    > height($$ v $$)가 0이면, $$ v $$는 리프입니다.
    - The black height of $$ v $$ is 0.
    > $$ v $$의 검은색 높이는 0입니다.
    - The sub-tree $$ T_v $$ rooted at $$ v $$ contains 0 = $$ 2^{bh(v)} - 1 $$ internal nodes.
    > $$ v $$를 루트로 하는 서브트리 $$ T_v $$에는 0 = $$ 2^{bh(v)} - 1 $$개의 내부 노드가 포함됩니다.
  - **<span style="color:red">Inductive step</span>**
  > <span style="color:red">귀납 단계</span>
    - Suppose $$ v $$ is a node with height($$ v $$) > 0.
    > height($$ v $$) > 0인 노드 $$ v $$가 있다고 가정합니다.
    - $$ v $$ has two children with strictly smaller height.
    > $$ v $$는 더 작은 높이를 가진 두 개의 자식을 가지고 있습니다.
    - These children ($$ c1, c2 $$) either have $$ bh(c_i) = bh(v) $$ or $$ bh(c_i) = bh(v) - 1 $$.
    > 이러한 자식($$ c1, c2 $$)은 $$ bh(c_i) = bh(v) $$ 또는 $$ bh(c_i) = bh(v) - 1 $$입니다.
    - By hypothesis, both sub-trees contains at least $$ 2^{bh(v)-1} - 1 $$.
    > 가설에 따라 두 서브트리는 적어도 $$ 2^{bh(v)-1} - 1 $$개를 포함합니다.
    - Then, $$ T_v $$ contains at least $$ 2(2^{bh(v)-1}-1)+1 >= 2^{bh(v)} - 1 $$ \[Q.E.D\]
    > 그런 다음, $$ T_v $$에는 적어도 $$ 2(2^{bh(v)-1}-1)+1 >= 2^{bh(v)} - 1 $$개가 포함됩니다 \[Q.E.D\]