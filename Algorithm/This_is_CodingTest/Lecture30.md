# 30강) 다익스트라 최단 경로 알고리즘

## 📍 최단 경로 알고리즘

- **가장 짧은 경로**를 찾는 알고리즘
    - 한 지점에서 다른 한 지점까지의 최단 경로
    - 한 지점에서 다른 모든 지점까지의 최단 경로
    - 모든 지점에서 다른 모든 지점까지의 최단 경로
- 각 `지점`은 그래프에서 `노드`로 표현
- 지점 간 `연결된 도로`는 그래프에서 `간선`으로 표현
- `다이나믹 프로그래밍`의 원리가 적용되었다고 볼 수 있음
    - A → C 로 가는 상황에서 B를 거쳐간다고 할 때 : A → B와 B → C를 모두 고려하기 때문

## 📍 다익스트라 최단 경로 알고리즘 개요

- **특정한 노드에서 출발**하여 다른 **모든 노드로 가는** 최단 경로 계산
- **음의 간선이 없을 때** 정상적으로 동작
    - 현실 세계의 도로(간선)은 음의 간선으로 표현되지 않음
- `그리디 알고리즘`으로 분류
    - 매 상황에서 **가장 비용이 적은 노드를 택해** 임의의 과정 반복하기 때문

## 📍 다익스트라 최단 경로 알고리즘

- **출발 노드** 설정
- **최단 거리 테이블** 초기화
    - 모든 노드 사이의 거리 무한으로 초기화

