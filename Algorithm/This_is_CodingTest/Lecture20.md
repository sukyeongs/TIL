# 20강) DFS & BFS 기초 문제 풀이

## 1. 음료수 얼려 먹기

**📌 문제 설명**

- N x M 크기의 얼음 틀. 구멍이 뚫려 있는 부분은 0, 칸막이가 존재하는 부분은 1

- 구멍이 뚫려 있는 부분끼리 상, 하, 좌, 우로 붙어 있는 경우 서로 연결되어 있는 것으로 간주

- 얼음 틀의 모양이 주어졌을 때 생성되는 총 아이스크림의 개수를 구하는 프로그램을 작성하라.

**📌 예시**

입력
````
4 5    # N, M

00110

00011

11111

00000

→ 4 x 5 얼음틀
````

출력
````
3
````

**📌 설명**

- 연결 요소 찾기 - DFS나 BFS로 해결할 수 있음

**1. DFS 활용**

1. 특정한 지점의 주변 상, 하, 좌, 우를 살표본 뒤에 주변 지점 중 값이 ‘0’이면서 아직 방문하지 않은 지점이 있다면 해당 지점 방문
2. 방문한 지점에서 다시 상, 하, 좌, 우를 살펴보면서 방문을 진행을 반복 ⇒ 연결된 모든 지점 방문
3. 모든 노드에 대하여 1~2번 과정 반복, 방문하지 않은 지점의 수를 카운트

```python
# DFS로 특정 노드를 방문하고 연결된 모든 노드들도 방문
def dfs(x, y):
	# 주어진 범위를 벗어나는 경우 즉시 종료
  if x <= -1 or x >= n or y <= -1 or y >= m:
    return False

  # 현재 노드를 아직 방문하지 않았다면
  if graph[x][y] == 0:
    # 해당 노드 방문 처리
    graph[x][y] = 1
    # 상, 하, 좌, 우의 위치들도 모두 재귀적으로 호출
    dfs(x - 1, y)
    dfs(x, y - 1)
    dfs(x + 1, y)
    dfs(x, y + 1)
    return True
  return False

# N, M을 공백을 기준으로 구분하여 입력 받기
n, m = map(int, input().split())

# 2차원 리스트의 맵 정보 입력 받기
graph = []
for i in range(n):
  graph.append(list(map(int, input())))

# 모든 노드(위치)에 대하여 음료수 채우기
result = 0
for i in range(n):
  for j in range(m):
    # 현재 위치에서 DFS 수행
    if dfs(i, j) == True:
      result += 1

print(result)
```

## 2. 미로 탈출

**📌 문제 설명**

- N x M 크기의 미로 / 동빈이의 위치 (1,1), 미로의 출구 (N, M) 한번에 한 칸씩 이동

- 괴물이 있는 부분 0, 괴물이 없는 부분 1

- 동빈이가 탈출하기 위해 움직여야 하는 최소 칸의 개수(시작 칸과 마지막 칸 모두 포함)

**📌 예시**

입력
````
5  6    # N, M

101010

111111

000001

111111

111111
````

출력
````
10
````

**📌 설명**

- BFS 사용 ⇒ 시작 지점에서 가까운 노드부터 차례대로 그래프의 모든 노드 탐색
- 상, 하, 좌, 우로 연결된 모든 노드로의 거리가 1로 동일
    - (1, 1) 지점부터 BFS를 수행하여 모든 노드의 최단 거리 값을 기록하면 해결 가능

**BFS 활용**

```python
from collections import deque

# BFS 구현
def bfs(x, y):
  # Queue 구현을 위해 deque 라이브러리 사용
  queue = deque()
  queue.append((x, y))
  # 큐가 빌 때까지 반복하기
  while queue:
    queue.popleft()
    # 현재 위치에서 4가지 방향으로의 위치 확인
    for i in range(4):
      nx = x + dx[i]
      ny = y + dy[i]
      # 미로 찾기 공가을 벗어난 경우 무시
      if nx < 0 or nx >= n or ny < 0 or ny >= m:
        continue
      # 벽인 경우 무시
      if graph[nx][ny] == 0:
        continue
      # 해당 노드를 처음 방문하는 경우에만 최단 거리 기록
      if graph[nx][ny] == 1:
        graph[nx][ny] = graph[x][y] + 1
        queue.append((nx, ny))

  return graph[n-1][m-1]   

n, m = map(int, input().split())

graph = []
for i in range(n):
  graph.append(list(map(int, input())))

# 이동할 네 가지 방향 정의
dx = [-1, 1, 0, 0]
dy = [0, 0, -1, 1]

print(bfs(0,0))
```