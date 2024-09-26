# Complexity  

알고리즘
- 유한한 단계를 통해 문제를 해결하기 위한 절차나 방법
- 주로 컴퓨터용어, 컴퓨터가 어떤 일을 수행하기 위한 단계쩍 방법을 말함


알고리즘의 효율 : 복잡도(Complexity)는 알고리즘의 성능을 나타내는 척도

복잡도는 `시간 복잡도`와 `공간 복잡도`로 나눌 수 있음.

동일한 기능을 수행하는 알고리즘이 있다면 일반적으로 복잡도가 낮은 것이 좋은 알고리즘이다. (복잡도가 낮을 수록 효율성이 높음)

## Time Complexity
> 특정한 크기의 입력에 대하여 알고리즘이 얼마나 오래걸리는지를 의미함

- <mark>알고리즘을 위해 필요한 연산의 횟수</mark>
- 별 다른 언급이 없으면 `복잡도`는 `시간 복잡도`를 의미.

### Big-O Notation
가장 빠르게 증가하는 항(함수의 상한)만 고려하는 표기법  

|빅오 표기법|명칭|
|---|---|
|$O(1)$|상수 시간 Constant time|
|$O(\log N)$|로그 시간 Log time|
|$O(N)$|선형 시간|
|$O(N\log N)$|로그 선형 시간|
|$O(N^2)$|이차 시간|
|$O(N^3)$|삼차 시간|
|$O(2^n)$|지수 시간|

빅오 표기법에서는 차수가 가장 큰 항만 남기지만, 실제로 N값이 작을 때 상수 값이 미치는 영향력이 매우 큼  

예시 : $3N^3 + 5N^2 + 1,000,000$
- N = 10
- $1,003,500$

일반적인 코딩 테스트 환경에서는 $O(N^3)$을 넘어가면 문제 풀이에서 사용하기 어려움
- CPU 기반의 개인 컴퓨터나 채점용 컴퓨터에서는 연산 횟수가 10억을 넘어가면 C언어를 기준으로 통상 1초 이상의 시간이 소요됨.
- 이때 N의 크기가 5,000이 넘는다면 족히 10초 이상의 시간이 걸릴 수 있음
- 파이썬의 경우
  - 1초당 3000만번
  - $O(2^n)$은 대략 5477이 넘어가면 터짐

||N이 1,000일 때의 연산 횟수|
|---|---|
|$O(N)$|1,000|
|$O(N\log N)$|10,000|
|$O(N^2)$|1,000,000|
|$O(N^3)$|1,000,000,000|

일반적으로 문제를 풀 때의 시간 제한이 1초인 문제에 대한 예시로
- N의 범위가 500인 경우: 시간 복잡도가 $O(N^3)$인 알고리즘을 설계하면 문제를 풀 수 있음
- N의 범위가 2000인 경우: 시간 복잡도가 $O(N^2)$인 알고리즘을 설계하면 문제를 풀 수 있음
- N의 범위가 100000인 경우: 시간 복잡도가 $O(N\log N)$인 알고리즘을 설계하면 문제를 풀 수 있음
- N의 범위가 10000000인 경우: 시간 복잡도가 $O(N)$인 알고리즘을 설계하면 문제를 풀 수 있음



## Space Complexity
> 특정한 크기의 입력에 대하여 알고리즘이 얼마나 많은 메모리를 차지하는지를 의미

- <mark>알고리즘을 위해 필요한 메모리의 양</mark>
- 시간복잡도를 표기했던 것처럼 빅오 표기법을 이용
- 메모리 사용량에도 절대적인 제한이 있음
- `시간 제한 1초, 메모리 제한 128MB`와 같은 문장은 시간 복잡도와 공간 복잡도를 함께 제한하기 위하여 명시함
- 코테 문제는 대부분 `리스트`를 사용해서 풂
- 대부분의 문제는 다수의 데이터에 대한 효율적인 처리를 요구함
- 고전적인 프로그래밍 언어에서 정수형 자료형인 `int`를 기준으로 리스트 크기에 따른 메모리 사용량을 확인 (단, 실제로 컴퓨터 시스템에서 차지하는 메모리양은 컴파일러에 따라 조금씩 다르게 적용)
  - int a[1000] : 4KB
  - int a[1000000] : 4MB
  - int a[2000][2000]: 16MB

보통 메모리 사용량을 128~512MB 정도로 제한.
- 다시 말해 일반적인 경우 데이터의 개수가 1000만 단위가 넘어가지 않도록 알고리즘을 설계해야 함
- 파이썬에서는 int 자료형이 없지만, 파이썬에서도 대략 100만 개 이상의 데이터가 들어갈 수 있는 크기의 리스트를 선언하는 경우는 적다
- 만약 리스트의 크기가 1000만 단위 이상이라면 자신이 알고리즘을 잘못 설계한 것이 아닌지 고민해야함

## Trade-off
**메모리를 많이 사용**하는 대신에 **반복되는 연산을 생략**하거나 더 **많은 정보를 관리**하면서 **계산의 복잡도를 줄일 수 있음**  

이때 메모리를 더 많이 소모 하는 대신에 얻을 수 있는 시간적 이점이 매우 큰 경우가 종종 있음.  

실제로 메모리를 더 많이 사용해서 시간을 비약적으로 줄이는 방법으로 메모이제이션 기법이 있음

## 복잡도 표현
- 시간/공간 복잡도는 입력 크기에 대한 함수료 표기하는데, 이 함수는 주로 여러 개의 항을 가지는 다항식
- 이를 단순한 함수를 표현하기 위해 점근적 표기(Asymptotic Notation)를 사용
- 입력 크기 `n`이 무한대로 커질 때의 복잡도를 간단히 표현하기 위해 사용하는 표기법
- 표기법 종류
  - O(Big-Oh) - 표기 → 최대 시간
  - Ω(Big-Omega) - 표기 → 최소 시간
  - Θ(Big-Theta) - 표기 → 평균 시간


## 수행시간 측정 소스코드
```py
import time
start_time = time.time()
end_time = time.time()
print('time: ', end_time - start_time)
```