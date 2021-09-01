# 구문 오류와 예외

오류의 종류

* 구문오류 : 실행 전 발생하는 오류 
* 예외 or 런타임 오류 : 프로그램 실행 중에 발생하는 오류 

## 기본 예외 처리

조건문을 사용하는 방법 try 구문을 사용하는 방법

* 조건문으로 예외 처리하기 

  ```python
  user_input_a = input("정수 입력> ")
  if user_input_a.isdigit():
    number_input_a = int(user_input_a)
    print("원의 반지름:", number_input_a)
    print("원의 둘레:", 2 * 3.14 * number_input_a)
    print("원의 넓이:", 3.14 * number_input_a * number_input_a)
  else:
    print("정수를 입력하지 않았습니다.")
  ```

* try except 구문으로 예외를 처리

  ```python
  try:
    number_input_a = int(input("정수 입력> "))
    print("원의 반지름:", number_input_a)
    print("원의 둘레:", 2 * 3.14 * number_input_a)
    print("원의 넓이:", 3.14 * number_input_a * number_input_a)
  except:
    print("무언가 잘못되었습니다.")
  ```

## try except 구문과 pass 키워드 조합하기

```python
list_input_a = ["52", "273", "32", "스파이", "103"]
list_number = []
for item in list_input_a:
    try:
        float(item) # 예외가 발생하면 알아서 다음으로 진행은 안 된다
        list_number.append(item) # 예외 없이 통과했으면 리스트에 담는다
    except:
        pass
print("{} 내부에 있는 숫자는".format(list_input_a))
print("{}입니다.".format(list_number))
```

## try except else 구문으로 예외를 처리

```python
try:
    number_input_a = int(input("정수 입력> "))
except:
    print("정수를 입력하지 않았습니다.")
else:
    # 출력합니다.
    print("원의 반지름:", number_input_a)
    print("원의 둘레:", 2 * 3.14 * number_input_a)
    print("원의 넓이:", 3.14 * number_input_a * number_input_a)
```

## try except else finally 구문으로 예외를 처리

```python
try:
    number_input_a = int(input("정수 입력> "))
    print("원의 반지름:", number_input_a)
    print("원의 둘레:", 2 * 3.14 * number_input_a)
    print("원의 넓이:", 3.14 * number_input_a * number_input_a)
except:
    print("정수를 입력하지 않았습니다.")
else:
    print("예외가 발생하지 않았습니다.")
finally:
    print("일단 프로그램이 어떻게든 끝났습니다.")
```

## 정리

* 예외 처리 조합

  ```text
  try + except 
  try + except + else 
  try + except + finally 
  try + except + else + finally 
  try + finally
  ```

  | 코드 | 설명 |
  | :--- | :--- |
  | try | 예외가 발생할 가능성이 있는 코드 |
  | except | 예외가 발생했을 때 실행할 코드 |
  | else | 예외가 발생하지 않았을때 실행할 코드 |
  | finally | 무조건 실행할 코드 |

## 예외 적용 : 파일이 제대로 닫혔는지 확인

```python
try:
    file = open("info.txt", "w")
    file.close()
except Exception as e:
    print(e)
print("# 파일이 제대로 닫혔는지 확인하기")
print("file.closed:", file.closed)
```

## 예외 적용 : 파일 처리 중간에 예외 발생

```python
try:
    file = open("info.txt", "w")
    예외.발생()
    file.close()
except Exception as e:
    print(e)
print("# 파일이 제대로 닫혔는지 확인하기")
print("file.closed:", file.closed)
```

## 예외 적용 : finally 구문 사용해 파일 닫기

```python
try:
    file = open("info.txt", "w")
    예외.발생()
except Exception as e:
    print(e)
finally:
    file.close()
print("# 파일이 제대로 닫혔는지 확인하기")
print("file.closed:", file.closed)
```

## 예외 적용 : try exceop 구문 끝난 후 파일 닫기

```python
try:
    file = open("info.txt", "w")
    예외.발생해라()
except Exception as e:
    print(e)
file.close()
print("# 파일이 제대로 닫혔는지 확인하기")
print("file.closed:", file.closed)
```

## 예외 적용 : try 구문 내부에서 return 키워드를 사용하는 경우

```python
def test():
    print("test() 함수의 첫 줄입니다.") #
    try:
        print("try 구문이 실행되었습니다.") #
        return
        print("try 구문의 return 키워드 뒤입니다.")
    except:
        print("except 구문이 실행되었습니다.")
    else:
        print("else 구문이 실행되었습니다.")
    finally:
        print("finally 구문이 실행되었습니다.") #
    print("test() 함수의 마지막 줄입니다.")
test()
```

## 예외 적용 : fianlly 키워드 활용

```python
def write_text_file(filename, text):
    try:
        file = open(filename, "w") #
        return
        file.write(text)
    except Exception as e:
        print(e)
    finally:
        file.close()
write_text_file("test.txt", "안녕하세요!")
```

