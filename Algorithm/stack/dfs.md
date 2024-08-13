<!-- TOC start (generated with https://github.com/derlin/bitdowntoc) -->

- [깊이 우선 탐색 DFS; Depth-First Search](#깊이-우선-탐색-dfs-depth-first-search)
  - [DFS 주요 특징](#dfs-주요-특징)
  - [DFS의 동작 방식](#dfs의-동작-방식)
  - [DFS의 구현](#dfs의-구현)
    - [DFS 알고리즘 구현 단계](#dfs-알고리즘-구현-단계)
  - [DFS의 응용](#dfs의-응용)

<!-- TOC end -->


# 깊이 우선 탐색 DFS; Depth-First Search

> 💡 그래프나 트리 구조를 탐색하는 데 사용되는 알고리즘으로, 
가능한 깊이 들어가면서 방문하지 않는 노드를 탐색하며, 
더 이상 깊이 들어갈 수 없을 때 이전 노드로 돌아가서 다른 경로를 탐색. 
주로 그래프의 모든 정점을 방문하거나 특정 정점을 찾는 데 사용


## DFS 주요 특징

- **탐색 방식**:
  - DFS는 한 정점에서 시작하여 가능한 한 깊이 탐색을 진행
  - 더 이상 진행할 수 없는 상태가 되면, 이전의 노드로 돌아가서 다른 경로를 탐색
    > 시작 정점의 한 방향으로 갈 수 있는 경로가 있는 곳까지 깊이 탐색해 가다가 더 이상 갈 곳이 없게 되면, 가장 마지막에 만났던 갈림길 간선이 있는 정점으로 되돌아와서 다른 방향의 정점으로 탐색을 계속 반복하여 결국 모든 정점을 방문하는 순회 방법
- **구현 방법: ⁉ 꼭 스택만 있는게 아니라는 점을 알아두기**
  - **재귀적 구현**: 함수가 자기 자신을 호출하여 탐색을 진행
  - **스택 기반 구현**: 스택을 사용하여 탐색할 노드를 관리 (스택은 LIFO(Last In, First Out) 구조입니다.)
    > 가장 마지막에 만났던 갈림길의 정점으로 되돌아가서 다시 깊이 우선 탐색을 반복해야 하므로 후입선출 구조의 스택 사용
- **시간 복잡도**:
  - 그래프의 정점 수를 V, 간선 수를 E라고 할 때,  
    DFS의 시간 복잡도는 O(V+E)
        
- **공간 복잡도**:
  - 스택을 사용하는 경우, 최악의 경우 O(V)의 공간이 필요

## DFS의 동작 방식
1. **시작**:
   - 시작 정점을 선택하고, 이 정점을 방문합니다.
   - 방문한 정점을 기록하여 무한 루프를 방지합니다.
2. **재귀 호출 (또는 스택 사용)**:
   - 현재 정점의 모든 인접 정점에 대해, 그 정점이 방문되지 않은 경우 재귀 호출(또는 스택에 푸시)하여 깊이 탐색을 계속합니다.
3. **백트래킹**:
   - 모든 인접 정점을 탐색한 후에는 이전 정점으로 돌아가서 다른 경로를 탐색합니다.
4. **종료**:
   - 모든 정점이 방문되거나, 특정 조건(예: 목표 정점 도달)이 충족될 때 탐색을 종료합니다.

## DFS의 구현

- 재귀적 구현
    
    ```python
    def dfs_recursive(graph, node, visited):
        if node not in visited:
            visited.add(node)
            print(node)  # 노드 방문 처리
            for neighbor in graph[node]:
                dfs_recursive(graph, neighbor, visited)
    
    # 예제 사용법
    graph = {
        'A': ['B', 'C'],
        'B': ['A', 'D', 'E'],
        'C': ['A', 'F'],
        'D': ['B'],
        'E': ['B', 'F'],
        'F': ['C', 'E']
    }
    visited = set()
    dfs_recursive(graph, 'A', visited)
    
    # A
    # B
    # D
    # E
    # F
    # C
    ```
    
- 스택 기반 구현
    
    ```python
    def dfs_stack(graph, start):
        visited = set()
        stack = [start]
        
        while stack:
            node = stack.pop()
            if node not in visited:
                visited.add(node)
                print(node)  # 노드 방문 처리
                stack.extend(neighbor for neighbor in graph[node] if neighbor not in visited)
    
    # 예제 사용법
    graph = {
        'A': ['B', 'C'],
        'B': ['A', 'D', 'E'],
        'C': ['A', 'F'],
        'D': ['B'],
        'E': ['B', 'F'],
        'F': ['C', 'E']
    }
    dfs_stack(graph, 'A')
    
    # A
    # C
    # F
    # E
    # B
    # D
    ```
    
    ```python
    # 슈도코드
    visited[], stack[] 초기화
    DFS(V)
    	시작점 V 방문;
    	visited[v] <- true:
    	while{
    		if (v의 인접 정점 중 방문 안한 정점 w가 있으면)
    			push(v);
    			v <- w; (w에 방문)
    			visited[w] <- True;
    		else:
    			if (스택이 비어 있지 않으면)
    				v <- pop(stack)
    			else:
    				break
    	}
    end DFS()
    ```
    
<details>
<summary>DFS 알고리즘 구현 단계</summary>
    
### DFS 알고리즘 구현 단계
    
1. 시작 정점 v를 결정하여 방문한다.
  1. 정점 v에 인접한 정점 중에서
      1. 방문하지 않은 정점 w가 있으면
          1. 정점 v를 스택에 push하고
          2. 정점 w를 방문
          3. 그리고 w를 v로 하여 다시 2번을 반복
      2. 방문하지 않은 정점이 없으면,
          1. 탐색의 방향을 바꾸기 위해서 스택을 pop하여 받은 가장 마지막 방문 정점을 v로 하여 다시 2번 반복
  2. 스택이 공백이 될 때까지 2번을 반복
---
1. 초기 상태: 배열 visited를 False로 초기화하고, 공백 스택을 생성
        
    <p align = 'center'>
    <image src = '..\image\stack-dfs1.png' width = 500>
    </p>
        
2. 정점 A를 시작으로 깊이 우선 탐색을 시작

    <p align = 'center'>
    <image src = '..\image\stack-dfs2.png' width = 500>
    </p>
        
3. 정점 A에 방문하지 않은 정점 B, C가 있으므로 A를 스택에 push하고, 인접정점 B와 C 중에서 **오름차순**에 따라 B를 선택하여 탐색을 계속한다.

    <p align = 'center'>
    <image src = '..\image\stack-dfs3.png' width = 500>
    </p>    
    
4. 정점 B에 방문하지 않은 정점 D, E가 있으므로 B를 스택에 push하고, 인접정점 D와 E중에서 **오름차순**에 따라 D를 선택하여 탐색을 계속한다
  
    <p align = 'center'>
    <image src = '..\image\stack-dfs4.png' width = 500>
    </p>    

5. 정점 D에 방문하지 않은 정점 F가 있으므로 D를 스택에 push하고, 인접정점 F를 선택하여 탐색을 계속한다.

    <p align = 'center'>
    <image src = '..\image\stack-dfs5.png' width = 500>
    </p>    
  
6. 정점 F에 방문하지 않은 정점 E, G가 있으므로 F를 스택에 push 하고, 인접정점 E와 G 중에서 오름차순에 따라 E를 선택하여 탐색을 계속한다.
  
    <p align = 'center'>
    <image src = '..\image\stack-dfs6.png' width = 500>
    </p>    

7.  정점 E에 방문하지 않은 정점 C가 있으므로 E를 스택에 push하고, 인접정점 C를 선택하여 탐색을 계속한다.

    <p align = 'center'>
    <image src = '..\image\stack-dfs7.png' width = 500>
    </p>    
  
8.  정점 C에서 방문하지 않은 인접정점이 없으므로, 마지막 정점으로 돌아가기 위해 스택을 pop하여 받은 정점 E에 대해서 방문하지 않은 인접정점이 있는지 확인

    <p align = 'center'>
    <image src = '..\image\stack-dfs8.png' width = 500>
    </p>    

  
9.  정점 E는 방문하지 않은 인접정점이 없으므로, 다시 스택을 pop하여 받은 정점 F에 대해서 방문하지 않은 인접정점이 있는지 확인한다.
  
    <p align = 'center'>
    <image src = '..\image\stack-dfs9.png' width = 500>
    </p>    

10. 정점 F에 방문하지 않은 정점 G가 있으므로 F를 스택에 push하고, 인접정점 G를 선택하여 탐색을 계속한다.

    <p align = 'center'>
    <image src = '..\image\stack-dfs10.png' width = 500>
    </p>    
  
11. 정점 G에서 방문하지 않은 인접정점이 없으므로, 마지막 정점으로 돌아가기 위해 스택을 pop하여 받은 정점 F에 대해서 방문하지 않은 인접정점이 있는지 확인

    <p align = 'center'>
    <image src = '..\image\stack-dfs11.png' width = 500>
    </p>    
  
12. 정점 F에서 방문하지 않은 인접정점이 없으므로, 다시 마지막 정점으로 돌아가기 위해 스택을 pop하여 받은 정점 D에 대해서 방문하지 않은 인접정점이 있는지 확인한다.

    <p align = 'center'>
    <image src = '..\image\stack-dfs12.png' width = 500>
    </p>    

13. 정점 D에서 방문하지 않은 인접정점이 없으므로, 다시 마지막 정점으로 돌아가기 위해 스택을 pop하여 받은 정점 B에 대해서 방문하지 않은 인접정점이 있는지 확인한다.
  
    <p align = 'center'>
    <image src = '..\image\stack-dfs13.png' width = 500>
    </p>    

  
14. 정점 B에서 방문하지 않은 인접정점이 없으므로, 다시 마지막 정점으로 돌아가기 위해 스택을 pop하여 받은 정점 A에 대해서 방문하지 않은 인접정점이 있는지 확인한다.
  
    <p align = 'center'>
    <image src = '..\image\stack-dfs14.png' width = 500>
    </p>    
  
15. 현재 정점 A에서 방문하지 않은 인접 정점이 없으므로 마지막 정점으로 돌아가기 위해 스택을 pop하는데, 스택이 공백이므로 깊이 우선 탐색을 종료한다.

    <p align = 'center'>
    <image src = '..\image\stack-dfs15.png' width = 500>
    </p>    
        
    
---

입력은 보통 노드 수와 간선 개수를 알려줌

그리고 인접 정점 정보를 1-2, 2-4, 2-5 이런식으로 알려줌

```python
'''
1
7 8
1 2 1 3 2 4 2 5 4 6 5 6 6 7 3 7
'''

def DFS(s, V):          # s: 시작 정점, V 정점 개수(1번 부터인 정점의 마지막 정점)
    visited = [0]*(V+1) # 방문한 정점을 표시
    stack = []          # 스택 생성
    print(s)
    visited[s] = 1      # 시작정점 방문 표시
    v = s
    while True:
        for w in adjL[v]:       # v에 인접하고, 방문안한 w가 있으면
            if visited[w] == 0:
                stack.append(v) # push(v) 현재 정점을 push
                v = w
                print(v)        # w에 방문
                visited[w] = 1  # w에 방문 표시
                break # for w에 대한 break # v부터 다시 탐색
        else:                   # 남은 인접정점이 없어서 break가 걸리지 않은 경우
            if stack:           # 이전 갈림길을 스택에서 꺼내서
                v = stack.pop()
            else:
                break # while에 대한 break

T = int(input())
for tc in range(1, T+1):
    V, E = map(int, input().split())

    # adjl = [[], [2, 3] ... ]
    adjL = [[] for _ in range(V+1)]
    arr = list(map(int, input().split()))

    for i in range(E):
        v1, v2 = arr[i*2], arr[i*2+1]
        adjL[v1].append(v2) # 노드 별로 인접한 행렬  정보 입력하기

    DFS(1,V)
    

# 1
# 2
# 4
# 6
# 7
# 5
# 3
```
</details>

## DFS의 응용

- **경로 찾기**: 특정 정점으로 가는 경로를 찾는 데 사용될 수 있습니다.
- **정점의 연결성 검사**: 그래프의 모든 정점이 서로 연결되어 있는지 확인합니다.
- **사이클 탐지**: 그래프에 사이클이 존재하는지 검사합니다.
- **토폴로지 정렬**: DAG(Directed Acyclic Graph)에서 정점의 순서를 정렬합니다.

DFS는 그래프의 구조와 성질을 깊이 탐색하는 데 유용하며, 다양한 그래프 관련 문제를 해결하는 데 중요한 알고리즘입니다.