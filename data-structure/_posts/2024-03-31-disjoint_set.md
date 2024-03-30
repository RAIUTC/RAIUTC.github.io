---
layout: post
title: Disjoint Set
description: |
  서로소 집합(union-find)에 대한 개념과 연산, 그리고 두 가지 효율적인 기법인 랭크에 의한 합병과 경로 압축에 대해 다룹니다. 이를 통해 서로소 집합이 빠른 연산을 지원하는 방법을 소개합니다.
categories: 자료구조
sitemap: false
hide_last_modified: true
---

# Disjoint Set

## Definition of disjoint set

### Disjoint Set
> 서로소 집합

- **<span style="color:blue">What is disjoint set?</span>**
  - **Disjoint set** is a data structure managing **<span style="color:red">non-overlapping</span>** sets
  > 서로소 집합은 겹치지 않는 집합들을 관리하는 데이터 구조입니다.
    - A **set** is used to contain unique objects.
    > 각각의 집합은 고유한 객체를 포함합니다.
    - Each intersection of two sets are empty.
    > 두 집합의 교집합은 비어 있습니다.

<p align="center">
<img src="/assets/img/blog/disjoint_set.png">
</p>

- **<span style="color:blue">Applications</span>**
  - Used when we need to manage multiple partitions or groups in a problem
  > 문제에서 여러 파티션이나 그룹을 관리해야 할 때 사용됩니다.
    - Connected components in a graph
    > 그래프에서 연결된 구성요소
    - Minimum spanning tree in a graph (Kruskal's algorithm)
    > 그래프에서의 최소 비용 신장 트리 (크루스칼 알고리즘)

### Main Operations

- **<span style="color:blue">make-set(u)</span>**
  - Create a new set containing only given element u
  > 주어진 요소 u만 포함하는 새로운 집합을 생성합니다.

- **<span style="color:blue">find-set(u)</span>**
  - Return the set containing given element u
  > 주어진 요소 u를 포함하는 집합을 반환합니다.

- **<span style="color:blue">union(u, v)</span>**
  - Merge (or union) the set having u and the set having v
  > 요소 u를 포함하는 집합과 요소 v를 포함하는 집합을 병합(또는 합칩니다).

- **<span style="color:blue">Notes</span>**
  - No need to consider intersect operation in disjoint set
  > 서로소 집합에서 교집합 연산을 고려할 필요가 없습니다.
  - Due to the operations, it's also known as <span style="color:blue">union-find.</span>
  > 이러한 연산들 때문에 이것은 union-find로도 알려져 있습니다.

## Disjoint set using non-binary tree

### How To Represent Disjoint Set

- **<span style="color:blue">A disjoint set is represented by a non-binary tree.</span>**
> 서로소 집합은 비이진 트리로 표현됩니다.
  - Unlike normal trees, we use **<span style="color:red">parent pointer tree.</span>**
  > 일반적인 트리와 달리 부모 포인터 트리를 사용합니다.
    - A child points to its parent, and the root points to itself (self-looped).
    > 자식은 부모를 가리키고, 루트는 자신을 가리킵니다. (self-looped)
  - Each tree represents a set(i.e., forest = multiple sets)
  > 각 트리는 하나의 집합을 나타냅니다(즉, forest = 여러 집합).
  - This tree is implemented by an 1D array called p.
  > 이 트리는 p라는 1차원 배열에 의해 구현됩니다.
    - Assume an element in the set is a positive integer.
    > 집합 내의 요소는 양의 정수라고 가정합니다.

<p align="center">
<img src="/assets/img/blog/disjoint_set_tree.png">
</p>

### Main Operations of Basic Version

- **<span style="color:blue">make-set(u)</span>**
  - It's implemented as u's parent points to u
  > u가 부모의 u를 가리키도록 구현됩니다.

- **<span style="color:blue">find-set(u)</span>**
  - Return the root of the set containing given u
  > 주어진 u를 포함하는 집합의 루트를 반환합니다.
  - Recursively walk up from u to the root
  > u부터 루트까지 재귀적으로 올라갑니다.

- **<span style="color:blue">union(u, v)</span>**
  - Merge the set having u and the set having v
  > 요소 u를 포함하는 집합과 요소 v를 포함하는 집합을 병합합니다.
    - Let the root of one set point to the root of other set
    > 한 집합의 루트를 다른 집합의 루트로 지정합니다.

<p align="center">
<img src="/assets/img/blog/disjoint_set_tree_operations.png">
<img src="/assets/img/blog/disjoint_set_tree_operations2.png">
</p>

### Analysis of Basic Version

- **<span style="color:blue">Space complexity</span>**
  - It takes $$ \theta(n) $$ space because of the array p.

- **<span style="color:blue">Time complexity</span>**
  - make-set(u) takes $$ \theta(1) $$ time.
  - find-set(u) takes $$ \theta(h_u) $$ time.
    - $$ h_u $$ is the height of the tree having u
  - union(u, v) takes $$ h_v + h_u + c $$ time.

- **<span style="color:blue">For a worst case, find-set(u) takes $$ \theta(n) $$ time.</span>**
  - When the tree of n nodes becomes degenerate
  > 트리가 n개의 노드를 가진 트리가 한 줄로 진행될 때
  - **<span style="color:red">Can we improve this even for such a worst case?</span>**
  > 이러한 최악의 경우에도 성능을 개선할 수 있을까?

## How to improve efficiency?

### How To Improve Efficiency?

- **<span style="color:blue">The efficiency of disjoint set can be improved</span>**
  - <span style="color:red">By reducing the height of each tree</span>
  - Because main operations totally depends on the tree height

- **<span style="color:blue">Two techniques can be used for the purpose</span>**
  - &rarr; <span style="color:red">Union by rank</span>
    - Idea: smaller tree is merged into taller tree in union

  - <span style="color:red">Path compression</span>
  > 경로 압축
    - Idea: flatten the tree while walking up to the root in find-set
    > 아이디어: find-set중에 루트로 올라가는 동안 트리를 펼침

### Union by Rank

- **<span style="color:blue">When does the tree's height increase?</span>**
  - It increases while we merge two disjoint sets - union(u, v)
  > 두 개의 서로소 집합을 병합하는 동안 트리의 높이가 증가합니다. - union(u, v)수행 시
  - Suppose the right tree is merged into the left one.
  > 오른쪽 트리가 왼쪽 트리로 합쳐진다고 가정해봅시다.

<p align="center">
<img src="/assets/img/blog/disjoint_set_union_by_rank.png">
</p>

- What if the left tree is merged into the right one?
> 만약 왼쪽 트리가 오른쪽 트리로 합쳐진다면 어떻게 될까요?
  - Then, the height dosen't change.
  > 그런 경우에는 높이가 변하지 않습니다.

- **<span style="color:blue">Smaller into taller strategy</span>**
> 작은 트리를 큰 트리로 흡수하는 전략
  - Let's merge the shorter tree into the taller tree
  > 더 짧은 트리를 더 긴 트리에 흡수시킵니다.

<p align="center">
<img src="/assets/img/blog/disjoint_set_union_by_rank2.png">
</p>

  - To check the tree's height quickly, let's store a variable for each node, called <span style="color:blue">rank.</span>
  > 트리의 높이를 빠르게 확인하기 위해 각 노드에 대해 변수를 저장합시다. 이를 랭크라고 부릅니다.

- **<span style="color:blue">make-set(u)</span>**
  - Make one disjoint set of u
  > 요소 u의 하나의 서로소 집합을 만듭니다.

<p align="center">
<img src="/assets/img/blog/disjoint_set_union_by_rank_operations.png">
</p>

- **<span style="color:blue">union(u, v)</span>**
  - Merge the set having u and the set having v by smaller into larger strategy
  > u와 v를 포함하는 집합을 작은 트리를 큰 트리로 흡수시키는 전략으로 병합합니다.

<p align="center">
<img src="/assets/img/blog/disjoint_set_union_by_rank_operations2.png">
</p>

### Examples

- **<span style="color:blue">When the height does not change after merge</span>**
> 병합 후에 높이가 변하지 않는 경우
  - If their heights are different, the height of the merged tree don't change.
  > 두 트리의 높이가 다르면, 병합된 트리의 높이는 변하지 않습니다.

<p align="center">
<img src="/assets/img/blog/disjoint_set_union_by_rank_example.png">
</p>

- **<span style="color:blue">When the height changes</span>**
> 높이가 변하는 경우
  - If their heights are the same, the height of the merged tree increases by 1.
  > 두 트리의 높이가 같으면, 병합된 트리의 높이가 1증가합니다.

<p align="center">
<img src="/assets/img/blog/disjoint_set_union_by_rank_example2.png">
</p>

### How To Improve Efficiency?

- **<span style="color:blue">The efficiency of disjoint set can be improved</span>**
> 서로소 집합의 효율성을 향상시킬 수 있습니다.
  - <span style="color:red">By reducing the height of each tree</span>
  > 각 트리의 높이를 줄이는 것
  - Because main operations totally depends on the tree height
  > 왜냐하면 주요 연산이 전적으로 트리의 높이에 의존하기 때문입니다.

- **<span style="color:blue">Two techniques can be used for the purpose</span>**
> 이를 위해 두 가지 기술을 사용할 수 있습니다.
  - <span style="color:red">Union by rank</span>
    - Idea: smaller tree is merged into taller tree in union
    > 아이디어: 더 작은 트리를 합병할 때 더 큰 트리에 흡수시킵니다.

  - &rarr; <span style="color:red">Path compression</span>
  > 경로 압축
    - Idea: flatten the tree while walking up to the root in find-set
    > 아이디어: find-set 중에 루트로 올라가는 동안 트리를 펼칩니다.

### Path Compression
> 경로 압축

- **<span style="color:blue">Even though we use union-by-rank, the tree's height can increase</span> during the union operation**
> 랭크에 의합 합병을 사용하더라도, 병합 작업 중에 트리의 높이가 증가할 수 있습니다.
  - When the height of the sets to be merged is the same
  > 병합할 집합의 높이가 동일한 경우
  - Where else can we reduce the tree's height?
  > 트리의 높이를 어떻게 더 줄일 수 있을까요?

- **Path compression's idea: <span style="color:blue">Let's flatten the tree</span>**
> 경로 압축의 아이디어: 트리를 펼쳐봅시다.
  - Every time we walk up the tree during find-set, let's re-assign parent pointers to make each node we pass a direct child of the root
  > find-set을 수행하는 동안 트리를 올라갈 때마다, 지나가는 각 노드를 루트의 직접적인 자식으로 만들기 위해 부모 포인터를 재지정합니다.

### Ecamples

- **<span style="color:blue">Flatten the tree during the find-set operation!</span>**

<p align="center">
<img src="/assets/img/blog/disjoint_set_path_compression.png">
<img src="/assets/img/blog/disjoint_set_path_compression2.png">
<img src="/assets/img/blog/disjoint_set_path_compression3.png">
<img src="/assets/img/blog/disjoint_set_path_compression4.png">
</p>

## Analysis of disjoint set

### Analysis of Union By Rank
> 랭크에 의한 합병 분석

- **Claim: using by rank, # of elements in a set represented by a root having rank $$ k $$ is at least $$ 2^k $$.**
> 주장: 랭크를 사용하면, 랭크가 k인 루트에 의해 표현된 집합의 원소 수는 최소 $$ 2^k $$입니다.
  - <span style="color:red">Base case</span>: If rank = 0, $$ 2^0 = 1 $$ element in the set.
  > 초기 조건: 랭크가 0인 경우, 집합에는 $$ 2^0 = 1 $$개의 원소가 있습니다.
  - <span style="color:blue">Inductive step</span>
  > 귀납적 단계
    - Assume the claim holds for rank $$ r $$; then, is it true for rank $$ r + 1 $$.
    > 랭크 r에 대해 주장이 참이라고 가정하고, 랭크 $$ r + 1 $$에 대해서도 참인지 확인합니다.
    - The rank becomes $$ r + 1 $$ when both ranks of two sets are $$ r $$.
    > 두 집합의 랭크가 모두 r일 때 랭크가 $$ r + 1 $$이 됩니다.
    - By the assumption, each set has at least $$ 2^r $$ elements.
    > 가정에 따라 각 집합에는 최소 $$ 2^r $$개의 원소가 있습니다.
    - Thus, the merged set of rank $$ r + 1 $$ has at least $$ 2^r + 2^r = 2^{r+1} $$ elements.
    > 따라서 랭크 r + 1의 병합된 집합은 최소 $$ 2^r + 2^r = 2^{r+1} $$개의 원소를 가집니다.

- Claim: using union by rank, if the set has $$ n $$ nodes, then the root of the set for has $$ O(log n) $$ rank.
> 주장: 랭크에 의한 합병을 사용하면, 집합이 n개의 노드를 가진 경우 집합의 루트는 $$ O(log n) $$ 랭크를 가집니다.
  - Let $$ k $$ be the root's rank; $$ n >= 2^k $$ &larr;&rarr; $$ k <= log_2 n = O(log n) $$
  > 루트의 랭크를 k라고 가정하면, $$ n >= 2^k $$ &larr;&rarr; $$ k <= log_2 n = O(log n) $$
    - The height of the tree <= rank $$ k $$ <= $$ log_2 n $$
    > 트리의 높이 <= 랭크 $$ k $$ <= $$ log_2 n $$입니다.

- **<span style="color:blue">Time complexity of basic version + union-by-rank</span>**
  - make-set(u) takes $$ \theta(1) $$ time.
  - find-set(u) takes $$ O(log n) $$ time.
  - union(u, v) takes $$ O(log n) $$ time.

- **<span style="color:blue">(Amortized) Analysis in a sequence of operations</span>**
> (상환적)연산 순서에서의 분석
  - Among $$ m $$ operations consisting of make-set, find-set, and union, let $$ n $$ be the number of make-set operations.
  > make-set, find-set, union으로 구성된 $$ m $$개의 연산 중에서, $$ n $$은 make-set 연산의 수를 $$ n $$이라고 합시다.
  - Then, the total complexity is $$ O(mlogn) $$.
  > 그러면, 전체 복잡도는 $$ O(mlogn) $$입니다.
    - Because after $$ n $$ make-set operations, there are $$ n $$ nodes; thus, the height of a tree cannot exceeds $$ O(log n) $$.
    > 왜냐하면, $$ n $$번의 make-set 연산 후에는 $$ n $$개의 노드가 있게 되며, 따라서 트리의 높이는 $$ O(log n) $$을 초과하지 않습니다.
    - Thus, $$ m $$ times of the above operations takes $$ O(mlogn) $$
    > 따라서 위의 연산을 $$ m $$번 반복하면 $$ O(mlogn) $$이 소요됩니다.

### Analysis of Path Compression

- **<span style="color:blue">(Amortized) Analysis in on a sequence of operations</span>**
> (상환적)연산 순서에서의 분석
  - Among $$ m $$ operations consisting of make-set, find-set, and union, let $$ n $$ be the number of make-set operations.
  > make-set, find-set, union으로 구성된 $$ m $$개의 연산 중에서, $$ n $$은 make-set 연산의 수를 $$ n $$이라고 합시다.
  - The total complexity is $$ O(mlog*n) $$ (proof is out-of-scope)
  > 전체 복잡도는 $$ O(mlog*n) $$입니다. (증명은 범위를 벗어납니다.)
    
<p align="center">
<img src="/assets/img/blog/disjoint_set_analysis.png">
</p>

  - &rarr; After m operations, it takes $$ O(m) $$ time for a worst case.
  > m번의 연산 후에, 최악의 경우에는 $$ O(m) $$시간이 소요됩니다.
    - On average, each operation takes $$ O(1) $$ time!
    > 평균적으로, 각 연산은 $$ O(1) $$시간이 소요됩니다!
  - <span style="color:red">Disjoint-set with union by-rank and path-compression supports very fast operations.</span>
  > 랭크에 의한 합병과 경로 압축을 사용한 서로소 집합은 매우 빠른 연산을 지원합니다.

## What You Need To Know

- **<span style="color:blue">Disjoint set (a.k.a union-find)</span>**
  - Data structure managing such non-overlapping sets
  > 서로 겹치지 않는 집합을 관리하는 데이터 구조
  - <span style="color:blue">Main operations</span>: make-set, find-set, union
  - Represented by a non-binary <span style="color:blue">parent pointer tree</span>
  > 비이진 부모 포인터 트리에 의해 표현됨
    - For positive integer elements, 1D-array is enough for the purpose
    > 양의 정수 요소의 경우, 1차원 배열이 목적을 충분히 수행할 수 있음
  - Disjoint set is improved by
  > 서로소 집합은 다음 기법들에 의해 개선됨
    - <span style="color:blue">Union by rank</span>: smaller into taller strategy
    - <span style="color:blue">Path compression</span>: flatten the tree while walking up to the root
  - Disjoint set with both techniques is very fast
    - By amortized analysis, each operation takes $$ O(1) $$ time!