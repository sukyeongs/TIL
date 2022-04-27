# 19강) BFS 알고리즘


## 📍 BFS(Breadth-First Search)  
- 너비우선탐색/그래프에서 가까운 노트부터 우선적으로 탐색
- 큐 자료구조 이용
    - 탐색 시작 노드를 큐에 삽입, 방문처리
    - 큐에서 노드 꺼낸 후, 해당 노드의 인접 노드 중에서 방문하지 않은 노드를 모두 큐에 삽입, 방문처리
    - 2번의 과정을 수행할 수 없을 때까지 반복
- 코테에서 자주 출제됨
- 특정 조건에서의 최단경로 문제에서 효과적으로 사용
- 거리가 가까운  노드부터 우선 탐색

```python
from collections import deque

# BFS 메서드 정의
def bfs(graph, start, visited):
	# 큐 구현을 위해 deque 라이브러리 사용
	queue = deque([start])   # 시작 노드를 큐에 삽입
	# 현재 노드 방문처리
	visited[start] = True
	# 큐가 빌 때까지 반복
	while queue:
		# 큐에서 하나의 원소 뽑아 출력
		v = queue.popleft()
		print(v, end=' ')
		# 아직 방문하지 않은 인접한 원소들을 큐에 삽입
		for i in graph[v]: 
				if not visited[i]:
					queue.append(i)
					visited[i] = True

# 각 노드가 연결된 정보를 표현(2차원 리스트)
graph = [
	[],
	[2,3,8],
	[2,3,8],
	[2,3,8],
	[2,3,8],
	[2,3,8],
	[2,3,8],
	[2,3,8],
	[2,3,8]
]

# 각 노드가 방문된 정보를 표현(1차원 리스트)
visited = [False] * 9

# 정의된 BFS 함수 호출
bfs(graph, 1, visited)
```