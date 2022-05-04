# 21강) 선택 정렬

## 📍 정렬(Sorting)

- 데이터를 특정 기준에 따라 순서대로 나열하는 것
- 문제 상황에 다라 적절한 정렬 알고리즘이 **공식**처럼 사용됨

## 📍 선택 정렬

- 처리되지 않은 데이터 중에서 `가장 작은 데이터`를 선택해 **맨 앞에 있는 데이터와 바꾸는 것**을 반복
- `이중 반복문`으로 구현

```python
array = [7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

for i in range(len(array)):
	min_index = i   # 가장 작은 원소의 인덱스
	for j in range(i+1, len(array)):
			if array[min_index] > array[j]:
					min_index = j
	array[i], array[min_index] = array[min_index], array[j]

print(array)
```

## 📍 선택 정렬의 시간 복잡도

- N번만큼 가장 작은 수를 찾아서 맨 앞으로 보내야 함
- 전체 연산 횟수: `N` + `(N-1)` + `(N-2)` + ... + `2`  = (N**2 + N - 2)/2 ⇒ `O(N**2)`


### 📍 출처
이것이 취업을 위한 코딩 테스트다 with 파이썬 - 나동빈