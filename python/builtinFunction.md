### BuiltinFunction

### abs
: 어떤 숫자를 입력 받았을 때, 그 숫자의 절댓값을 돌려주는 함수

```python
abs(3) # 3
abs(-3) # -3
abs(-1.2) # 1.2
```

### all
: 반복 가능한 (iterable) 자료형 x를 입력 인수로 받으며, x의 요소가 모두 참이면 Ture, 거짓이 하나라도 있으면 False
- 반복 가능한 자료형이란 for문으로 그 값을 출력할 수 있는 것을 의미, 리스트, 튜플, 문자열, 딕셔너리, 집합 등
```python
all([1, 2, 3]) # True
all([1, 2, 3, 0]) # False, 요소 0은 거짓이다 
all([]) # True , 입력 인수가 빈 값인 경우는 True
```

### any
: 반복 가능한 (iterable) 자료형 x를 입력 인수로 받으며, x의 요소가 하나라도 참이면 Ture, 모두 거짓일때 False
```python
any([1, 2, 3, 0]) # True
any([0, ""]) # False
all([]) # False, any의 입력 인수가 빈 값인 경우 False를 리턴
```

### chr
:  아스키(ASCII) 코드 값을 입력받아 그 코드에 해당하는 문자를 출력하는 함수
```python
chr(97) # a
chr(98) # b
chr(48) # 0
chr(49) # 1
```

### dir
: 객체가 자체적으로 가지고 있는 변수나 함수, 리스트와 딕셔너리 객체 관련 함수(메서드)를 보여 주는 예
```python
dir([1, 2, 3]) # 리스트
dir({'1':'a'}) # 딕셔너리
```

### enumerate
: 순서가 있는 자료형(리스트, 튜플, 문자열)을 입력으로 받아 인덱스 값을 포함하는 enumerate 객체를 돌려준다
```python
for i, name in enumerate(['body', 'foo', 'bar']):
    print(i, name)
# 0 body
# 1 foo
# 2 bar
```

### eval
: eval(expression )은 실행 가능한 문자열(1+2, 'hi' + 'a' 같은 것)을 입력으로 받아 문자열을 실행한 결괏값을 돌려준다
```python
eval('1+2') # 3
eval("'hi' + 'a'") # 'hia'
eval('divmod(4, 3)') # (1, 1)
```

### filter
: 입력값으로 받아 각각의 요소를 판별해서 결과값을 돌려주는 함수 
사용법 
```
filter (함수 이름, 반복 가능한 자료형)
```
```python
#positive.py 
def positive(l): 
    result = [] 
    for i in l: 
        if i > 0: 
            result.append(i) 
    return result
print(positive([1,-3,2,0,-5,6])) # [1, 2, 6]
#filter1.py
def positive(x):
    return x > 0
print(list(filter(positive, [1, -3, 2, 0, -5, 6]))) # [1, 2, 6]
# lambda
print(list(filter(lambda x: x > 0, [1, -3, 2, 0, -5, 6]))) # [1, 2, 6]
```

### hex
: 정수 값을 입력받아 16진수(hexadecimal)로 변환하여 돌려주는 함수
```python
hex(234) # '0xea'
hex(3) # '0x3'
```
### id
: id(object)는 객체를 입력받아 객체의 고유 주소 값(레퍼런스)을 돌려주는 함수
```python
a = 3
id(3) # 135072304
id(a) # 135072304
b = a
id(b) # 135072304
```

### input
: 사용자 입력을 받는 함수 
```python
b = input("Enter: ")
>>> Enter: hi
print(b) # 'hi'
```

### int
: 문자열 형태의 숫자나 소수점이 있는 숫자 등을 정수 형태로 돌려주는 함수로, 정수를 입력으로 받으면 그대로 돌려준다.
```python
int('3') # 3
int(3.4) # 3
# int(x, radix)는 radix 진수로 표현된 문자열 x를 10진수로 변환
int('11', 2) # 3, 2진수로 표현된 11를 10진수 값으로 변환
int('1A', 16) # 26, 16진수로 표현된 1A를 10진수 값으로 변환
```

### isinstance 
: 입력으로 받은 인스턴스가 그 클래스의 인스턴스인지를 판단하여 참이면 True, 거짓이면 False
isinstance(object, class)
```python
class Person(): pass
a = Person()
isinstance(a, Person) # True;
```

### len
: 입력값 s의 길이(요소의 전체 개수)를 돌려주는 함수
```python
len("python") # 6
len([1,2,3]) # 3
len((1, 'a')) # 2
```

### list
: 반복 가능한 자료형 s를 입력받아 리스트로 만들어 돌려주는 함수
```python
list("python") # ['p', 'y', 't', 'h', 'o', 'n']
list((1,2,3)) # [1, 2, 3]
```

