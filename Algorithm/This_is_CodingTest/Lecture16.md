# 16강) 스택과 큐 자료구조

그래프 **탐색** 알고리즘: `DFS` / `BFS`

→ 탐색: 많은 양의 데이터 중 원하는 데이터를 찾는 과정

⭐ DFS, BFS: 코테에 자주 등장, 매우 중요

## 📍 스택 자료구조

![스택.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fdf921c9-be4e-40f4-b9fd-0d64c5a4583c/스택.jpeg)

- `먼저 들어온` 데이터가 `나중에 나가는` 형식(= `선입후출`)의 자료구조
- 입구와 출구가 동일한 형태
- DFS 뿐만이 아니라 다른 알고리즘에서도 자주 사용됨

### ⭐ 스택 구현 코드 ⇒ 리스트 사용

```python
# 스택 구현 - 리스트 사용
stack = []

stack.append(5)   # 스택에 5 삽입
stack.append(2)
stack.append(3)
stack.append(7)
stack.pop()   # 스택에서 원소 하나 삭제 => 7이 삭제됨

print(stack[::-1])   # 최상단 원소부터 출력
print(stack)   # 최하단 원소부터 출력
```

- `stack[::-1]` : 리스트 거꾸로 출력
- `append()` , `pop()` : **상수시간** 복잡도 `O(1)`

## 📍 큐 자료구조

![큐.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6afbdbf2-1033-40b6-ac7b-b9a317d6c94e/큐.png)

- `먼저 들어온` 데이터가 `먼저 나가는` 형식(= `선입선출`)의 자료구조
- 입구와 출구가 모두 뚫려있는 형태

### ⭐ 큐 구현 코드 ⇒ deque() 라이브러리 사용

```python
# 큐 구현 - deque() 사용
from collections import deque

queue = deque()   # 큐 생성

queue.append(5)   # 큐에 원소 삽입
queue.append(2)
queue.append(3)
queue.append(7)

queue.popleft()   # 큐에서 원소 삭제 => 5가 삭제됨

print(queue)

queue.reverse()   # 큐 순서 거꾸로 정렬
print(queue)
```

- `deque()` 라이브러리로 큐 구현


### 📍 출처
이것이 취업을 위한 코딩 테스트다 with 파이썬 - 나동빈