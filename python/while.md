# while

기본구조

```text
while <조건문>:
    <수행할 문장1>
    <수행할 문장2>
    <수행할 문장3>
    ...
```

## while 반복문 : for 반복문처럼 사용하기

```python
i = 0
while i < 10:
    print("{}번째 반복입니다.".format(i))
    i += 1
```

## while 반복문 : 상태를 기반으로 반복하기

```python
list_test = [1, 2, 1, 2]
value = 2
while value in list_test: # list_test 내부에 value가 있다면 반복
    list_test.remove(value)
print(list_test) # [1, 1]
```

## while 반복문 : 시간을 기반으로 반복하기

```python
import time
number = 0
# 5초 동안 반복합니다.
target_tick = time.time() + 5 
while time.time() < target_tick:
    number += 1
print("5초 동안 {}번 반복했습니다.".format(number)) # 5초 동안 25604106번 반복했습니다.
```

## while 반복문 : break 키워드 / continue 키워드

* break 키워드 : while문을 강제로 빠져나가고 싶을 때 사용

  ```python
  i = 0
  while True:
   print("{}번째 반복문입니다.".format(i))
   i = i + 1
   input_text = input("> 종료하시겠습니까?(y): ")
   if input_text in ["y", "Y"]:
       print("반복을 종료합니다.")
       break
  ```

* continue 키워드 : 조건이 맞지 않으면 맨 처음\(조건문\)으로 돌아가게 만드는 것

  ```python
  numbers = [5, 15, 6, 20, 7, 25]
  for number in numbers:
    if number < 10: # number가 10보다 작으면 다음 반복으로 넘어갑니다.
        continue
    print(number) # 15 20 25
  ```

## 무한반복 while True:

* while문의 조건문이 True이므로 항상 참이 된다. 따라서 while문 안에 있는 문장들은 무한하게 수행될 것이다.

  ```python
  while True:
    print(".", end="") 
  # "."을 출력합니다.
  # 기본적으로 end가 "\n"이라 줄바꿈이 일어나는데, 
  # 빈 문자열 ""로 바꿔서 줄바꿈이 일어나지 않게 합니다.
  ```

* 이때는 Ctrl+C를 눌러서 while문을 빠져나갈 수 있다.

