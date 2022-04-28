# 13강) 그리디 유형 문제 풀이

## 1. 1이 될 때 까지

**📌 문제 설명**

어떤 수 N이 1이 될 때까지 다음의 두 과정 중 하나를 반복적으로 선택하여 수행

단, 두번째 연산은 N이 K로 나누어 떨어질 때만 선택 가능

1) N에서 1을 뺀다

2) N을 K로 나눈다

최소 횟수를 구하는 프로그램 작성

**📌 예시**

N=17, K=4 

⇒ 1) → 2) → 2) : 총 `3`번

**📌 설명**

- 최대한 나누기를 많이 진행하면 됨

**📌 정당성 분석**

N이 아무리 커도, K가 2 이상이라면 나눌 때 기하급수적으로 빠르게 줄일 수 있음

**📌 코드**

```python
n, k = map(int, input().split())
result = 0

while True:
		target = (n//k) * k   # N이 K로 나누어 떨어질 때까지 빼기
		result += n - target
		n = target
		if n < k:
				break
		result += 1
		n //= k

result += (n - 1)
```

## 2. 곱하기 혹은 더하기

**📌 문제 설명**

각 자리가 숫자(0~9)로만 이루어진 문자열 S

왼쪽부터 오른쪽으로 ‘+’ or ‘x’를 넣어 만들어질 수 있는 가장 큰 숫자 구하는 프로그램 작성

**📌 설명**

- 두 수 중에서 하나라도 ‘0’ or ‘1’이면 더하기, 이외엔 곱하기

**📌 코드**

```python
data = input()
result = int(data[0])

for i in range(1, len(data)):
    num = data[i]
    if int(num) <= 1 or result <= 1:
        result += int(num)
    else:
        result *= int(num)

print(result)
```

## 3. 모험가 길드

**📌 문제 설명**

모험가 N명, 공포도가 높은 모험가 = 쉽게 공포를 느낌

공포도가 X인 모험가는 반드시 X명 이상으로 구성된 모험가 그룹에 참여해야함

N명의 정보가 주어질 때, 그룹 수의 최댓값

**📌 설명**

- 오름차순으로 정렬 ⇒ 최소한의 모험가수만 포함하여 그룹 결성

**📌 코드**

```python
n = int(input())
data = list(map(int, input().split()))
data.sort()

result = 0   # 그룹 수
count = 0   # 그룹에 포함된 모험가 수

for i in data:
    count += 1
    if i <= count:
        result += 1
        count = 0
```



### 📍 출처
이것이 취업을 위한 코딩 테스트다 with 파이썬 - 나동빈