## 예외 적용 : 반복문과 함꼐 사용하는 경우

```python
print("프로그램이 시작되었습니다.") # 
while True:
    try:
        print("try 구문이 실행되었습니다.")
        break
        print("try 구문의 break 키워드 뒤입니다.")
    except:
        print("except 구문이 실행되었습니다.")
    finally:
        print("finally 구문이 실행되었습니다.") #
    print("while 반복문의 마지막 줄입니다.") #
print("프로그램이 종료되었습니다.") #
```

## 예외 처리 고급

```text
try: 
   예외가 발생할 가능성이 있는 구문
except 예외의 종류 as 예외 객체를 활용할 변수 이름: 
   예외가 발생했을 때 실행할 구문
```

## 예외 객체

```python
try:
    number_input_a = int(input("정수 입력> "))
    print("원의 반지름:", number_input_a)
    print("원의 둘레:", 2 * 3.14 * number_input_a)
    print("원의 넓이:", 3.14 * number_input_a * number_input_a)
except Exception as exception:
    print("type(exception):", type(exception))
    print("exception:", exception) # Exception은 부모클래스
```

## 여러가지 예외가 발생할 수 있는 코드 : 2가지

에러 1 : 정수로 변환될수 없는 값을 입력 ex\) "yes!!" 에러 2 : 리스트의 길이를 넘는 인덱스를 입력한 경우 ex\) 100

```python
list_number = [52, 273, 32, 72, 100]
try:
    number_input = int(input("정수 입력> "))
    print("{}번째 요소: {}".format(number_input, list_number[number_input]))
except Exception as exception:
    print("type(exception):", type(exception))
    print("exception:", exception)
```

## 여러가지 예외가 발생할 수 있는 코드 : 다중

```text
try: 
   예외가 발생할 가능성이 있는 구문
except 예외의 종류 A: 
   예외A가 발생했을 때 실행할 구문 
except 예외의 종류 B: 
   예외B가 발생했을 때 실행할 구문 
except 예외의 종류 C: 
   예외C가 발생했을 때 실행할 구문
```

```python
list_number = [52, 273, 32, 72, 100]
try:
    number_input = int(input("정수 입력> "))
    print("{}번째 요소: {}".format(number_input, list_number[number_input]))
except ValueError:
    # ValueError가 발생하는 경우
    print("정수를 입력해 주세요!")
except IndexError:
    # IndexError가 발생하는 경우
    print("리스트의 인덱스를 벗어났어요!")
```

## 예외 구분 구문과 예외 객체 : as 키워드를 사용하여 추가

```python
list_number = [52, 273, 32, 72, 100]
try:
    number_input = int(input("정수 입력> "))
    print("{}번째 요소: {}".format(number_input, list_number[number_input]))
except ValueError as exception:
    print("정수를 입력해 주세요!")
    print("exception:", exception)
except IndexError as exception:
    print("리스트의 인덱스를 벗어났어요!")
    print("exception:", exception)
```

## 예외 처리를 했지만 예외를 못잡는 경우

```python
list_number = [52, 273, 32, 72, 100]
try:
    number_input = int(input("정수 입력> "))
    print("{}번째 요소: {}".format(number_input, list_number[number_input]))
    예외.발생해주세요()
except ValueError as exception:
    print("정수를 입력해 주세요!")
    print(type(exception), exception)
except IndexError as exception:
    print("리스트의 인덱스를 벗어났어요!")
    print(type(exception), exception)
```

## 모든 예외 잡기

```python
list_number = [52, 273, 32, 72, 100]
try:
    number_input = int(input("정수 입력> "))
    print("{}번째 요소: {}".format(number_input, list_number[number_input]))
    예외.발생해주세요()
except ValueError as exception:
    # ValueError가 발생하는 경우
    print("정수를 입력해 주세요!")
    print(type(exception), exception)
except IndexError as exception:
    # IndexError가 발생하는 경우
    print("리스트의 인덱스를 벗어났어요!")
    print(type(exception), exception)
except Exception as exception:
    # 이외의 예외가 발생한 경우
    print("미리 파악하지 못한 예외가 발생했습니다.")
    print(type(exception), exception)
```

## 예외 강제 처리 :  raise 구문

프로그램 강제 종료되는 것을 막기 위해 예외 처리를 해야하며, 아직 구현되지 않는 부분이므로 일부러 예외를 발생시켜 프로그램을 죽게 만들어 잊어버리지 않도록 하는 것이 raise 키워드 이다

* 사용법 

  ```text
  number = input("정수 입력> ")
  number = int(number)
  ```

  ```python
  if number > 0:
    print("양수입니다 !")
    raise NotImplementedError
  else:
    print("음수입니다 !")
    raise NotImplementedError
  ```

