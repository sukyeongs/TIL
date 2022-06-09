# 31강) 플로이드 워셜 알고리즘

## 📍 플로이드 워셜 알고리즘 개요

- **모든 노드**에서 다른 **모든 노드**까지의 최단 경로를 모두 계산
- 플로이드 워셜(Floyd-Warshall) 알고리즘은 다익스트라 알고리즘과 마찬가지로 **단계별로 거쳐 가는 노드를 기준**으로 알고리즘 수행
    - But, 매 단계마다 방문하지 않은 노드 중에 최단 거리를 갖는 노드를 찾는 과정이 필요하지 않음
- `2차원 테이블`에 **최단 거리 정보 저장**
- `다이나믹 프로그래밍` 유형에 속함
    - 최단 거리 정보를 **점화식**을 통해 갱신 ⇒ `다이나믹 프로그래밍`
    - 시간 복잡도: `O(N**3)`
    - 노드의 개수가 적을 때 효과적
- 각 단계마다 **특정한 노드 k를 거쳐가는 경우** 확인
    - `a → b`로 가는 최단 거리보다 `a → k → b`로 가는 거리가 **더 짧은지** 검사
- **점화식**은 아래와 같음

```python
Dab = min(Dab, Dak + Dkb)
```

## 📍 플로이드 워셜 알고리즘 동작 과정

![1](https://user-images.githubusercontent.com/80563849/172791174-76b5fab8-1e27-4577-a186-e86746dff6eb.png)

![2](https://user-images.githubusercontent.com/80563849/172791189-996908b3-7d4e-4bd2-bbbd-e447b1b8265e.png)

- 1번 노드를 거쳐 가는 경우를 고려하기 때문에, 시작이 1번 노드이거나 도착이 1번 노드인 경우는 제외 (자기 자신도 포함)

![3](https://user-images.githubusercontent.com/80563849/172791226-0e8b3b88-93f0-49d3-9b03-7c22e81d30f5.png)

![4](https://user-images.githubusercontent.com/80563849/172791249-db80ff54-326c-4d72-a512-3079055e1abd.png)

![5](https://user-images.githubusercontent.com/80563849/172791264-c96bed96-35eb-4a2b-9780-af73874b82a5.png)

## 📍 플로이드 워셜 알고리즘 구현

```python
INF = int(1e9)  # 무한을 의미하는 값으로 10억 설정

# 노드의 개수 및 간선의 개수 입력 받기
n = int(input())
m = int(input())
# 2차원 리스트(그래프 표현)를 만들고, 무한으로 초기화
graph = [[INF] * (n+1) for _ in range(n+1)]

# 자기 자신에서 자기 자신으로 가는 비용은 0으로 초기화
for a in range(1, n+1):
    for b in range(1, n+1):
        if a == b:
            graph[a][b] = 0

# 각 간선에 대한 정보를 입력 받아, 그 값으로 초기화
for _ in range(m):
    # A에서 B로 가는 비용은 C라고 설정
    a, b, c = map(int, input().split())
    graph[a][b] = c

# 점화식에 따라 플로이드 워셜 알고리즘 수행
for k in range(1, n+1):
    for a in range(1, n+1):
        for b in range(1, n+1):
            graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b])

# 수행된 결과를 출력
for a in range(1, n+1):
    for b in range(1, n+1):
        # 도달할 수 없는 경우, 무한(INFINITY)이라고 출력
        if graph[a][b] == INF:
            print("INFINITY", end=" ")
        # 도달할 수 있는 경우 거리를 출력
        else:
            print(graph[a][b], end=" ")
    print()
```

### 📍 플로이드 워셜 알고리즘 성능 분석

- 노드의 개수가 N개일 때 알고리즘 상으로 N번의 단계 수행
    - 각 단계마다 `O(N**2)` 의 연산을 통해 현재 노드를 거쳐 가는 모든 경로 고려
- 총 시간 복잡도 : `O(N**3)`
