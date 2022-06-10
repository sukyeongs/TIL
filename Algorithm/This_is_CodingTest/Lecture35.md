# 35강) 크루스칼 

## 📍 신장 트리

- 그래프에서 **모든 노드를 포함**하면서 **사이클이 존재하지 않는** `부분 그래프`
    - **모든 노드**가 포함되어 서로 연결되면서 **사이클이 존재하지 않는다**는 조건은 **트리의 조건**이기도 함
- 모든 노드가 **연결**은 되어있지만, **일부 간선은 사용하지 않아도 되도록 한다**는 점에서 실제 문제에서 효과적으로 사용될 수 있음

## 📍 크루스칼 알고리즘

- 대표적인 **최소 신장 트리 알고리즘**
- `그리디` 알고리즘으로 분류
- 동작 과정
    - 간선 데이터를 `비용`에 따라 `오름차순`으로 정렬
    - 간선을 하나씩 확인하며 현재의 간선이 **사이클을 발생시키는지 확인**
        - 사이클이 **발생하지 않는 경우** **최소 신장 트리에 포함(합집합 연산)**
        - 사이클이 **발생하는 경우** **최소 신장 트리에 포함X**
    - 모든 간선에 대하여 2번의 과정을 반복

( 최종적으로 만들어지는 **최소 신장 트리의 간선 개수**는 `전체 노드의 개수 - 1` )

## 📍 크루스칼 알고리즘 구현

```python
# 특정 원소가 속한 집합 찾기
def find_parent(parent, x):
    # 루트 노드가 아니라면, 루트 노드를 찾을 때까지 재귀적으로 호출
    if parent[x] != x:
        parent[x] = find_parent(parent, parent[x])
    return parent[x]

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

# 모든 간선을 담을 리스트와 최종 비용을 담을 변수
edges = []
result = 0

# 부모 테이블상에서 부모를 자기 자신으로 초기화
for i in range(1, v+1):
    parent[i] = i

# 모든 간선에 대한 정보 입력 받기
for _ in range(e):
    a, b, cost = map(int, input().split())
    # 비용순으로 정렬하기 위해서 튜플의 첫 번째 원소를 비용으로 설정
    edges.append((cost, a, b))

# 간선을 비용순으로 정렬
edges.sort()

# 간선을 하나씩 확인하며
for edge in edges:
    cost, a, b = edge
    # 사이클이 발생하지 않는 경우에만 집합에 포함
    if find_parent(parent, a) != find_parent(parent, b):
        union_parent(parent, a, b)
        result += cost

print(result)
```

## 📍 크루스칼 알고리즘 성능 분석

- 시간 복잡도: 간선의 개수가 E개일 때, `O(ElogE)`
- 가장 많은 시간을 요구하는 곳: **간선을 정렬**하는 부분
    - 표준 라이브러리를 이용하여 E개의 데이터를 정렬하기 위한 시간 복잡도는 `O(ElogE)`
