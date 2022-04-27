# 11강) 파이썬 문법 - 자주 사용되는 표준 라이브러리

## 📍 실전에서 유용한 표준 라이브러리

- `내장 함수` : **기본 입출력** ~ **정렬함수**까지 없어서는 안 될 **필수적인 기능** 함수 제공(`import 없이` 사용)
- `itertools` : **반복되는 형태**의 데이터를 처리하기 위한 유용한 기능 제공 / 특히 `순열`, `조합` 라이브러리 ⇒ `완전 탐색`에서 **모든 경우의 수**를 고려할 때 유용
- `heapq` : **힙(Heap)** 자료구조 제공 / 일반적으로 `우선순위큐` 기능 구현할 때 사용
- `bisect` : **이진탐색**기능 제공
- `collections` : **덱(deque)**, **카운터(counter)** 등 유용한 자료구조 포함
- `math` : 팩토리얼, 제곱근, 최대공약수(GCD), 삼각함수, 파이(pi) 등 **수학적 기능** 제공

### 1. 자주 사용되는 내장 함수

- sum() : 모든 요소를 더함
```python
result = sum([1, 2, 3, 4, 5])   # 매개변수로 집합, 튜플 다 가능

print(result)
=> 15
```

- min(), max() : 최솟값, 최댓값
```python
min_result = min(7, 3, 5, 2)   # 매개변수로 리스트, 집합, 튜플 다 가능
max_result = max(7, 3, 5, 2)

print(min_result, max_result)
=> 2  7
```

- eval() : 매개변수로 받은 문자열을 계산
```python
result = eval("(3+5)*7")

print(result)
=> 56
```

- sorted() : 정렬
```python
result = sorted([9, 1, 8, 5, 4])
reverse_result = sorted([9, 1, 8, 5, 4], reverse = True)


# sorted() with key
array = [('홍길동', 50), ('이순신', 32), ('아무개', 74)]   # 튜플 리스트
result = sorted(array, key=lambda x:x[1], reverse = True)
```

### 2. 순열과 조합(itertools 라이브러리)

- 모든 경우의 수를 고려해야 할 때

- `순열` : 서로 다른 n개에서 r개를 택하여 **일렬로 나열**

```python
from itertools import permutations

data = ['A', 'B', 'C']
result = list(permutations(data, 3))

print(result)
=> [('A', 'B', 'C'), ('A','C','B'), ('B', 'A', 'C'), ...]
```

- `조합` : 서로 다른 n개에서 **순서 상관없이** r개를 택하는 것

```python
from itertools import combinations

data = ['A', 'B', 'C']
result = list(combinations(data, 2))

print(result)
=> [('A', 'B'), ('A','C'), ('B', 'C')]
```

- `중복 순열`

```python
from itertools import product

data = ['A', 'B', 'C']
result = list(product(data, repeat=2))
```

- `중복 조합`

```python
from itertools import combinations_with_replacement

data = ['A', 'B', 'C']
result = list(combinations_with_replacement(data, 2))
```

### 3. Counter

- collections 라이브러리의 `Counter`
- **등장 횟수**를 셈
- 리스트같이 **반복가능한 객체**가 주어졌을 때, 내부의 원소가 몇 번씩 등장했는지 알려줌

```python
from collections import Counter

counter = Counter(['red', 'blue', 'red', 'green', 'blue', 'blue'])

print(counter['blue'])
=> 3

print(dict(counter))
=> {'red': 2, 'blue': 3, 'green': 1}   # 사전 자료형으로 변환
```

### 4. 최대공약수와 최소공배수

```python
import math

# 최소 공배수를 구하는 함수
def lcm(a, b):
		return a * b // math.gcd(a, b)   # math.gcd(a, b) : 최대공약수를 구하는 함수

print(math.gcd(21, 14))   # 최대공약수 계산
print(lcm(21, 14))   # 최소공배수 계산
```

### 📍 출처
이것이 취업을 위한 코딩 테스트다 with 파이썬 - 나동빈