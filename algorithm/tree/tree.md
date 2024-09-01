- [Tree](#tree)
  - [트리의 개념](#트리의-개념)
  - [트리의 기본 용어](#트리의-기본-용어)
  - [트리의 종류](#트리의-종류)
    - [이진 트리 Binary Tree](#이진-트리-binary-tree)
    - [포화 이진 트리 Full Binary Tree](#포화-이진-트리-full-binary-tree)
    - [완전 이진 트리 Complete Binary Tree](#완전-이진-트리-complete-binary-tree)
    - [편향 이진 트리 Skewed Binary Tree](#편향-이진-트리-skewed-binary-tree)
  - [순회 Traversal](#순회-traversal)
    - [전위 순회](#전위-순회)
    - [중위 순회](#중위-순회)
    - [후위 순회](#후위-순회)
  - [이진 트리의 표현](#이진-트리의-표현)
    - [배열을 이용한 이진 트리의 표현](#배열을-이용한-이진-트리의-표현)
    - [이진 트리의 저장](#이진-트리의-저장)
    - [연결 리스트를 이용한 이진 트리의 표현](#연결-리스트를-이용한-이진-트리의-표현)
  - [수식 트리](#수식-트리)
  - [연습문제](#연습문제)

# Tree
> 트리(tree)는 데이터 구조 중 하나로, 계층적(hierarchical)인 관계를 표현하기 위해 사용한다.  
> 트리는 그래프의 한 종류로, 노드(node)와 노드를 연결하는 간선(edge)로 구성된다. 트리의 중요한 특징은 사이클(cycle)이 없고 모든 노드가 단일 부모 노드를 가진다는 점이다.

- cycle이 없다 : 형제간 간선이 없다

## 트리의 개념
- 비선형 구조
- 원소들 간에 1:N 관계를 가지는 자료구조
- 원소들 간에 계층관계를 가지는 계층형 자료구조
- 상위 원소에서 하위 원소로 내려가면서 확장되는 트리(나무)모양의 구조
- 한 개 이상의 노드로 이루어진 `유한 집합`이며 다음 조건을 만족한다  <p align = 'center'>
      <image src = '../image/tree-fundament.png' width = 500>
    </p>  

  - 노드 중 최상위 노드를 루트(root)라 한다.
  - 나머지 노드들은 n(>=0)개의 분리 집합 $T_1, ..., T_N$으로 분리될 수 있다.
  - $T_1, ..., T_N$은 각각 하나의 트리가 되며 (재귀적 정의)루트의 부트리(subtree)라 한다.

## 트리의 기본 용어
<p align = 'center'>
      <image src = '../image/tree-fundament2.png' width = 500>
    </p>  

- 노드 Node
  - 트리의 원소
  - [예시] 트리 T의 노드 : A, B, C, D, E, F, G, H, I, J, K
- 간선 Edge
  - 노드를 연결하는 선
  - 부모 노드와 자식 노드를 연결
- 루트 노드 Root Node
  - 트리의 최상단에 위치한 노드
  - 모든 트리는 하나의 루트 노드를 가짐
  - 루트 노드에서 다른 모든 노드들이 연결된다
  - [예시] 트리 T의 루트 노드 : A
- 형제 노드 Sibling Node
  - 같은 부모 노드의 자식 노드들
  - [예시] B, C, D의 형제 노드
- 조상 노드
  - 간선을 따라 루트 노드까지 이르는 경로에 있는 모드 노드들
  - [예시] K의 조상 노드 : F, B, A
- 자손 노드
  - 서브 트리에 있는 하위 레벨의 노드들
  - [예시] B의 자손 노드 : E, F, K
- 서브 트리 Subtree
  - 트리의 어떤 노드와 그 노드의 자손들로 이루어진 트리
  - 부모 노드와 연결된 간선을 끊었을 때 생성되는 트리
- 부모 노드 Parent Node
  - 특정 노드에서 한 단계 위에 있는 노드
- 자식 노드 Child Node
  - 특정 노드에서 한 단계 아래에 있는 노드
- 리프 노드 Leaf Node
  - 자식 노드가 없는 노드
  - 트리 끝에 위차한 노드
  - 차수가 0인 노드
- 깊이 Depth
  - 루트 노드에서 특정 노드까지의 간선의 수
- 차수 Degree
  - 노드의 차수 : 노드에 연결된 자식 노드의 수
    - [예시] B의 차수 = 2
    - [예시] C의 차수 = 1
  - 트리의 차수 : 트리에 있는 노의 차수 중에서 가장 큰 값
    - [예시] 트리 T의 차수 = 3
- 높이 Height
  - 특정 노드에서 가장 먼 리프 노드까지의 간선 수
  - 트리의 높이는 루트 노드의 높이로 정의
  - 노드의 높이 : 루트 노드에 이르는 간선의 수, 노드의 레벨
    - [예시] B의 높이 = 1
    - [예시] F의 높이 = 2
  - 트리의 높이 : 트리에 있는 노드의 높이 중에서 가장 큰 값, 최대 레벨
    - [예시] 트리 T의 높이 = 3

## 트리의 종류
### 이진 트리 Binary Tree
> 모든 노드들이 **2개의 서브트리를 갖는 특별한 형태**의 트리 

- 각 노드가 <mark>최대 두개</mark>의 자식 노드를 가지는 트리
- 자식 노드는 보통 `왼쪽 자식(left child)`와 `오른쪽 자식(right child)`으로 구분
- 각 노드가 자식 노드를 최대한 2개 까지만 가질 수 있는 트리
  - 왼쪽 자식 노드 (left child node)
  - 오른쪽 자식 노드 (right child node)
- 이진 트리 예시  <p align = 'center'> <image src = '../image/binary-tree.png' width = 500></p>  
- 레벨 i에서 노드의 최대 개수는 $2^i$개
- 높이가 h인 이진 트리가 가질 수 있는 노드의 
  - 최소 개수는 $h+1$
  - 최대 개수는 $2^{h+1}-1$  
 
  <p align = 'center'> <image src = '../image/binary-tree2.png' width = 500></p>  

### 포화 이진 트리 Full Binary Tree

> 모든 레벨에 노드가 포화상태로 차 있는 이진 트리

- 높이가 h일 때, 최대의 노드 개수인 ($2^{h+1}-1$)의 노드를 가진 이진 트리
  - 높이가 3일때 15개의 노드를 가짐
- 루트를 1번으로 하여 $(2^{h+1}-1)$까지 정해진 위치에 대한 노드 번호를 가짐


### 완전 이진 트리 Complete Binary Tree

높이가 h이고 노드 수가 n일 때 (단, $2^h <= n <= 2^{h+1}-1$) 포화 이진 트리의 노드 번호 1번 부터 n번까지 빈자리가 없는 이진 트리

[예시] 노드가 10개인 완전 이진 트리  
<p align = 'center'> <image src = '../image/complete-binary-tree.png' width = 500></p>  


### 편향 이진 트리 Skewed Binary Tree

<p align = 'center'> <image src = '../image/skewed-binary-tree.png' width = 500></p>  

- 높이 h에 대한 최소 개수의 노드를 가지면서 한쪽 방향의 자식 노드만을 가진 이진 트리
- 종류
  - 왼쪽 편향 이진 트리
  - 오른족 편향 이진 트리  


## 순회 Traversal
> 순회(Traversal)란 트리의 각 노드를 중복되지 않게 전부 방문(visit)하는 것을 말한다

- 트리는 비선형 구조이기 때문에 선형구조에서와 같이 선후 연결 관계를 알 수 없다.

<p align = 'center'> <image src = '../image/tree-traversal.png' width = 300></p> 

- 3가지 기본적인 순회 방법
  - 전위 순회 VLR - Preorder traversal
    1. V 부모 노드 방문
    2. L 왼쪽 자식 노드 방문
    3. R 오른쪽 자식 노드 방문 
  - 중위 순회 LVR - Inorder traversal
    1. L 왼쪽 자식 노드 방문
    2. V 부모 노드 방문
    3. R 오른쪽 자식 노드 방문 
  - 후위 순회 LRV - Postorder Traversal
    1. L 왼쪽 자식 노드 방문
    2. R 오른쪽 자식 노드 방문 
    3. V 부모 노드 방문


### 전위 순회
- 수행 방법
  - 현재 노드 n을 방문하여 <mark>처리</mark>
  - 현재 노드 n의 왼쪽 서브트리로 이동한다
  - 현재 노드의 n의 오른쪽 서브 트리로 이동한다


- 전위 순회 알고리즘
  ```py
  def preorder_traverse(T):
    if T:             # T is not None
      visit(T)        # print(T.item)
      preorder_traverse(T.left)
      preorder_traverse(T.right)
  ```

- 예시  <p align = 'center'> <image src = '../image/preorder-traversal.png' width = 500></p> 


### 중위 순회
- 수행 방법
  - 현재 노드 n의 왼쪽 서브트리로 이동한다
  - 현재 노드 n을 방문하여 <mark>처리</mark>
  - 현재 노드의 n의 오른쪽 서브 트리로 이동한다


- 중위 순회 알고리즘
  ```py
  def inorder_traverse(T):
    if T:             # T is not None
      inorder_traverse(T.left)
      visit(T)        # print(T.item)
      inorder_traverse(T.right)
  ```

- 예시  <p align = 'center'> <image src = '../image/inorder-traversal.png' width = 500></p>  

### 후위 순회
- 수행 방법
  - 현재 노드 n의 왼쪽 서브트리로 이동한다
  - 현재 노드의 n의 오른쪽 서브 트리로 이동한다
  - 현재 노드 n을 방문하여 <mark>처리</mark>


- 후위 순회 알고리즘
  ```py
  def postorder_traverse(T):
    if T:             # T is not None
      postorder_traverse(T.left)
      postorder_traverse(T.right)
      visit(T)        # print(T.item)
  ```

- 예시  <p align = 'center'> <image src = '../image/postorder-traversal.png' width = 500></p> 


## 이진 트리의 표현

### 배열을 이용한 이진 트리의 표현
<p align = 'center'> <image src = '../image/expression-binary-tree.png' width = 500></p> 

- 이진 트리에 각 노드 번호를 다음과 같이 부여
  - 루트의 번호를 1
  - 레벨 n에 있는 노드에 대하여 왼쪽부터 오른족으로 $2^n$부터 $2^{n+1}-1$까지 번호를 차례로 부여
- 배열을 이용한 이진 트리의 표현   

  <p align = 'center'> <image src = '../image/arr-binary-tree.png' width = 300></p> 
  <p align = 'center'> <image src = '../image/arr-binary-tree2.png' width = 500></p> 

  - 노드 번호의 성질
    - 노드 번호가 i인 노드의 부모 번호 → $\lfloor i/2 \rfloor$
    - 노드 번호가 i인 노드의 왼쪽 자식 노드 번호 → $2*i$
    - 노드 번호가 i인 노드의 오른족 자식 노드 번호 → $2*i + 1$
    - 레벨 n의 노드 번호 시작 번호는? → $2^n$
  - 노드 번호를 배열의 인덱스로 사용
    - 높이가 h인 이진 트리를 위한 배열의 크기
      - 레벨 i의 최대 노드 수는? $2^i$
      - 따라서 $1 + 2 + 4+ 8 +...+2 ^i = \sum{2^i}  =2 ^{h+1} - 1$


<p align = 'center'> <image src = '../image/arr-binary-tree3.png' width = 500></p> 

<p align = 'center'> <image src = '../image/arr-binary-tree4.png' width = 500></p> 

### 이진 트리의 저장
- 부모 번호를 인덱스로 자식 번호를 저장  <p align = 'center'> <image src = '../image/save-binary-tree.png' width = 500></p> 
- 자식 번호를 인덱스로 부모 번호를 저장  <p align = 'center'> <image src = '../image/save-binary-tree2.png' width = 500></p> 
- 루트 찾기, 조상 찾기  <p align = 'center'> <image src = '../image/save-binary-tree3.png' width = 500></p> 

📌 배열을 이용한 이진트리의 표현의 단점
- 편향 이진 트리의 경우에 사용하지 않은 배열 원소에 대한 메모리 공간 낭비 발생
- 트리의 중간에 새로운 노드를 삽입하거나 기존의 노드를 삭제할 경우 배열의 크기 변경 어려워서 비효율적

### 연결 리스트를 이용한 이진 트리의 표현

<p align = 'center'> <image src = '../image/binary-tree-and-link.png' width = 600></p> 

- 배열을 이용한 이진 트리의 표현의 단점을 보완하기 위해 연결리스트를 이용하여 트리를 표현 가능
- 연결 자료구조를 이용한 이진 트리의 표현
  - 이진 트리의 모든 노드는 최대 2개의 자식 노드를 가지므로 일정한 구조의 단순 연결 리스트 노드를 사용하여 구현  <p align = 'center'> <image src = '../image/binary-tree-and-link2.png' width = 400></p> 
  

## 수식 트리
<p align = 'center'> <image src = '../image/expression-tree.png' width = 500></p>  
<p align = 'center'> <image src = '../image/expression-tree2.png' width = 500></p>

- 수식을 표현하는 이진 트리
- 수식 이진 트리(Expression Binary Tree)라고 부르기도 함
- 연산자는 루트 노드이거나 가지 노드
- 피연산자는 모두 leaf 노드

## 연습문제
<p align = 'center'> <image src = '../image/tree-example.png' width = 500></p>

```py

'''
13
1 2 1 3 2 4 3 5 3 6 4 7 5 8 5 9 6 10 6 11 7 12 11 13
'''

def preorder(node):
    if node == 0:
        return

    print(node, end=' ')  # 전위 순회
    preorder(left[node])
    # print(node, end=' ')  # 중위 순회
    preorder(right[node])
    # print(node, end=' ')  # 후위 순회

# left, right를 쓰는 버전
N = int(input())  # 정점의 개수(정점: 1~N 번)
arr = list(map(int, input().split()))
# 왼쪽 자식번호를 저장할 리스트
left = [0] * (N+1)
# 오른쪽 자식번호를 저장할 리스트
right = [0] * (N+1)

for i in range(0, len(arr), 2):
    parent, child = arr[i], arr[i+1]

    # 왼족 자식이 없다면, 왼쪽에 삽입
    if left[parent] == 0:
        left[parent] = child
    # 왼쪽 자식은 있는데, 오른쪽 자식이 없다면 오른쪽에 삽입
    else:
        right[parent] = child

# print(left)
# print(right)

root = 1
preorder(root)
```
