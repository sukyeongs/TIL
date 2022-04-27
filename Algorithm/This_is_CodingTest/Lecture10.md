# 10강) 함수와 람다 표현식

## 📍 함수

- **특정한 작업**을 **하나**로 묶어놓은 것
- 장점 : 불필요한 소스코드의 반복을 줄일 수 있음
- 종류
    1. `내장 함수` : 파이썬이 **기본적으로 제공**하는 함수
    2. `사용자 정의 함수` : **개발자가 직접 정의**하여 사용하는 함수

## 📍 함수 정의하기

```python
def 함수명(**매개변수**):
		```
		실행 코드
		```
		return **반환값**
```

1. `매개 변수` : 함수 내부에서 사용할 변수
2. `반환값` : 처리된 결과 ⇒ 여러개일 수 있음
    
    ```python
    def operator(a, b):
    		add_var = a + b
    		subtract_var = a - b
    		multiply_var = a * b
    		divide_var = a / b
    		return add_var, subtract_var, multiply_var, divide_var   # 패킹(packing)
    
    a, b, c, d = operator(7, 3)   # 언패킹(unpacking)
    ```
    

**예시**

```python
def add(a, b):
		return a + b

print(add(3, 7))   # 3, 7 : 인자
=> 10

print(add(b = 7, a = 3))   # 매개변수 직접 지정 가능
```

## 📍 함수를 정의할 때 사용되는 키워드

- `global` : **해당 함수**에서는 **지역 변수 생성X**, **함수 바깥의 변수**를 바로 참조

```python
a = 0

def func():
		global a
		a += 1

for i in range(10):
		func()

print(a)
=> 10
```

```python
array = [1, 2, 3, 4, 5]

def func():
		array = [3, 4, 5]
		array.append(6)
		print(array)

func()
print(array)
=>
[3, 4, 5, 6]
[1, 2, 3, 4, 5]
```

- `리스트`는 `global` 키워드를 **사용하지 않아도** **함수 내에서** **전역변수 바로 참조 가능**

```python
list = [1, 2, 3, 4, 5]

def func():
    list.append(6)
    print(list)

func()
=> [1, 2, 3, 4, 5, 6]
```

## 📍 람다 표현식

- 함수를 간단하게 작성 가능 ⇒ `이름 없는 함수`
- 함수 자체를 입력받는 함수에서 쓰기에 용이

```python
# 기존 덧셈 함수 정의
def add(a, b):
		return a + b

print(add(3, 7))

# 람다 표현식 사용
print((lambda a, b: a + b)(3, 7))
```

- 내장함수에서 자주 쓰이는 람다 함수

```python
# 기존 함수 정의
array = [('홍길동', 50), ('이순신', 32), ('아무개', 74)]   # 튜플 리스트

def my_key(x):
		return x[1]

print(sorted(array, key=my_key))   # key=함수: 정렬할 때 기준으로 사용할 함수

# 람다 표현식 사용
print(sorted(array, key=lambda x:x[1]))
```

- 여러개의 리스트에 적용

```python
list1 = [1, 2, 3, 4, 5]
list2 = [6, 7, 8, 9, 10]

result = map(lambda a, b: a + b, list1, list2)

print(list(result))
=> [7, 9, 11, 13, 15]
```

### 📍 출처
이것이 취업을 위한 코딩 테스트다 with 파이썬 - 나동빈