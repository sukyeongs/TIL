# 9강) 파이썬 문법 - 반복문

## 📍 while / for

- for문이 주로 더 간결

### 1. while문

```python
i = 1
result = 0

while i <= 9:   # while 뒤가 True일 때까지 실행
		result += i
		i += 1
```

`무한루프` : **끊임없이 반복**되는 반복 구문

코테에서는 무한루프를 구현할 일이 **거의 없음**

⇒ 반복문 안에 **탈출할 만한 요소**가 있는지 꼭 유의하기

### 2. for문

```python
array = [9, 8, 7, 6, 5]

for i in array:
		print(i)
```

- 연속적인 값을 순회할 때 : `range()` 사용
    - range(시작, **끝값+1**)
    - range의 인자가 하나인 경우 : 시작값이 0
    
    ```python
    result = 0
    
    for i in range(1, 10):   # 1부터 9까지 순회
    		result += i
    
    print(result)
    => 45
    ```
    

## 📍 반복문에서 자주 사용되는 키워드

- `continue` : 남은 코드 실행을 건너뛰고, 다음 반복 진행

```python
result = 0

for i in range(1, 10):
		if i % 2 == 0:   # i가 짝수면 넘어감
				continue
		result += i
```

- `break` : 반복문 즉시 탈출

```python
i = 1

while True:
		print(i)
		if i == 5:
				break   # i가 5면 탈출 (출력은 5까지 함)
		i += 1
```

- 반복문 사용 예시 : 특정 번호인 학생을 제외한 시험 합격 인원 체크

```python
scores = [90, 85, 79, 65, 97]

cheating_student_list = {2, 4}   # 집합 => 유무 확인에 용이

for i in range(5):
		if i+1 in cheating_student_list:
				continue
		if scores[i] >= 80:
				print(i+1, "번 합격")
```

## 📍 중첩된 반복문(이중 반복문)

```python
for i in range(2, 10):
		for j in range(1, 9):
				print(i, "x", j, "=", i*j
```


### 📍 출처
이것이 취업을 위한 코딩 테스트다 with 파이썬 - 나동빈