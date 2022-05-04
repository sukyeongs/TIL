# 23강) 퀵 정렬

## 📍 퀵 정렬

- `기준 데이터`를 설정하고, 그 기준보다 **큰 데이터**와 **작은 데이터**의 **위치를 바꾸는 방법**
- 일반적인 상황에서 `가장 많이 사용되는 정렬 알고리즘` 중 하나
- **병합 정렬**과 더불어 대부분의 프로그래밍 언어의 **정렬 라이브러리의 근간**이 되는 알고리즘
- 가장 `기본`적인 퀵 정렬: **첫 번째 데이터**를 **기준 데이터(Pivot)**으로 설정

## 📍 퀵 정렬의 시간 복잡도

- `O(NlogN)`
- 최악의 경우: `O(N**2)`
    - **이미 정렬 되어있는** 데이터의 경우
- 표준 라이브러리 사용 시 `O(NlogN)` 보장

```python
array = [7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

def quick_sort(array, start, end):
	if start >= end:   # 원소가 1개인 경우 종료
			return
	pivot = start
	left = start + 1
	right = end
	while(left <= right):
		# 피벗보다 큰 데이터를 찾을 때까지 반복
		while(left <= end and array[left] <= array[pivot]):
			left += 1
		# 피벗보다 작은 데이터를 찾을 때까지 반복
		while(right > start and array[right] >= array[pivot]):
			right -= 1
		if(left > right):  # 엇갈렸다면 작은 데이터와 피벗 교체
			array[right], array[pivot] = array[pivot], array[right]
		else:  # 엇갈리지 않았다면 작은 데이터와 큰 데이터 교체
			array[left], array[right] = array[right], array[left]
	# 분할 이후 왼쪽 부분과 오른쪽 부분에서 각각 정렬 수행
	quick_sort(array, start, right-1)
	quick_sort(array, right+1, end)

quick_sort(array, 0, len(array)-1)
print(array)
```

## 📍 파이썬의 장점을 살린 퀵 정렬 구현

```python
array = [7, 5, 9, 0, 3, 1, 6, 2, 4, 8]

def quick_sort(array):
	# 리스트가 하나 이하의 원소만을 담고 있다면 종료
	if len(array) <= 1:
			return array
	pivot = array[0]  # 피벗은 첫 번째 원소
	tail = array[1:]  # 피벗을 제외한 리스트
		
	left_side = [x for x in tail if x <= pivot]  # 분할된 왼쪽 부분
	right_side = [x for x in tail if x >= pivot]  # 분할된 오른쪽 부분

	return quick_sort(left_side) + [pivot] + quick_sort(right_side)

print(quick_sort(array))
```


### 📍 출처
이것이 취업을 위한 코딩 테스트다 with 파이썬 - 나동빈