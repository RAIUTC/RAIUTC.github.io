---
layout: post
title: Graph Algorithm
description: |
  이 블로그 글은 그래프 알고리즘을 탐구하며, Kahn의 알고리즘과 DFS를 기반으로 한 위상 정렬에 초점을 맞추고 있습니다. 위상 정렬의 동기와 응용 사례를 살펴보고, 두 알고리즘의 상세한 설명과 예제를 제시합니다. 또한 구현 세부 정보, 시간 복잡도 분석 및 주요 결론을 다룹니다.
categories: 자료구조
sitemap: false
hide_last_modified: true
---

# Graph Algorithm

## Topological sorting

### Motivation

- **<span style="color:blue">Suppose we are going to make a ramen. There are sub-tasks for the purpose.</span>**
> 라면을 만들려고 한다. 이를 위한 하위 작업들이 있다.
  - T1. Turn on the stove
  - T2. Put the egg
  - T3. Put water into the pot
  - T4. Put the ramen
  - T5. Put the powder soup
  - T6. Open the ramen bag

- **<span style="color:blue">How to define the order of sub-tasks?</span>**
> 하위 작업들의 순서를 어떻게 정의할 것인가?

- **<span style="color:blue">One sub-task must be performed before another.</span>**
  - We can <span style="color:red">put a ramen into a pot</span> after <span style="color:blue">turning on the stove</span>.
  - We can <span style="color:red">put an egg</span> after <span style="color:blue">putting the ramen</span>.

- <span style="color:blue">Such dependencies are represented as follows:</span>
> 이러한 의존성은 다음과 같이 표현된다.
  - If task $$ i $$ must precede task $$ j $$, this is represented as a directed edge from task $$ i $$ and task $$ j $$ (i.e., $$ i \rightarrow j $$)
  > 작업 $$ i $$가 작업 $$ j $$보다 앞서야 한다면, 이는 작업 $$ i $$와 작업 $$ j $$ 사이에 방향성 간선으로 표현된다. (즉, $$ i \rightarrow j $$)

<p align="center">
<img src="/assets/img/blog/graph_algorithm_topological_sorting.png">
</p>

### Directed Acyclic Graph

- <span style="color:blue">Topological sort aim to sort nodes in a graph</span>
  - For a directed edge $$ i \rightarrow j $$, node $$ i $$ must precede node $$ j $$ in the sorted result!
  > 방향성 간선 $$ i \rightarrow j $$에 대해, 노드 $$ i $$는 정렬된 결과에서 노드 $$ j $$보다 앞서야 한다!
  - What if there a cycle in the directed graph?
    - Suppose we have a cycle $$ i \rightarrow j \rightarrow k \rightarrow i $$.
    - Node $$ j $$ can precede node $$ i $$ in the result while there is an edge $$ i \rightarrow j $$
    > 간선 $$ i \rightarrow j $$가 있는 동안 노드 $$ j $$는 결과에서 노드 $$ i $$보다 앞서 있을 수 있다.
    - Thus, we cannot do topological sorting in a directed graph having cycles
  - Directed graph having no cycles is called **<span style="color:red">directed acyclic graph (DAG)</span>**
    > 사이클이 없는 방향성 그래프를 방향성 비순환 그래프(DAG)라고 한다.

### Topological Sorting

- **<span style="color:blue">Problem definition</span>**
  - **Input**: a directed acyclic graph (DAG)
  - **Output**: sorted nodes in the topological order
    - For $$ i \rightarrow j $$, node $$ i $$ must precede node $$ j $$ in the sorted result
    > $$ i \rightarrow j $$에 대해, 노드 $$ i $$는 정렬된 결과에서 노드 $$ j $$보다 앞서야 한다.

- **<span style="color:blue">Applications (instruction scheduling)</span>**
  - **Spreadsheet**: to determine the order of formula cell evaluation
  > 수식 셀 평가의 순서를 결정하기 위해
  - **Makefile**: to determine the order of compliation tasks
  > 컴파일 작업의 순서를 결정하기 위해
  - **Tensorflow**: to determine the order of operations in a computational graph
  > 계산 그래프의 작업 순서를 결정하기 위해

## Kahn's Algorithm

- **<span style="color:blue">Kahn's intuition</span>**
  - A node not having incoming edges should precede others!
  > 들어오는 간선이 없는 노드는 다른 노드보다 앞서야 한다!

<p align="center">
<img src="/assets/img/blog/graph_algorithm_kahns_algorithm.png">
</p>

