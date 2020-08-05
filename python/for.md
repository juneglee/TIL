# for

기본 구조
```
for 변수 in 리스트(또는 튜플, 문자열):
    수행할 문장1
    수행할 문장2
    ...
```
### range 함수 (for문과 함께 자주 사용)
```python
a = range(5) # range(5) 는 0부터 5미만의 숫자를 포함하는 range 객체를 만들어 준다  
b = range(0, 5) # 시작과 끝의 숫자를 지정할 수 있다. 이때 끝 숫자는 포함되지 않는다 
c = range(0 , 10 , 2) # 0부터 2씩 증가하면서 범위를 만듬

print(a) # range(0, 5)
print(list(a)) # [0, 1, 2, 3, 4]

print(b) # range(0, 5)
print(list(b)) # [0, 1, 2, 3, 4]

print(c) # range(0, 10, 2)
print(list(c)) # [0, 2, 4, 6, 8]
```

### range 함수의 매개변수로 사용
```python
n = 10
d = range(0 , int(n/2)) # 실수를 정수로 바꾸는 방법
e = range(0 , n // 2) # 정수 나누기 연산자를 많이 사용

print(list(d)) # [0, 1, 2, 3, 4]
print(list(e)) # [0, 1, 2, 3, 4]
```

### for문 사용 (for 키 변수 in 범위:)
```python
for i in range(5):
    print(str(i) + "= 반복 변수")
print()

for i in range(5, 10):
    print(str(i) + "= 반복 변수")
print()

for i in range(0, 10, 3):
    print(str(i) + "= 반복 변수")
print()
```

### for 반복문 : 리스트와 범위 조합하기 
```python
array = [273, 32, 103, 57, 52]
for element in array:
    print(element)
```

### for 반복문 : 반대로 반복하기 (format)
```python
for i in range(4, 0 - 1, -1):
    print("현재 반복 변수: {}".format(i))
print("----------------------------------")
for i in reversed(range(5)):
    print("현재 반복 변수: {}".format(i))
```


### 다양한 for 문의 사용
```python
a = [(1,2),(3, 4),(5, 6)]
for (first, last) in a:
    print(first + last)
3
7
11
```

### for문 과 continue
```python
marks = [90, 25, 67, 45, 80]

number = 0 
for mark in marks: 
    number = number +1 
    if mark < 60:
        continue 
    print("%d번 학생 축하합니다. 합격입니다. " % number)
# 1번 학생 축하합니다. 합격입니다.
# 3번 학생 축하합니다. 합격입니다.
# 5번 학생 축하합니다. 합격입니다.
```

### for문과 range를 이용한 구구단
```python
for i in range(2, 10)
    for j in range(1, 10)
        print(i * j, end=" ")
    print('')
2 4 6 8 10 12 14 16 18 
3 6 9 12 15 18 21 24 27 
4 8 12 16 20 24 28 32 36
5 10 15 20 25 30 35 40 45
6 12 18 24 30 36 42 48 54 
7 14 21 28 35 42 49 56 63 
8 16 24 32 40 48 56 64 72 
9 18 27 36 45 54 63 72 81
```

### 리스트 안에 내포하여 사용하기 
```
[표현식 for 항목 in 반복가능객체 if 조건문]
```
```python
a = [1, 2, 3, 4]
result = [num * 3 for num in a if num % 2 == 0]
# a의 리스트 안에 2로 나누었을 때 0이 되는 요소에 *3을 하여 출력하라 
print(result)
# [6, 12]
```

```
조금 복잡하지만 for문을 2개 이상 사용하는 것도 가능하다 
[표현식 for 항목1 in 반복가능객체1 if 조건문1
        for 항목2 in 반복가능객체2 if 조건문2
        ...
        for 항목n in 반복가능객체n if 조건문n]
```
```python
# 구구단의 모든 결과를 출력 
result = [x*y for x in range(2,10)
              for y in range(1,10)]
print(result)
[2, 4, 6, 8, 10, 12, 14, 16, 18, 3, 6, 9, 12, 15, 18, 21, 24, 27, 4, 8, 12, 16,
20, 24, 28, 32, 36, 5, 10, 15, 20, 25, 30, 35, 40, 45, 6, 12, 18, 24, 30, 36, 42
, 48, 54, 7, 14, 21, 28, 35, 42, 49, 56, 63, 8, 16, 24, 32, 40, 48, 56, 64, 72,
9, 18, 27, 36, 45, 54, 63, 72, 81]
```
