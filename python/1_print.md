# print\(\)

## 하나만 출력하기

```python
print(52)
```

## 여러개 출력하기

```python
print(52, 273, "Hello World")
print("안녕하세요", "방갑습니다")
```

## 줄바꿈\(빈공간\)

```python
print()
```

## 한줄에 여러문장 사용 - 세미콜론 사용

```python
print(52); print(273)
```

## sep로 값 사이에 문자 넣기

* 값 사이에 공백이 아닌 다른 문자를 넣을 때 사용 
* print\(값1, 값2, sep='문자 또는 문자열 '\)

  ```python
  print(1, 2, 3, sep=",") # 1,2,3
  print(1920, 1080, sep="x") # 1920x1080
  ```

## end 사용

* 한줄에 여러개의 값을 출력할 수 있다 

  ```python
  print(1, end=' ')
  print(2, end=' ')
  print(3)
  # 1 2 3
  ```