- **<span style="color:blue">Process of Kahn's Algorithm</span>**
  - **Step 1.** Pick a node $$ u $$ not having in-coming edges & push $$ u $$ into queue $$ Q $$ (sorted result)
  > 들어오는 간선이 없는 노드 $$ u $$를 선택하고 큐 $$ Q $$에 $$ u $$를 넣는다 (정렬된 결과)
  - **Step 2.** Remove node $$ u $$ and out-going edges from $$ u $$
  > 노드 $$ u $$와 노드 $$ u $$에서 나가는 간선을 제거한다
    - Repeat Steps 1 & 2 until there are no more nodes to be sorted
    > 더 이상 정렬할 노드가 없을 때까지 단계 1 및 2를 반복한다

### Example

- **<span style="color:blue">Step 1.</span> Pick a node $$ u $$ not having in-coming edges**
  - Then, push $$ u $$ into queue $$ Q $$

<p align="center">
<img src="/assets/img/blog/graph_algorithm_kahns_algorithm_example1.png">
</p>

- **<span style="color:blue">Step 2.</span> Remove node $$ u $$ and out-going edges**

<p align="center">
<img src="/assets/img/blog/graph_algorithm_kahns_algorithm_example2.png">
</p>

- **<span style="color:blue">Step 1.</span> Pick a node $$ u $$ not having in-coming edges**
  - Then, push $$ u $$ into queue $$ Q $$

<p align="center">
<img src="/assets/img/blog/graph_algorithm_kahns_algorithm_example3.png">
</p>

- **<span style="color:blue">Step 2.</span> Remove node $$ u $$ and out-going edges**

<p align="center">
<img src="/assets/img/blog/graph_algorithm_kahns_algorithm_example4.png">
</p>

- **<span style="color:blue">Step 1.</span> Pick a node $$ u $$ not having in-coming edges**
  - Then, push $$ u $$ into queue $$ Q $$

<p align="center">
<img src="/assets/img/blog/graph_algorithm_kahns_algorithm_example5.png">
</p>

- **<span style="color:blue">Step 2.</span> Remove node $$ u $$ and out-going edges**

<p align="center">
<img src="/assets/img/blog/graph_algorithm_kahns_algorithm_example6.png">
</p>

- **<span style="color:blue">Step 1.</span> Pick a node $$ u $$ not having in-coming edges**
  - Then, push $$ u $$ into queue $$ Q $$

<p align="center">
<img src="/assets/img/blog/graph_algorithm_kahns_algorithm_example7.png">
</p>

- **<span style="color:blue">Step 2.</span> Remove node $$ u $$ and out-going edges**

<p align="center">
<img src="/assets/img/blog/graph_algorithm_kahns_algorithm_example8.png">
</p>

- **<span style="color:blue">Step 1.</span> Pick a node $$ u $$ not having in-coming edges**
  - Then, push $$ u $$ into queue $$ Q $$

<p align="center">
<img src="/assets/img/blog/graph_algorithm_kahns_algorithm_example9.png">
</p>

- **<span style="color:blue">Step 2.</span> Remove node $$ u $$ and out-going edges**

<p align="center">
<img src="/assets/img/blog/graph_algorithm_kahns_algorithm_example10.png">
</p>

- **<span style="color:blue">Step 1.</span> Pick a node $$ u $$ not having in-coming edges**
  - Then, push $$ u $$ into queue $$ Q $$

<p align="center">
<img src="/assets/img/blog/graph_algorithm_kahns_algorithm_example11.png">
</p>

### Kahn's Algorithm

- **<span style="color:blue">Pseudocode</span>**

<p align="center">
<img src="/assets/img/blog/graph_algorithm_kahns_algorithm_pseudocode.png">
</p>

