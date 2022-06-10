# 33강) 서로소 집합 자료구조

## 📍 서로소 집합(Disjoint Sets) 자료구조

- `서로소 집합` : 공통 원소가 없는 두 집합
- 서로소 부분 집합들로 나누어진 원소들의 데이터를 처리하기 위한 자료구조
- 두 종류의 연산 가능
    - **합집합(Union)**: 두 개의 원소가 포함된 집합을 **하나의 집합**으로 합치는 연산
    - **찾기(Find)**: 특정한 원소가 속한 집합이 어떤 집합인지 알려주는 연산
- `합치지 찾기(Union Find)` 자료구조라고 불리기도 함
- 동작 과정
    - 합집합 연산을 확인하여 서로 연결된 두 노드 A, B 확인
        - A와 B의 루트노드 A’, B’ 각각 찾기
        - A’를 B’의 부모 노드로 설정
    - 모든 합집합 연산을 처리할 때까지 위 과정 반복

![1](https://user-images.githubusercontent.com/80563849/173015687-44a26288-49e7-46f4-9211-8f4d731b76d8.png)

- 기본적인 형태의 서로소 집합 자료구조에서는 **루트 노드에 즉시 접근할 수 없음**
    - 루트 노드를 찾기 위해 부모 테이블을 **계속해서 확인**하며 거슬러 올라가야함

## 📍 서로소 집합 자료구조 기본적인 구현

```python
# 특정 원소가 속한 집합을 찾기
def find_parent(parent, x):
    # 루트 노드를 찾을 때까지 재귀 호출
    if parent[x] != x:
        return find_parent(parent, parent[x])
    return x

# 두 원소가 속한 집합을 합치기
def union_parent(parent, a, b):
    a = find_parent(parent, a)
    b = find_parent(parent, b)
    if a < b:
        parent[b] = a
    else:
        parent[a] = b

# 노드의 개수와 간선(Union 연산)의 개수 입력 받기
v, e = map(int, input().split())
parent = [0] * (v+1)  # 부모 테이블 초기화

# 부모 테이블상에서 부모를 자기 자신으로 초기화
for i in range(1, v+1):
    parent[i] = i

# Union 연산을 각각 수행
for i in range(e):
    a, b = map(int, input().split())
    union_parent(parent, a, b)

# 각 원소가 속한 집합 출력하기
print('각 원소가 속한 집합: ', end='')
for i in range(1, v+1):
    print(find_parent(parent, i), end='')

print()

# 부모 테이블 내용 출력하기
print('부모 테이블: ', end='')
for i in range(1, v+1):
    print(parent[i], end='')
```

## 📍 서로소 집합 자료구조 기본적인 구현 방법의 문제점

- 합집합(Union) 연산이 편향되게 이루어지는 경우 **찾기 함수가 비효율적**으로 동작
- **최악의 경우**에는 찾기 함수가 모든 노드를 다 확인하게 되어 시간 복잡도가 `O(V)`

⇒ `경로 압축`으로 최적화

## 📍 서로소 집합 자료구조 경로 압축(Path Compression)

- 찾기 함수를 `최적화`하기 위한 방법
    - 찾기 함수를 재귀적으로 호출한 뒤에 부모 테이블 값을 바로 갱신

```python
# 특정 원소가 속한 집합을 찾기
def find_parent(parent, x):
    # 루트 노드가 아니라면, 루트 노드를 찾을 때까지 재귀적으로 호출
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]
```
