# 32강) 최단 경로 알고리즘 기초 문제 풀이

## 1. 전보

**📌 문제 설명**

- **N개**의 도시. 보내고자 하는 메시지가 있는 경우, 다른 도시로 전보를 보내서 해당 메시지 전송 가능
- X → Y 도시로 전보를 보내려면 X에서 Y로 향하는 통로(간선)가 설치되어 있어야 함 ⇒  방향성이 있는 간선
    - X → Y 통로 O, Y → X 통로 X인 경우: Y → X 메시지 보낼 수 없음
- 통로를 거쳐 메시지를 보낼 때, 일정 시간 소요
- **C 도시**에 위급 상황 발생하여 최대한 많은 도시로 메시지를 보내고자 함
- 각 **도시의 번호와 통로**가 설치되어 있는 정보가 주어졌을 때, 도시 C에서 보낸 메시지를 받게 되는 **도시의 개수**는 총 몇 개이며, 도시들이 모두 메시지를 받는 데까지 **걸리는 시간**은 얼마인지 계산하는 프로그램

📌 **입력 예시**

3 2 1

1 2 4

1 3 2

📌 **출력 예시**

2 4

**📌 설명**

- **핵심 아이디어**: 한 도시에서 다른 도시까지의 최단 거리 문제로 치환 가능
- N과 M 범위가 충분히 큼 → `우선순위 큐`를 활용한 `다익스트라 알고리즘`
- 도달 가능한 도시 중에서 가장 거리가 먼 도시를 출력

```python
import heapq
import sys
input = sys.stdin.readline
INF = int(1e9)  # 무한을 의미하는 값으로 10억을 설정

def dijkstra(start):
    q = []
    # 시작 노드로 가기 위한 최단 경로는 0으로 설정, 큐에 삽입
    heapq.heappush(q, (0, start))
    while q:  # 큐가 비어있지 않다면
        # 가장 최단 거리가 짧은 노드에 대한 정보를 꺼내기
        dist, now = heapq.heappop(q)
        if distance[now] < dist:
            continue
        # 현재 노드와 연결된 다른 인접한 노드들을 확인
        for i in graph[now]:
            cost = dist + i[1]
            # 현재 노드를 거쳐서, 다른 노드로 이동하는 거리가 더 짧은 경우
            if cost < distance[i[0]]:
                distance[i[0]] = cost
                heapq.heappush(q, (cost, i[0]))

# 노드의 개수, 간선의 개수, 시작 노드를 입력받기
n, m, start = map(int, input().split())
# 각 노드에 연결되어 있는 노드에 대한 정보를 담는 리스트 만들기
graph = [[] for i in range(n+1)]
# 최단 거리 테이블을 모두 무한으로 초기화
distance = [INF] * (n+1)

# 모든 간선 정보를 입력받기
for _ in range(m):
    x, y, z = map(int, input().split())
    # X번 노드에서 Y번 노드로 가는 비용이 Z라는 의미
    graph[x].append((y,z))

# 다익스트라 알고리즘 수행
dijkstra(start)

# 도달할 수 있는 노드의 개수
count = 0
# 도달할 수 있는 노드 중에서, 가장 멀리 있는 노드와의 최단 거리
max_distance = 0
for d in distance:
    # 도달할 수 있는 노드인 경우
    if d != 1e9:
        count += 1
        max_distance = max(max_distance, d)

# 시작 노드는 제외해야 하므로 count - 1을 출력
print(count - 1, max_distance)
```

## 2. 미래도시

**📌 문제 설명**

- 1~N번까지의 회사. 회사끼리는 도로를 통해 연결되어 있음
- 방문 판매원 A는 1번 회사에 위치, X번 회사에 방문해 물건을 판매하고자 함
- 회사끼리 연결되어 있는 도로를 통해 이동. 연결된 2개의 회사는 양방향으로 이동 가능 (도로 이동 시 소요 시간 1)
- 소개팅 상대는 K번 회사에 위치. X번 회사에 가서 물건을 판매하기 전에 소개팅 상대의 회사에 찾아가 커피를 마실 예정
- A의 목표: 가능한 한 빠르게 1번 회사에서 출발하여 K번 회사를 방문한 뒤에 X번 회사로 가는 것
- 회사 사이를 이동하게 되는 최소 시간을 계산하는 프로그램

📌 **예시**

5 7

1 2

1 3

1 4

2 4

3 4

3 5

4 5

4 5

출력⇒ 3

**📌 설명**

- **핵심 아이디어**: 전형적인 최단 거리 문제 ⇒ `최단 거리 알고리즘`으로 해결
- N의 크기가 최대 **100** ⇒ **플로이드 워셜 알고리즘을 이용해도 효율적**으로 해결 가능
- 플로이드 워셜 알고리즘을 수행한 뒤에 (1번 노드에서 X까지의 최단 거리 + X에서 K까지의 최단 거리)를 계산하여 출력

```python
INF = int(1e9)  # 무한을 의미하는 값으로 10억을 설정

# 노드의 개수 및 간선의 개수 입력받기
n, m = map(int, input().split())
# 2차원 리스트(그래프 표현)를 만들고, 모든 값을 무한으로 초기화
graph = [[INF] * (n+1) for _ in range(n+1)]

# 자기 자신에서 자기 자신으로 가는 비용은 0으로 초기화
for a in range(1, n+1):
    for b in range(1, n+1):
        if a == b:
            graph[a][b] = 0

# 각 간선에 대한 정보를 입력 받아, 그 값으로 초기화
for _ in range(m):
    # A와 B가 서로에게 가는 비용은 1이라고 설정
    a, b = map(int, input().split())
    graph[a][b] = 1
    graph[b][a] = 1

# 거쳐 갈 노드 X와 최종 목적지 노드 K를 입력받기
x, k = map(int, input().split())

# 점화식에 따라 플로이드 워셜 알고리즘 수행
for k in range(1, n+1):
    for a in range(1, n+1):
        for b in range(1, n+1):
            graph[a][b] = min(graph[a][b], graph[a][k] + graph[k][b])

# 수행된 결과를 출력
distance = graph[1][k] + graph[k][x]

# 도달할 수 없는 경우, -1을 출력
if distance >= INF:
    print("-1")

# 도달할 수 있다면, 최단 거리를 출력
else:
    print(distance)
```