- **<span style="color:blue">Implementation details</span>**
  - If we use adjacency list and store out-going edges, it is easy to remove an out-going edge (i.e., $$ O(1) $$ time using iterator)
  > 인접 리스트를 사용하고 나가는 간선을 저장하면 나가는 간선을 제거하기 쉽다 (즉, 반복자를 사용하여 $$ O(1) $$ 시간이 걸림)
  - If we use a queue for $$ S $$, it is easy to remove and push an item (i.e., $$ O(1) $$ time)
  > $$ S $$에 대해 큐를 사용하면 항목을 제거하고 넣기 쉽다 (즉, $$ O(1) $$ 시간)
  - How can we know if a node has in-coming edges or not?
  > 노드가 들어오는 간선이 있는지 여부를 어떻게 알 수 있을까?
    - Use a counter variable c\[v\] to keep tracking the number of in-coming neighbors
    > 들어오는 이웃의 수를 추적하는 카운터 변수 c\[v\]를 사용한다
      - Increase c\[v\] by 1 when $$ u \rightarrow v$$ is inserted into the adjacency list
      - Decrease c\[v\] by 1 when $$ u \rightarrow v$$ is removed from the adjacency list
    - If c\[v\] is 0, then node $$ v $$ hasn't in-coming edges.
    > c\[v\]가 0이면 노드 $$ v $$에 들어오는 간선이 없다.
    - The above operations take $$ O(1) $$ time, respectively
    > 위의 작업은 각각 $$ O(1) $$ 시간이 걸린다

- **<span style="color:blue">Time complexity analysis</span>**

<p align="center">
<img src="/assets/img/blog/graph_algorithm_kahns_algorithm_time_complexity.png">
</p>

- **<span style="color:blue">Limitation</span>**
  - Kahn's algorithm directly modifies the input graph
    - Extra costs occur for checking in-coming edges and removing edges

## Algorithm based on DFS

- **<span style="color:blue">Main intutuin of algorithm based on DFS</span>**
> DFS 기반 알고리즘의 주요 아이디어
  - Suppose we fill nodes reversely in the topological order
  > 노드를 역순으로 채운다고 가정
  - Then, node $$ u $$ can be placed after all its out-going neighbors and descendant are processed
  > 그런 다음, 노드 $$ u $$는 모든 나가는 이웃 및 후손이 처리된 후에 배치될 수 있다
    - Since node $$ u $$ must precede its out-going neighbors
    > 노드 $$ u $$는 반드시 나가는 이웃보다 앞서야 한다

<p align="center">
<img src="/assets/img/blog/graph_algorithm_dfs_based_algorithm.png">
</p>

  - During DFS, push node $$ u $$ inti the stack after DFS of $$ u $$'s out-going neighbors are finished
  > DFS 중에는 노드 $$ u $$를 스택에 넣는다. 이는 노드 $$ u $$의 나가는 이웃들의 DFS가 끝난 후에 이루어진다
    - Do not need to modify the input graph!

<p align="center">
<img src="/assets/img/blog/graph_algorithm_dfs_based_algorithm_example.png">
</p>

- **<span style="color:blue">Pseudocode</span>**

<p align="center">
<img src="/assets/img/blog/graph_algorithm_dfs_based_algorithm_pseudocode.png">
</p>

### Example

- **<span style="color:blue">During DFS, push node $$ u $$ into the stack after DFS of $$ u $$'s out-neighbors are finished</span>**

<p align="center">
<img src="/assets/img/blog/graph_algorithm_dfs_based_algorithm_example1.png">
<img src="/assets/img/blog/graph_algorithm_dfs_based_algorithm_example2.png">
<img src="/assets/img/blog/graph_algorithm_dfs_based_algorithm_example3.png">
<img src="/assets/img/blog/graph_algorithm_dfs_based_algorithm_example4.png">
<img src="/assets/img/blog/graph_algorithm_dfs_based_algorithm_example5.png">
<img src="/assets/img/blog/graph_algorithm_dfs_based_algorithm_example6.png">
<img src="/assets/img/blog/graph_algorithm_dfs_based_algorithm_example7.png">
<img src="/assets/img/blog/graph_algorithm_dfs_based_algorithm_example8.png">
<img src="/assets/img/blog/graph_algorithm_dfs_based_algorithm_example9.png">
<img src="/assets/img/blog/graph_algorithm_dfs_based_algorithm_example10.png">
<img src="/assets/img/blog/graph_algorithm_dfs_based_algorithm_example11.png">
</p>

### What You Need To Know

- **<span style="color:blue">Topological sorting</span>**
  - Sort nodes of a DAG in the topological order
    - For $$ i \rightarrow j $$, node $$ i $$ must precede node $$ j $$ in the sorted result

- **<span style="color:blue">Kahn's algorithm</span>**
  - Remove a node with no in-coming edges step by step
  - Time complexity is $$ O(n + m) $$

- **<span style="color:blue">Algorithm based on DFS</span>**
  - During DFS, push node $$ u $$ into the stack after DFS of $$ u $$'s out-neighbors are finished
    - Without modifying the input graph
  - Time complexity is $$ O(n + m) $$