# String function

## String function

### 문자 개수 세기 : count\(\)

```python
a = "hobby"
print(a.count('b')) # 2
```

### 문자열 찾기\_1 : find\(\)와 rfind\(\)

| 함수 | 설명 |
| :--- | :--- |
| find\(\) | 왼쪽에서 찾아서 처음 등장하는 위치를 찾습니다. |
| rfind\(\) | 오른쪽부터 찾아서 처음 등장하는 위치를 찾습니다. |

```python
c = "안녕하세요".find("안녕") 
print(c) # 0 
# 문자열은 0번째부터 시작하기 때문에 안녕은 0번쨰 위치로 찾은 것이다
```

```python
d = "안녕안녕하세요".rfind("안녕")
print(d) # 2 
# 오른쪽에서부터 찾았기 때문에 0 1 2인 2번째 인것이다
```

### 문자열 찾기\_2 : index\(\)

```python
a = "Life is too short"
print(a.index('t')) # 8
# 만약 찾는 문자나 문자열이 존재하지 않는다면 오류를 발생
```

### 문자열 삽입 : join\(\)

```python
>>> ",".join('abcd')
'a,b,c,d'

>>> ",".join(['a', 'b', 'c', 'd'])
'a,b,c,d'
```

### 대소문자 바꾸기 : upper\(\)와 lower\(\)

```python
a = "Hello Python Programing"
print(a.upper()) # HELLO PYTHON PROGRAMING
print(a.lower()) # hello python programing
```

### 문자열 공백 제거 : Strip\(\)

: strip\(\)을 사용하면 양쪽 공백을 지우는 것이다

```python
b = """
    안녕하세요 
공백 제거 합니다
"""
print(b.strip())
```

* 왼쪽 공백 지우기 : lstrip\(\)

  ```python
  >>> a = " hi "
  >>> a.lstrip()
  'hi '
  ```

* 오른쪽 공백 지우기 : rstrip\(\)

  ```python
  >>> a= " hi "
  >>> a.rstrip()
  ' hi'
  ```

### 문자열 바꾸기 : replace\(\)

: replace\(바뀌게 될 문자열, 바꿀 문자열\)

```python
>>> a = "Life is too short"
>>> a.replace("Life", "Your leg")
'Your leg is too short'
```

### 문자열의 구성 파악하기: isOO\(\)

| 함수 | 설명 |
| :--- | :--- |
| isalnum\(\) | 문자열이 알파벳 또는 숫자로만 구성되어 있는지 확인 |
| isalpha\(\) | 문자열이 알파벳으로로 구성되어 있는지 확인 |
| isidentifier\(\) | 문자열이 식별자로 구성되어 있는지 확인 |
| isdecimal\(\) | 문자열이 정수로 구성되어 있는지 확인 |
| isdigit\(\) | 문자열이 숫자로 구성되어 있는지 확인 |
| isspace\(\) | 문자열이 공백으로 구성되어 있는지 확인 |
| islower\(\) | 문자열이 소문자로 구성되어 있는지 확인 |
| isuppser\(\) | 문자열이 대문자로 구성되어 있는지 확인 |

```python
print("trainA10".isalnum()) # True
print("10".isdigit()) # True
```

## 문자열과 in 연산자

: 문자열 내부에 어떤 문자열이 있는지 확인하려면 in 연산자를 사용한다

```python
print("안녕" in "안녕하세요") # True
print("메롱" in "안녕하세요") # False
```

## 문자열 자르기 : split\(\)

```python
e = "10 20 30 40 50".split()
print(e) # ['10', '20', '30', '40', '50'] # 실행결과로 리스트(list)가 나옴
```

* 입력 값을 정수로 변환 

  ```python
  f, g = input('숫자를 두 개 입력하세요 : ').split()
  f = int(f)
  g = int(g)
  print(f + g) # 10 20 입력 30 출력
  ```

## map을 사용하여 정수로 변환

```python
h, i = map(int, input('숫자를 두 개 입력하세요 : ').split())
print(h + i)
```

