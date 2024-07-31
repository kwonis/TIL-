- [2차원 List](#2차원-list)
  - [구조](#구조)
  - [초기화](#초기화)
  - [입력받기](#입력받기)
  - [위치 찾기](#위치-찾기)
  - [순회](#순회)
    - [행 우선 순회](#행-우선-순회)
    - [열 우선 순회](#열-우선-순회)
    - [지그재그 순회](#지그재그-순회)
  - [델타를 이용한 2차 List 탐색](#델타를-이용한-2차-list-탐색)
  - [전치행렬](#전치행렬)
    - [zip](#zip)
- [부분집합](#부분집합)
  - [itertools 라이브러리의 combinations 메서드 사용하기](#itertools-라이브러리의-combinations-메서드-사용하기)
  - [단순 반복문과 배열](#단순-반복문과-배열)
  - [재귀](#재귀)
  - [비트연산](#비트연산)
  

# 2차원 List
## 구조
- 2차원 이상의 다차원 List는 차원에 따라 Index를 선언
- 2차원 List의 선언: 세로길이(행의 개수), 가로 길이(열의 개수)를 필요로 함.

```py
# 2행 4열의 2차원 List
arr =[[0, 1, 2, 3], [4, 5, 6, 7]]
```

## 초기화
📍 파이썬에서는 데이터 초기화를 통해 변수선언과 초기화가 가능

```py
arr = [0, 0, 0, 0, 0]
arr = [0] * 5  # [0, 0, 0, 0, 0]
arr = [i for i in range(2, 9) if i%2 == 0]  # [2, 4, 6, 8]
```
```py
brr = [[1, 2, 3], [1, 2, 3], [1, 2, 3]]
brr = [[1, 2, 3]]*3  # [[1, 2, 3], [1, 2, 3], [1, 2, 3]]
brr = [[1, 2, 3] for i in range(3)]  # [[1, 2, 3], [1, 2, 3], [1, 2, 3]]
brr = [[i, j] for i in range(3) for j in range(2)]  # [[0, 0], [0, 1], [1, 0], [1, 1], [2, 0], [2, 1]]
```

## 입력받기
```py
'''
3 4
0 1 0 0
0 0 0 0
0 0 1 0
'''
# 첫 줄에 n행 m열
# 둘째 줄 부터 n*m의 행열 데이터가 주어질 경우 입력을 받는 방법

## case1
n, m = map(int, input().split())
mylist = [0 for _ in range(n)]
# mylist = [0]*n

for i in range(n):
  mylist[i] = list(map(int, input().split()))

print(mylist)  # [[0, 1, 0, 0], [0, 0, 0, 0], [0, 0, 1, 0]]
```
📌 시퀀스자료형의 `*` 연산자로 반복을 이용하는 방법도 가능  
단, 깊은 복사 주의!

<p align = 'center'>
  <image src = '..\image\list2-copy.png' width = 500>
</p>

```py
# case2
n, m = map(int, input().split())
mylist = []
for i in range(n):
  mylist.append(list(map(int, input().split())))

print(mylist)  # [[0, 1, 0, 0], [0, 0, 0, 0], [0, 0, 1, 0]]
```
```py
# case3
n, m = map(int, input().split())
mylist = [list(map(int, input().split())) for _ in range(n)]  # [[0, 1, 0, 0], [0, 0, 0, 0], [0, 0, 1, 0]]
```

## 위치 찾기
```py
'''
3 4
0 1 0 0
0 0 0 0
0 0 1 0
'''
# 1이 입력된 [행, 열]
n, m = map(int, input().split())
mylist = [list(map(int, input().split())) for _ in range(n)]
newlist = [(i,j) for i in range(n) for j in range(m) if mylist[i][j] == 1]

print(newlist) # [(0, 1), (2, 2)]
```

## 순회
n*m List의 n*m개의 모든 원소를 빠짐없이 조사하는 방법
### 행 우선 순회
```py
arr = [[0, 1, 2, 3],
       [4, 5, 6, 7],
       [8, 9, 10, 11]]

for i in range(len(arr)):
    for j in range(len(arr)):
        arr[i][j] # 필요시 연산 수행
```
### 열 우선 순회
```py
for i in range(len(arr)):
    for j in range(len(arr)):
        arr[j][i] # 필요시 연산 수행
```
### 지그재그 순회
```py
arr = [[0, 1, 2, 3],
       [4, 5, 6, 7],
       [8, 9, 10, 11]]

# i: 행의 좌표, n = len(arr)
# j: 열의 좌표, m = len(arr[0])
for i in range(len(arr)):
    for j in range(len(arr[0])):
        # arr[i][j + (m-1-2*j)*(i%2)]
        arr[i][j + (len(arr[0])-1-2*j)*(i%2)] # 필요시 연산 수행
```

<figure class="half">  
  <a href="link"><img src="..\image\list2-row.png"></a>  
  <a href="link"><img src="..\image\list2-col.png"></a>  
  <a href="link"><img src="..\image\list2-zigzag.png"></a>  
  <figcaption>2개이미지.</figcaption>
</figure>

## 델타를 이용한 2차 List 탐색
- 2차 List의 한 좌표에서 네 방향의 인접 List 요소를 탐색할 때 사용하는 방법
- 델타 값은 한 좌표에서 네 방향의 좌표와 x, y의 차이를 저장한 List로 구형
- 델타 값을 이용하여 특정 원소의 상하좌우에 위치한 원소에 접근할 수 있음
  - 상하좌우에서 더 넓힐 수 있음

📌2차원 List의 가장자리 원소들은 상하좌우 네 방향에 원소가 존재하지 않을 경우가 있으므로, Index를 체크하거나 Index의 범위를 제한해야 함

```py
dx = [0, 0, -1, 1]
dy = [-1, 1, 0, 0]

for x in range(len(arr)):
  for y in range(len(arr[x])):
    for i in range(4):
      testX = x + dx[i]
      testY = y + dy[i]
      print(arr[testX][testY])
```
- right ➡ i+0, j+1
- down ➡ i+1, j+0
- left ➡ i+0, j-1
- up ➡ i-1, j+0

💻 전치행렬 예시 : 풍선팡2
```py
# 테스트 케이스
tc = int(input())
for ind in range(1, tc + 1):
  n, m = map(int, input().split())
  arr = [list(map(int, input().split())) for _ in range(n)]

  # Right, Down, Left, Up
  di = [0, 1, 0, -1]  # 행
  dj = [1, 0, -1, 0]  # 열

  max_value = 0
  for i in range(n):
      for j in range(m):
          score = arr[i][j]
          for k in range(4):
              ni = i + di[k]
              nj = j + dj[k]
              if 0 <= ni < n and 0 <= nj < m:  # 범위 내 있으면
                  score += arr[ni][nj]  # 추가
          if max_value < score:
              max_value = score

  print(f'#{ind} {max_value}')
```

## 전치행렬
📍 행과 열의 값이 반대인 행렬을 의미
```py
# i : 행의 좌표, len(arr)
# j : 열의 좌표, len(arr[0])
arr = [[1, 2, 3], [4, 5, 6], [7, 8, 9]] # 3*3 행렬

for i in range(3):
  for j in range(3):
    if i < j:
      arr[i][j], arr[j][i] = arr[j][i], arr[i][j]
```
- 모든 좌표에 대하여 행과 열의 값을 바꾸게 되면 본래의 모습으로 되돌아오기 때문에 이를 주의해야 함

|`i < j`|`i == j`|`i > j`|`2-i == j`|
|:---:|:---:|:---:|:---:|
|<img src="..\image\list2-ij1.png">|<img src="..\image\list2-ij2.png">|<img src="..\image\list2-ij3.png">|<img src="..\image\list2-ij4.png">|


### zip
`zip(iterable*)`
- 동일한 개수로 이루어진 자료형들을 묶어 주는 역할을 하는 함수
```py
list1 = ['a', 'b', 'c']
list2 = [1, 2, 3]
list12 = list(zip(list1, list2))
print(list12) # [('a', 1), ('b', 2), ('c', 3)]
```

<p align = 'center'>
  <image src = '..\image\list2-zip.png' width = 300>
</p>

```py
arr = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print(list(zip(*arr)))  # [(1, 4, 7), (2, 5, 8), (3, 6, 9)]
```

# 부분집합
- 집합의 원소가 n개일 때, 공집합을 포함한 부분집합의 수는 2^n개.
- 이는 각 원소를 부분집합에 포함시키거나 포함시키지 않는 2가지 경우를 모든 원소에 적용한 경우의 수와 같다.
  - {1, 2, 3, 4} ➡ 2 X 2 X 2 X 2 = 16가지

## itertools 라이브러리의 combinations 메서드 사용하기
🤔

## 단순 반복문과 배열
🤔

## 재귀
🤔

## 비트연산

📌비트 연산자
- `&` : 비트 단위로 AND 연산을 함  
- `|` : 비트 단위로 OR 연산을 함
- `<<` : 피연산자의 비트 열을 왼쪽으로 이동시킴 (왼쪽 쉬프트 연산자)
- `>>` : 피연산자의 비트 열을 오른쪽으로 이동 시킴 (오른쪽 쉬프트 연산자)

```python
a = 5  # 5의 이진 표현 : 0000 0101
b = a << 2 # 5를 왼쪽으로 2비트 쉬프트
print(b) # 20 (0001 0100)
```
`<<n`을 하게 되면 숫자는 2의 'n'의 제곱배로 커지게 됨.
- 2**2 = 4
- 5 * 4

```python
a = 30 # 30의 이진 표현 : 0001 1110
b = a >> 3 # 30을 오른쪽으로 3비트 쉬프트 0000 0011 
print(b)  # 3
```
`>>n`을 하게 되면 숫자는 2의 'n' 제곱배로 나눠지며, 정수형으로 결과가 반환됨
- 2**3 = 8
- 30/8 = 3.75

📌 비트 연산자를 이용하여 부분집합을 생성
```py
for i in range(1<<3):
    print(i, end= " ")
# 0 1 2 3 4 5 6 7

for i in range(2<<3):
    print(i, end= " ")
# 0 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15
```
- `range(1<<n)`을 이용 : 원소가 n개일 경우의 모든 부분집합의 수를 의미

<p align = 'center'>
  <image src = '..\image\list2-bit.png' width = 400>
</p>

- `i & (1<<j)`: i의 j번째 비트가 1인지 아닌지 검사


```py
arr = [3, 6, 7]
n = len(arr)

for i in range(1 << n): # 1<<n : 부분 집합의 개수
    for j in range(n): # 원소의 수 만큼 비트를 비교함
        print(f'#i:{i} j:{j}') 
        if i & (1 << j): #i의 j번 비트가 1인 경우 
            print(f'조건 만족 {arr[j]}') # j번 원소 출력
```

<details>
<summary> 답 </summary>

```py
'''
#i:0 j:0
#i:0 j:1
#i:0 j:2
#i:1 j:0
조건 만족 3
#i:1 j:1
#i:1 j:2
#i:2 j:0
#i:2 j:1
조건 만족 6
#i:2 j:2
#i:3 j:0
조건 만족 3
#i:3 j:1
조건 만족 6
#i:3 j:2
#i:4 j:0
#i:4 j:1
#i:4 j:2
조건 만족 7
#i:5 j:0
조건 만족 3
#i:5 j:1
#i:5 j:2
조건 만족 7
#i:6 j:0
#i:6 j:1
조건 만족 6
#i:6 j:2
조건 만족 7
#i:7 j:0
조건 만족 3
#i:7 j:1
조건 만족 6
#i:7 j:2
조건 만족 7
'''
```

</details>
<br>  

```python
arr = [3, 6, 7, 1, 5, 4]
n = len(arr)

for i in range(1 << n):
    sub_arr = [] # 부분집합 리스트
    for j in range(n):
         if i & (1 << j):
             sub_arr += [arr[j]]
    print(sub_arr)
```
<details>
<summary> 답 </summary>

```py
'''
[]
[3]
[6]
[3, 6]
[7]
[3, 7]
[6, 7]
[3, 6, 7]
[1]
[3, 1]
[6, 1]
[3, 6, 1]
[7, 1]
[3, 7, 1]
[6, 7, 1]
[3, 6, 7, 1]
[5]
[3, 5]
[6, 5]
[3, 6, 5]
[7, 5]
[3, 7, 5]
[6, 7, 5]
[3, 6, 7, 5]
[1, 5]
[3, 1, 5]
[6, 1, 5]
[3, 6, 1, 5]
[7, 1, 5]
[3, 7, 1, 5]
[6, 7, 1, 5]
[3, 6, 7, 1, 5]
[4]
[3, 4]
[6, 4]
[3, 6, 4]
[7, 4]
[3, 7, 4]
[6, 7, 4]
[3, 6, 7, 4]
[1, 4]
[3, 1, 4]
[6, 1, 4]
[3, 6, 1, 4]
[7, 1, 4]
[3, 7, 1, 4]
[6, 7, 1, 4]
[3, 6, 7, 1, 4]
[5, 4]
[3, 5, 4]
[6, 5, 4]
[3, 6, 5, 4]
[7, 5, 4]
[3, 7, 5, 4]
[6, 7, 5, 4]
[3, 6, 7, 5, 4]
[1, 5, 4]
[3, 1, 5, 4]
[6, 1, 5, 4]
[3, 6, 1, 5, 4]
[7, 1, 5, 4]
[3, 7, 1, 5, 4]
[6, 7, 1, 5, 4]
[3, 6, 7, 1, 5, 4]
'''
```

</details>