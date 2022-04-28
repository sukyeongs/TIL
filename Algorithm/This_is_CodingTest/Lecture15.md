# 15강) 구현 유형 문제 풀이

## 1. 시각

**📌 문제 설명**

정수 `N`을 입력받아 **00시00분00초 ~ N시59분59초**까지의 모든 시각 중에서 `3`이 하나라도 포함되는 경우의 수를 구하는 프로그램 작성

**📌 설명**

- 가능한 모든 시각의 경우를 하나씩 모두 세서 풀 수 있는 문제
- 하루: 60 * 60 * 24 = 86,400초
    
    ⇒ 단순히 시각을 1씩 증가시키면서 3이 있는지 보면 됨
    
    ⇒ `완전 탐색` 유형 (**가능한 경우 모두 탐색**)
    

**📌 코드**

```python
h = int(input())
count = 0

for i in range(h+1):
		for j in range(60)
				for k in range(60):
						if '3' in str(i)+str(j)+str(k): count += 1
```

## 2. 왕실의 나이트

**📌 문제 설명**

`8 x 8` 평면의 정원. 행: `1~8` / 열: `a~h`

**L자 형태**로 이동 가능, 정원 밖 X

⇒ 1) **수평 2칸**, **수직 1칸** / 2) **수평 1칸**, **수직 2칸**

나이트 위치가 주어질 때, 이동할 수 있는 경우의 수를 출력하는 프로그램 작성

**📌 코드**

```python
input_data = input()

row = int(input_data[1])
column = int(ord(input_data[0])) - int(ord('a')) + 1

# 이동 가능 방향
steps = [(-2, -1), (-1, -2), (2, -1), (1, -2), (2, 1), (1, 2), (-2, 1), (-1, 2)]

result = 0

for step in steps:
		next_row = row + step[0]
		next_column = column + step[1]

		if next_row >= 1 and next_row <= 8 and next_column >= 1 and next_column <= 8:
				result += 1
```

- `ord()` : 입력 받은 문자의 유니코드 값을 반환하는 함수

## 3. 문자열 재정렬

**📌 문제 설명**

알파벳 대문자 + 숫자(0~9)로 이루어진 문자열 입력

알파벳 오름차순 + 숫자 더한 값 출력

**📌 설명**

숫자인 경우 합계에 더하고, 알파벳은 별도의 리스트에 저장 → 정렬된 리스트 + 합계 출력

**📌 코드**

```python
input_str = input()
sum = 0   # 숫자합계
alphabet_list = list()   # 알파벳 리스트

for x in input_str:
    if x.isalpha():
        alphabet_list.append(x)
    else:
        sum += int(x)

alphabet_list.sort()
if sum != 0:
    alphabet_list.append(str(sum))

print(''.join(alphabet_list))
```

- `isalpha()` : **알파벳인지 아닌지 판별**하는 함수
- `''.join(alphabet_list)` : **리스트 → 문자열** 출력
    - 공백 없는 문자열로 출력하라는 의미
    - 공백 있게 출력 = `'  '.join(alphabet_list)`


### 📍 출처
이것이 취업을 위한 코딩 테스트다 with 파이썬 - 나동빈