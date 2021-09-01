# function

사용법

```text
def 함수이름(): 
    문장
```

## 기본적인 함수

```python
def print_3_times():
    print("안녕하세요")
    print("안녕하세요")
    print("안녕하세요")
print_3_times()
```

## 키워드 매개변수

```python
# 가변 매개변수가 기본 매개변수보다 앞에 올 때 
def print_n_times( *values, n=2):     
    for i in range(n):             
        for value in values:
            print(value)          
        print()
print_n_times("안녕하세요", "즐거운", "파이썬 프로그래밍", 3)

# 기본 매개변수가 가변 매개변수보다 앞에 올 때 (error가 발생)
def print_n_times(n=2, *values):     
    for i in range(n):             
        for value in values:
            print(value)          
        print()
print_n_times("안녕하세요", "즐거운", "파이썬 프로그래밍")
```

## 키워드 매개 변수

```python
def print_n_times( *values, n=2):     
    for i in range(n):             
        for value in values:
            print(value)          
        print()
print_n_times("안녕하세요", "즐거운", "파이썬 프로그래밍", 3)
# 안녕하세요     
# 즐거운
# 파이썬 프로그래밍
# 3 
# => 다음과 같이 3이 출력되며, 문자열은 두번을 반복한다
```

```python
def print_n_times(*values, n=2):
    for i in range(n):
        for value in values:
            print(value)
        print()
print_n_times("안녕하세요", "즐거운", "파이썬 프로그래밍", n=3)
# 안녕하세요     
# 즐거운
# 파이썬 프로그래밍
# => 문자열이 세번 반복한다
```

## 기본 매개변수 중에서 필요한 값만 입력하기

```python
# 여러 함수 호출 형태 
def test(a, b=10, c=100):
    print(a + b + c)
# 1) 기본 형태
test(10, 20, 30)
# 2) 키워드 매개변수로 모든 매개변수를 지정한 형태
test(a=10, b=100, c=200)
# 3) 키워드 매개변수로 모든 매개변수를 마구잡이로 지정한 형태
test(c=10, a=100, b=200)
# 4) 키워드 매개변수로 일부 매개변수만 지정한 형태
test(10, c=200)
```

## 리턴

```python
# 자료 없이 리턴하기 
def return_test():
    print("A 위치입니다.")
    return # 리턴합니다.
    print("B 위치입니다.")
return_test() # A 위치입니다.

# 자료와 함께 리턴하기
def return_test():
    return 100
value = return_test()
print(value) # 100

# 아무것도 리턴하지 않기 
def return_test():
    return
value = return_test()
print(value) # None
```

## 기본적인 함수의 활용

사용법

```text
def 함수(매개변수):
    변수 = 초깃값
    여러 가지 처리 
    여러 가지 처리 
    여러 가지 처리 
    return 변수
```

## 범위 내부의 정수를 모두 더하는 함수

```python
def sum_all(start, end):
    output = 0
    for i in range(start, end + 1):
        output += i
    return output
print("0 to 100:", sum_all(0, 100))       # 0 to 100: 5050
print("0 to 1000:", sum_all(0, 1000))     # 0 to 1000: 500500
print("50 to 100:", sum_all(50, 100))     # 50 to 100: 3825
print("500 to 1000:", sum_all(500, 1000)) # 500 to 1000: 375750
print("---------------------------------------")
```

## 기본 매개변수와 키워드 매개변수를 활용해 범위의 정수를 더하는 정수

```python
def sum_all(start=0, end=100, step=1):
    output = 0
    for i in range(start, end + 1, step):
        output += i
    return output
print("A.", sum_all(0, 100, 10))      # A. 550
print("B.", sum_all(end=100))         # B. 5050
print("C.", sum_all(end=100, step=2)) # C. 2550
```

## 재귀함수

```python
# 반복문으로 팩토리얼 구하기 
def factorial(n):
    output = 1
    for i in range(1, n + 1):
        output *= i
    return output
print("1!:", factorial(1))
print("2!:", factorial(2))
print("3!:", factorial(3))
print("4!:", factorial(4))
print("5!:", factorial(5))

# 재귀 함수로 팩토리얼 구하기 
def factorial(n):
    # n이 0이라면 1을 리턴
    if n == 0:
        return 1
    # n이 0이 아니라면 n * (n-1)!을 리턴
    else:
        return n * factorial(n - 1)
print("1!:", factorial(1))
print("2!:", factorial(2))
print("3!:", factorial(3))
print("4!:", factorial(4))
print("5!:", factorial(5))
```

## 피보나치 수열

* n번째 수열 = \(n-1\) 번째 수열 + \(n-2\) 번째 수열 

```python
# 재귀 함수로 구현한 피보나치 수열(1)
def fibonacci(n):
    if n == 1:
        return 1
    if n == 2:
        return 1
    else:
        return fibonacci(n - 1) + fibonacci(n - 2)
print("fibonacci(1):", fibonacci(1))
print("fibonacci(2):", fibonacci(2))
print("fibonacci(3):", fibonacci(3))
print("fibonacci(4):", fibonacci(4))
print("fibonacci(5):", fibonacci(5))

# 재귀 함수로 구현한 피보나치 수열(2)
counter = 0
def fibonacci(n):
    print("fibonacci({})를 구합니다.".format(n))
    global counter # global 변수이름 : 함수의 외부의 변수를 참조하기 위해서 사용
    counter += 1
    if n == 1:
        return 1
    if n == 2:
        return 1
    else:
        return fibonacci(n - 1) + fibonacci(n - 2)
fibonacci(10)
print("---")
print("fibonacci(10) 계산에 활용된 덧셈 횟수는 {}번입니다.".format(counter))
# 트리 형태에서 각각의 지점을 노드, 노드 중에 가장 마지막 단계의 노드를 리프라고 부른다
```

