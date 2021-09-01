# input\(variable\)

## 변수 variable

* 영문 문자와 숫자를 사용할수 있음
* 대소문자를 구분
* 문자부터 시작하며, 숫자부터 시작하면 안된다
* \_\(밑줄 문자\)로 시작할 수 있다
* 특수문자 사용할 수 없다 
* 파이썬 키워드\(if, for\)는 변수로 사용할 수 없다
* 변수 = 값

  ```python
  pi = 3.14159265
  print(pi)
  ```

## 원의 둘레와 넓이 구하기

```python
pi = 3.14159265
r = 10

print("원주율 = ", pi)
print("반지름 = ", r)
print("원의 둘레 = ", 2 * pi * r)
print("원의 넓이 = ", pi * r ** 2)
```

## 파이썬 자료형 특징

* 파이썬은 C, java 처럼 변수의 자료형에 대해 미리 선언하지 않고 

  여러 종류의 자료형을 넣을 수 있는 유연성을 가지고 있다

  ```python
  a = "문자열"
  a = True
  a = 10
  print(a) # 10
  ```

## 복합 대입 연산자

| 코드 | 설명 |
| :--- | :--- |
| += | 숫자 덧셈 후 대입 |
| -= | 숫자 뺄셈 후 대입 |
| \*= | 숫자 곱셈 후 대입 |
| /= | 숫자 나눗셈 후 대입 |
| %= | 숫자의 나머지를 구한 후 대입 |
| \*\*= | 숫자 제곱 후 대입 |

```python
num = 100
num += 10
num -= 20
num *= 3
print("num 결과값 : ", num) # 270
```

## 문자열 복합대입 연산자\(마찬가지로 += 와 \*= 사용가능 \)

```python
String = "안녕하세요" 
String += "!"
String += "!"
print("String 결과 : ", String) # 안녕하세요!!
```

## 사용자 입력 : input\(\)

```python
String = input("인사말을 입력하세요> ")
print(String)
```

## input\(\) 함수의 입력 자료형

```python
number = input("숫자를 입력하세요> ")
print(number) # 12345
print(type(number)) # 결과값 :  Str
```

* 무엇을 입력하여도 무조건 문자열 자료형이다.

## 문자열 숫자로 바꾸기

```python
String_a = input("입력A > ")
int_a = int(String_a)
int_fa = float(String_a)

String_b = input("입력B > ")
int_b = int(String_b)
int_fb = float(String_b)
```

* 예제 A : 123 B : 45

  ```python
  print("문자열 자료 : ", String_a + String_b) # 12345
  print("숫자 자료 :" , int_a + int_b) # 168
  print("float 자료 :" , int_fa + int_fb) # 168.0
  ```

## ValueError 예외처리

1. 숫자가 아닌 것을 숫자로 변환하려고 할때 

   ```python
   int("안녕하세요")
   ```

2. 소수점이 있는 숫자 형식을 문자열 int\(\) 함수로 변환하려고 할때 

   ```python
   int("52.273")
   ```

## 숫자로 문자열 바꾸기 : str

```python
output_a = str(52)
output_b = str(52.273)
print(type(output_a), output_a) # <class 'str'> 52
print(type(output_b), output_b) # <class 'str'> 52.273
```