### map
: 입력받은 자료형의 각 요소를 함수 f가 수행한 결과를 묶어서 돌려주는 함수
- map(f, iterable)은 함수(f)와 반복 가능한(iterable) 자료형
```python
# two_times.py
def two_times(numberList):
    result = [ ]
    for number in numberList:
        result.append(number*2)
    return result
result = two_times([1, 2, 3, 4])
print(result)  # [2, 4, 6, 8]
# map
def two_times(x): 
    return x*2
print(list(map(two_times, [1, 2, 3, 4]))) # [2, 4, 6, 8]
# lambda
print(list(map(lambda a: a*2, [1, 2, 3, 4]))) # [2, 4, 6, 8]
```

### max
: max(iterable)는 인수로 반복 가능한 자료형을 입력받아 그 최댓값을 돌려주는 함수
```python
max([1, 2, 3]) # 3
max("python") # 'y'
```

### min
: min(iterable)은 max 함수와 반대로, 인수로 반복 가능한 자료형을 입력받아 그 최솟값을 돌려주는 함수
```python
min([1, 2, 3]) # 1
min("python") # 'h'
```

### oct
: 정수 형태의 숫자를 8진수 문자열로 바꾸어 돌려주는 함수
```python
oct(34) # '0o42'
oct(12345) # '0o30071'
```

### open
: open(filename, [mode])은 "파일 이름"과 "읽기 방법"을 입력받아 파일 객체를 돌려주는 함수
- 읽기 방법(mode)을 생략하면 기본값인 읽기 전용 모드(r)로 파일 객체를 만들어 돌려준다.

| 파일열기모드 | 설명 |
| --- | --- |
| w | write모드 (새로쓰기 모드) |
| r | read 모드 (읽기 모드) |
| a | append 모드 (뒤에 이어서 쓰기 모드) |
| b | 바이너리 모드로 파일 열기 |

```python
# b는 w, r, a와 함께 사용
f = open("binary_file", "rb") # 바이너리 읽기 모드 
```

### ord
:  문자의 아스키 코드 값을 돌려주는 함수 (ord 함수는 chr 함수와 반대)
```python
ord('a') # 97
ord('0') # 48
```

### pow
: pow(x, y)는 x의 y 제곱한 결괏값을 돌려주는 함
```python
pow(2, 4) # 16, 2의 4승
pow(3, 3) # 27, 3의 3승 
```

### range
: 입력받은 숫자에 해당하는 범위 값을 반복 가능한 객체로 만들어 돌려준다

```python
a = range(5) # range(5) 는 0부터 5미만의 숫자를 포함하는 range 객체를 만들어 준다
print(a) # range(0, 5)
print(list(a)) # [0, 1, 2, 3, 4]

b = range(0, 5) # 시작과 끝의 숫자를 지정할 수 있다. 이때 끝 숫자는 포함되지 않는다 
print(b) # range(0, 5)
print(list(b)) # [0, 1, 2, 3, 4]

c = range(0 , 10 , 2) # 0부터 2씩 증가하면서 범위를 만듬
print(c) # range(0, 10, 2)
print(list(c)) # [0, 2, 4, 6, 8]
```

### round
: 숫자를 입력받아 반올림해 주는 함수
```python
round(4.6) # 5
round(4.2) # 4
round(5.678, 2) # 5.68, 소수점 2자리까지만 반올림하여 표시
```

### sorted
: 입력값을 정렬한 후 그 결과를 리스트로 돌려주는 함
- 리스트 자료형의 sort 함수는 리스트 객체 그 자체를 정렬만 할 뿐 정렬된 결과를 돌려주지는 않는다.
```python
sorted([3, 1, 2]) # [1, 2, 3]
sorted((3, 2, 1)) # [1, 2, 3]
sorted(['a', 'c', 'b']) # ['a', 'b', 'c']
sorted("zero") # ['e', 'o', 'r', 'z']
```

### str
: 문자열 형태로 객체를 변환하여 돌려주는 함수
```python
str(3) # '3'
str('hi') # 'hi'
str('hi'.upper()) # 'HI'
```

### sum
: 입력받은 리스트나 튜플의 모든 요소의 합을 돌려주는 함수
```python
sum([1,2,3]) # 6
sum((4,5,6)) # 15
```

### tuple 
: 반복 가능한 자료형을 입력받아 튜플 형태로 바꾸어 돌려주는 함수
```python
tuple("abc") # ('a', 'b', 'c')
tuple([1, 2, 3])  # (1, 2, 3)
tuple((1, 2, 3)) # (1, 2, 3)
```

### type 
:  입력값의 자료형이 무엇인지 알려 주는 함수
```python
type("abc") # <class 'str'>
type([ ]) # <class 'list'>
type(open("test", 'w')) # <class '_io.TextIOWrapper'>
```

### zip
: 동일한 개수로 이루어진 자료형을 묶어 주는 역할을 하는 함수
```python
list(zip([1, 2, 3], [4, 5, 6])) # [(1, 4), (2, 5), (3, 6)]
list(zip([1, 2, 3], [4, 5, 6], [7, 8, 9])) # [(1, 4, 7), (2, 5, 8), (3, 6, 9)]
list(zip("abc", "def")) # [('a', 'd'), ('b', 'e'), ('c', 'f')]
```