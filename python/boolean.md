# Boolean

## Boolean

### 불 만들기 : 비교 연산자

```python
print(10 == 100) # False
print(10 != 100) # True
print(10 < 100) # True
print(10 > 100) # False
print(10 <= 100) # True
print(10 >= 100) # False
```

```python
print("가방" == "하마") # True
print("가방" != "하마") # True
print("가방" < "하마") # True
# 사전 순서로 가방이 하마보다 앞에 있으므로 작은 값을 갖는다.
print("가방" > "하마") # False
```

## 불 연산하기 : 논리 연산자 \(and 와 or \)

* and : a와 b True 일 때만 True 이다

  | a | b | x |
  | :--- | :--- | :--- |
  | 0 | 0 | 0 |
  | 0 | 1 | 0 |
  | 1 | 0 | 0 |
  | 1 | 1 | 1 |

  ```python
  print(True and True) #True 
  print(True and False) #False
  print(False and True) #False
  print(False and False) #False
  ```

* or : a와 b가 하나라도 True라면 True이다

  | a | b | x |
  | :--- | :--- | :--- |
  | 0 | 0 | 0 |
  | 0 | 1 | 1 |
  | 1 | 0 | 1 |
  | 1 | 1 | 1 |

  ```python
  print(True or True) #True 
  print(True or False) #True
  print(False or True) #True
  print(False or False) #False
  ```

### x in s, x not in s

| in | not in |
| :--- | :--- |
| x in 리스트 | x not in 리스트 |
| x in 튜플 | x not in 튜플 |
| x in 문자열 | x not in 문자열 |

* in의 뜻인 "~안에"라는 것 처럼 안에 있는 문장인지 확인할 수 있다

```python
>>> 1 in [1, 2, 3]
True
>>> 1 not in [1, 2, 3]
False

>>> 'a' in ('a', 'b', 'c')
True
>>> 'j' not in 'python'
True
```