## 메모화

* 딕셔너리를 사용해서 한번 계산한 값을 지정하는 것을 메모라고 하며, 
* 메모화를 사용하면 실행 후 곧바로 결과를 출력할 정도로 속도가 빨라진다.

  ```python
  dictionary = {
    1: 1,
    2: 2
  }
  def fibonacci(n):
    if n in dictionary:
        # 메모 되어 있으면 메모된 값 리턴
        return dictionary[n]
    else:
        # 메모 되어 있지 않으면 값을 구함
        output = fibonacci(n - 1) + fibonacci(n - 2)
        dictionary[n] = output
        return output
  print("fibonacci(10):", fibonacci(10))
  print("fibonacci(20):", fibonacci(20))
  print("fibonacci(30):", fibonacci(30))
  print("fibonacci(40):", fibonacci(40))
  print("fibonacci(50):", fibonacci(50))
  ```

## 코드 유지 보수

```python
# p 태그로 감싸는 함수 
def p(content):
    # 기존 코드 주석 처리 
    # return "<p>{}</p>".format(content)
    return "<p class='content-line'>{}</p>".format(content)

print(p("안녕하세요"))
print(p("간단한 HTML 태그를 만드는 예입니다."))
```

## 함수 고급

튜플 : 함수와 함께 많이 사용되는 리스트와 비슷한 자료형으로, 리스트와 다른점은 한번 결정되면 요소를 바꿀 수 없다는 것 람다 : 매개 변수로 함수를 전달하기 위해 함수 구문을 작성하는 것이 번거롭고, 코드 공간 낭비라는 생각이 들때 함수를 간단하고 쉽게 선언하는 방법

## 튜플

```python
# 리스트와 튜플의 특이한 사용
[a, b] = [10, 20]
(c, d) = (10, 20)
print("a:", a) # a: 10
print("b:", b) # b: 20
print("c:", c) # c: 10
print("d:", d) # d: 20

# 괄호가 없는 튜플 
tuple_test = 10, 20, 30, 40
print("# 괄호가 없는 튜플의 값과 자료형 출력")
print("tuple_test:", tuple_test) # tuple_test: (10, 20, 30, 40)
print("type(tuple_test):", type(tuple_test)) # type(tuple_test): <class 'tuple'>
print("-----------------------------")
a, b, c = 10, 20, 30
print("# 괄호가 없는 튜플을 활용한 할당")
print("a:", a) # a: 10
print("b:", b) # b: 20
print("c:", c) # c: 30

# 변수의 값을 교환하는 튜플
a, b = 10, 20
print("# 교환 전 값")
print("a:", a)
print("b:", b)
print("-----------------------------")
a, b = b, a
print("# 교환 후 값")
print("a:", a)
print("b:", b)
print("-----------------------------")

# 여러 개 값 리턴하기 
def test():
    return (10, 20)
a, b = test()
print("a:", a)
print("b:", b)

# 함수의 매개 변수로 함수 전달하기 
# 매개변수로 받은 함수를 10번 호출하는 함수
def call_10_times(func):
    for i in range(10):
        func()
def print_hello():
    print("안녕하세요")
call_10_times(print_hello)
```

## filter\(\) 함수와 map\(\) 함수

함수를 매개변수로 전달하는 대표적인 표준함수

```text
map(함수, 리스트)
filter(함수, 리스트)
```

```python
def power(item):
    return item * item
def under_3(item):
    return item < 3

list_input_a = [1, 2, 3, 4, 5]
```

```python
# map() 함수를 사용합니다.
output_a = map(power, list_input_a)
print("# map() 함수의 실행 결과")
print("map(power, list_input_a):", output_a)
print("map(power, list_input_a):", list(output_a))
print("-----------------------------------------")
# filter() 함수를 사용합니다.
output_b = filter(under_3, list_input_a)
print("# filter() 함수의 실행 결과")
print("filter(under_3, list_input_a):", output_b)
print("filter(under_3, list_input_a):", list(output_b))
print("+========================================")
```

## 람다

lambda 매개변수 : 리턴값

```python
# 람다 
power = lambda x: x * x
under_3 = lambda x: x < 3
list_input_a = [1, 2, 3, 4, 5]

output_a = map(power, list_input_a)
print("# map() 함수의 실행 결과")
print("map(power, list_input_a):", output_a) 
# map(power, list_input_a): <map object at 0x000001DC96167208>
print("map(power, list_input_a):", list(output_a))
# map(power, list_input_a): [1, 4, 9, 16, 25]
print("-----------------------------------------")
output_b = filter(under_3, list_input_a)
print("# filter() 함수의 실행 결과")
print("filter(under_3, list_input_a):", output_b)
# filter(under_3, list_input_a): <filter object at 0x000001DC961660C8>
print("filter(under_3, list_input_a):", list(output_b))
# filter(under_3, list_input_a): [1, 2]
```

```python
# 인라인 람다
list_input_a = [1, 2, 3, 4, 5]
output_a = map(lambda x: x * x, list_input_a)
print("# map() 함수의 실행 결과")
print("map(power, list_input_a):", output_a)
print("map(power, list_input_a):", list(output_a))
print("-----------------------------------------")
output_b = filter(lambda x: x < 3, list_input_a)
print("# filter() 함수의 실행 결과")
print("filter(under_3, list_input_a):", output_b)
print("filter(under_3, list_input_a):", list(output_b))
```