![0](https://user-images.githubusercontent.com/80563849/172782358-81f11d8c-a6f0-4194-bbcb-45813a06bbe0.png)

- **방문하지 않은** 노드 중에서 **최단거리가 가장 짧은 노드** 선택 → `그리디 알고리즘`으로 분류되는 이유
- 해당 노드를 거쳐 다른 노드로 가는 **비용 계산** → **최단 거리 테이블 갱신**
- 3, 4번 반복

![1](https://user-images.githubusercontent.com/80563849/172782406-9ce8f24e-be2a-4797-97ef-e59486faaa5f.png)

![2](https://user-images.githubusercontent.com/80563849/172782435-9d35f7fe-03c5-4474-a6bc-a642c737e424.png)

![3](https://user-images.githubusercontent.com/80563849/172782462-62f49de2-542d-48a0-95b2-0089904e31ab.png)

![4](https://user-images.githubusercontent.com/80563849/172782483-4ae6a130-9f7c-416b-9159-ebb8362275a2.png)

![5](https://user-images.githubusercontent.com/80563849/172782507-d4fb58bc-2549-4fe9-a4bc-c7337b524a76.png)

- **최단 거리 테이블** : 각 노드에 대한 **현재까지의 최단 거리 정보** 저장
    - 처리 과정에서 더 짧은 경로를 찾으면 ‘이제부터 이 경로가 제일 짧은 경로야’ 라고 갱신함

## 📍 다익스트라 알고리즘의 특징

- `그리디 알고리즘` : 매 상황에서 방문하지 않은 **가장 비용이 적은 노드**를 선택해 임의의 과정 반복
- 단계를 거치며 **한 번 처리된 노드의 최단 거리는 고정** → 더 이상 바뀌지 않음
    - 한 단계당 하나의 노드에 대한 최단 거리를 확실히 찾는 것
- 다익스트라 알고리즘을 수행한 뒤에 테이블에 **각 노드까지의 최단 거리 정보 저장**
    - 완벽한 형태의 최단 경로를 구하려면 소스코드에 추가적인 기능을 넣어야 함

## 📍 다익스트라 알고리즘 간단한 구현

- 단계마다 방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택하기 위해 **매 단계마다 1차원 테이블의 모든 원소를 확인**(`순차 탐색`)

```python
import sys
input = sys.stdin.readline
INF = int(1e9)  # 무한을 의미하는 값으로 10억 설정

# 노드의 개수, 간선의 개수 입력 받기
n, m = map(int, input().split())
# 시작 노드 번호 입력 받기
start = int(input())
# 각 노드에 연결되어 있는 노드에 대한 정보를 담는 리스트 만들기
graph = [[] for i in range(n+1)]
# 방문한 적이 있는지 체크하는 목적의 리스트 만들기
visited = [False] * (n+1)
# 최단 거리 테이블을 모두 무한으로 초기화
distance = [INF] * (n+1)

# 모든 간선 정보를 입력받기
for _ in range(m):
    a, b, c = map(int, input().split())
    # a번 노드에서 b번 노드로 가는 비용이 c라는 의미
    graph[a].append((b,c))

# 방문하지 않은 노드 중에서, 가장 최단 거리가 짧은 노드의 번호를 반환
def get_smallest_node():
    min_value = INF
    index = 0  # 가장 최단 거리가 짧은 노드(인덱스)
    for i in range(1, n+1):
        if distance[i] < min_value and not visited[i]:
            min_value = distance[i]
            index = i
    return index

def dijkstra(start):
    # 시작 노드에 대해서 초기화
    distance[start] = 0
    visited[start] = True
    for j in graph[start]:
        distance[j[0]] = j[1]
    # 시작 노드를 제외한 전체 n-1개의 노드에 대해 반복
    for i in range(n-1):
        # 현재 최단 거리가 가장 짧은 노드를 꺼내서, 방문처리
        now = get_smallest_node()
        visited[now] = True
        # 현재 노드와 연결된 다른 노드를 확인
        for j in graph[now]:
            cost = distance[now] + j[1]
            # 현재 노드를 거쳐서 다른 노드로 이동하는 거리가 더 짧은 경우
            if cost < distance[j[0]]:
                distance[j[0]] = cost

# 다익스트라 알고리즘을 수행
dijkstra(start)

# 모든 노드로 가기 위한 최단 거리를 출력
for i in range(1, n+1):
    # 도달할 수 없는 경우, 무한(INFINITY)이라고 출력
    if distance[i] == INF:
        print("INFINITY")
    else:
        print(distance[i])
```

### 📍 다익스트라 알고리즘 간단한 구현 방법 성능 분석

- O(V)번에 걸쳐서 최단 거리가 가장 짧은 노드를 매번 선형 탐색
- **전체 시간 복잡도**: `O(V**2)`
- 코딩 테스트의 최단 경로 문제에서 전체 노드의 개수가 5,000개 이하라면 이 코드로 해결 가능
    - 노드의 개수가 10,000개를 넘어가는 문제는? ⇒ **우선순위 큐 사용**
    

## 📍 우선순위 큐(Priority Queue)

- `우선순위`가 **가장 높은 데이터**를 **가장 먼저 삭제**하는 자료구조
    - 여러 개의 물건 데이터를 자료구조에 넣었다가 가치가 높은 물건부터 꺼내서 확인해야 하는 경우 우선순위 큐 이용
- Python, C++, Java를 포함한 대부분의 프로그래밍 언어에서 **표준 라이브러리** 형태로 지원

| 자료구조 | 추출되는 데이터 |
| --- | --- |
| 스택(Stack) | 가장 나중에 삽입된 데이터 |
| 큐(Queue) | 가장 먼저 삽입된 데이터 |
| 우선순위 큐(Priority Queue) | 가장 우선순위가 높은 데이터 |

## 📍 힙(Heap)

- **우선순위 큐를 구현하기 위해 사용**하는 자료구조 중 하나
- `최소 힙`(Min Heap): 값이 낮은 데이터부터 추출
- `최대 힙`(Max Heap): 값이 높은 데이터부터 추출

| 우선순위 큐 구현 방식 | 삽입 시간 | 삭제 시간 |
| --- | --- | --- |
| 리스트 | O(1) | O(N) |
| 힙(Heap) | O(logN) | O(logN) |

### 📍 힙 라이브러리 사용 예제 - 최소 힙

```python
import heapq

# 오름차순 힙 정렬(Heap Sort)
def heapsort(iterable):
    h = []
    result = []
    # 모든 원소를 차례대로 힙에 삽입
    for value in iterable:
        heapq.heappush(h, value)
    # 힙에 삽입된 모든 원소를 차례대로 꺼내어 담기
    for i in range(len(h)):
        result.append(heapq.heappop(h))
    return result

result = heapsort([1, 3, 5, 7, 9, 2, 4, 6, 8, 0])
print(result)

# 실행 결과
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### 📍 힙 라이브러리 사용 예제 - 최대 힙

- 최소 힙을 사용하되, 데이터를 넣고 추출할 때 **부호를 바꾸면** 최대 힙 구현 가능

```python
import heapq

# 내림차순 힙 정렬(Heap Sort)
def heapsort(iterable):
    h = []
    result = []
    # 모든 원소를 차례대로 힙에 삽입
    for value in iterable:
        heapq.heappush(h, **-value**)
    # 힙에 삽입된 모든 원소를 차례대로 꺼내어 담기
    for i in range(len(h)):
        result.append(**-heapq.heappop(h)**)
    return result

result = heapsort([1, 3, 5, 7, 9, 2, 4, 6, 8, 0])
print(result)

# 실행 결과
[9, 8, 7, 6, 5, 4, 3, 2, 1, 0]
```

## 📍 다익스트라 알고리즘 개선된 구현

- 단계마다 방문하지 않은 노드 중에서 최단 거리가 가장 짧은 노드를 선택하기 위해 `힙(Heap)` 자료구조 이용
- 다익스트라 알고리즘이 동작하는 **기본 원리는 동일**
    - 간단한 구현 방법과의 차이점: 현재 **가장 가까운 노드를 저장**해 놓기 위해 `힙 자료구조`를 추가적으로 이용한다는 점
    - 현재의 최단 거리가 가장 짧은 노드를 선택해야 하므로 `최소 힙` 사용

```python
import heapq
import sys
input = sys.stdin.readline
INF = int(1e9) # 무한을 의미하는 값으로 10억을 설정

# 노드의 개수, 간선의 개수를 입력받기
n, m = map(int, input().split())
# 시작 노드 번호를 입력받기
start = int(input())
# 각 노드에 연결되어 있는 노드에 대한 정보를 담는 리스트를 만들기
graph = [[] for i in range(n+1)]
# 최단 거리 테이블을 모두 무한으로 초기화
distance = [INF] * (n+1)

# 모든 간선 정보를 입력받기
for _ in range(m):
    a, b, c = map(int, input().split())
    # a번 노드에서 b번 노드로 가는 비용이 c라는 의미
    graph[a].append((b,c))

def dijkstra(start):
    q = []
    # 시작 노드로 가기 위한 최단 경로는 0으로 설정, 큐에 삽입
    heapq.heappush(q, (0, start))
    distance[start] = 0
    while q:  # 큐가 비어있지 않다면
        # 가장 최단 거리가 짧은 노드에 대한 정보 꺼내기
        dist, now = heapq.heappop(q)
        # 현재 노드가 이미 처리된 적이 있는 노드라면 무시
        if distance[now] < dist:
            continue
        # 현재 노드와 연결된 다른 인접한 노드들을 확인
        for i in graph[now]:
            cost = dist + i[1]
            # 현재 노드를 거쳐서, 다른 노드로 이동하는 거리가 더 짧은 경우
            if cost < distance[i[0]]:
                distance[i[0]] = cost
                heapq.heappush(q, (cost, i[0]))

# 다익스트라 알고리즘을 수행
dijkstra(start)

# 모든 노드로 가기 위한 최단 거리를 출력
for i in range(1, n+1):
    # 도달할 수 없는 경우, 무한(INFINITY)이라고 출력
    if distance[i] == INF:
        print("INFINITY")
    else:
        print(distance[i])
```

### 📍 다익스트라 알고리즘 개선된 구현 방법 성능 분석

- 힙 자료구조를 이용하는 다익스트라 알고리즘의 시간 복잡도: `O(ElogV)`
- 노드를 하나씩 꺼내 검사하는 반복문(while문)은 노드의 개수 V 이상의 횟수로는 처리되지 않음
    - 현재 우선순위 큐에서 꺼낸 노드와 연결된 다른 노드들을 확인하는 총횟수는 최대 간선의 개수(E)만큼 연산이 수행될 수 있음
- 전체 과정은 **E개의 원소를 우선순위 큐에 넣었다가 모두 빼내는 연산과 매우 유사**
    - 시간복잡도: O(ElogE)로 판단할 수 있음
    - 중복 간선을 포함하지 않는 경우 → `O(ElogV)`로 정리할 수 있음
        - O(ElogE) → O(ElogV**2) → O(2ElogV) → O(ElogV)
