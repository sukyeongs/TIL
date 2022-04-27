# 6강) 파이썬 문법 - 사전, 집합 자료형

## 📍 사전 자료형

- `키`와 `값`의 **쌍**을 데이터로 가지는 자료형
    - `키(Key)` : **변경 불가능한 자료형**만 키값이 될 수 있음
- 키값으로 데이터에 접근 ⇒ `인덱스 X`
- 파이썬의 사전 자료형은 `해시 테이블` 이용 ⇒ 데이터의 **조회 및 수정** `O(1)` 시간에 처리 가능

```python
data = dict()   # 사전자료형 선언

data['사과'] = 'Apple'
data['바나나'] = 'Banana'
data['포도'] = 'Grape'

key_list = data.keys()
print(key_list)
=> dict_keys(['사과', '바나나', '포도'])

value_list = data.values()
print(value_list)
=> dict_values(['Apple', 'Banana', 'Grape'])

for key in key_list:
		print(data[key])   # 키 값으로 데이터 조회
=>
Apple
Banana
Grape

key_list = list(data_keys())   # list로 형변환 => ['사과', '바나나', '포도']
```

## 📍 집합 자료형

- **중복 허용 X** , **순서 X** ⇒ 특정 데이터의 `존재 유무 판별`에 용이
- 초기화
    1. **리스트** or **문자열** 이용 ⇒ `set()` 함수 이용
    2. `중괄호({})` 안에 원소를 콤마로 구분하여 삽입
- 데이터의 **조회 및 수정** `O(1)` 시간에 처리 가능

```python
data1 = set([1, 2, 3, 4, 5])

print(data1)
=> {1, 2, 3, 4, 5}

data2 = {1, 2, 3, 4}

print(data2)
=> {1, 2, 3, 4}
```

- **집합 자료형의 연산**
    1. `합집합` ( `|` )
    2. `교집합` ( `&` )
    3. `차집합` ( `-` )

## 📍 집합 자료형 관련 메서드

- add(특정 값) : 원소 추가
- update(리스트나 집합 형태의 값들) : 원소 여러개 추가
- remove() : 원소 삭제

```python
# 예시

data = {1, 2}

data.add(3)
print(data)
=> {1, 2, 3}

data.update([4, 5])
print(data)
=> {1, 2, 3, 4, 5}

data.update({5, 6, 7})
print(data)
=> {1, 2, 3, 4, 5, 6, 7}   # 집합 자료형: 중복 허용 X

data.remove(2)
print(data)
=> {1, 3, 4, 5, 6, 7}
```

## 📍 사전/집합 자료형의 특징

- **순서 X** ⇒ `인덱싱 X`
- **키(key)** or **원소**를 이용하여 `O(1)`의 시간복잡도로 조회
    - **키(key)**는 `변경불가능`한 자료형 → ex. 문자열, 튜플 ...


### 📍 출처
이것이 취업을 위한 코딩 테스트다 with 파이썬 - 나동빈