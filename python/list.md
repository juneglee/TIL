# list

: 파이썬에서 리스트의 의미는 여러가지 자료를 저장할 수 있는 자료

* 사용법 \[요소, 요소, 요소 ...\], 이때 요소는 element라고 부른다 

```python
[1, 2, 3, 4]
["안","녕","하","세","요"]
[273,32,108,'문자열',True,False]

list_a = [273, 32, 108, '문자열', True, False]
print(list_a[0]) # 273
print(list_a[1]) # 32
print(list_a[2]) # 108
print(list_a[3]) # 문자열
print(list_a[4]) # True
print(list_a[5]) # False
```

## 리스트 사용 방법

1. 대괄호 안에 음수를 넣어 뒤에서부터 요소를 선택할 수 있습니다.

   ```python
   print(list_a[-1]) # False
   print(list_a[-2]) # True
   ```

2. 리스트 접근 연산자를 다음과 같이 이중으로 사용할 수 있습니다.

   ```python
   print(list_a[3]) # 문자열
   print(list_a[3][0]) # 문
   ```

3. 리스트 안에 리스트를 사용할 수 있습니다

   ```python
   list_b = [[1, 2, 3],[4, 5 ,6],[7 ,8 ,9]]
   print(list_b[1]) # [4, 5 ,6]
   print(list_b[1][1]) # 5
   ```

4. 리스트 index 안에 존재하지 않는 요소를 접근할때 indexError 발생

## 리스트 연선자 : 연결\(+\), 반복\(\*\), len\(\)

* 리스트 연산자 

```python
list_a = [1, 2, 3]
list_b = [4, 5, 6]

print("list_a = ", list_a)
print("list_b = ", list_b)
print()
```

* 기본 연산자 :  연결\(+\) , 반복\(\*\)

```python
print("list_a + list_b =", list_a + list_b)
print("list_a * 3 =", list_a * 3)
print()
```

* 길이 구하기 : len\(\) 

```python
print("len(list_a) = ", len(list_a))
```

## 리스트 요소 추가하기 : append, insert, extend

사용법

* 리스트명.append\(요소\)
* 리스트명.insert\(위치,요소\) = \(삽입할 위치, 삽입할 값\)

```python
list_a = [1, 2, 3]
list_b = [1, 2, 3]
```

* 리스트 뒤에 요소 추가하기 : append \(\)

```python
list_a.append(4)
list_a.append(5)
print(list_a) # [1, 2, 3, 4, 5]
print("------------------")
```

* 한번에 여러 요소를 추가하고 싶을 때는 extend\(\)

```python
list_b.extend([4, 5, 6]) 
print(list_b) # [1, 2, 3, 4, 5]
print("------------------")
```

* 리스트 중간에 요소 추가하기 : insert\(\)

```python
list_a.insert(0, 10)
print(list_a) # [10, 1, 2, 3, 4, 5]
```

* '+' 를 사용한 연결 연산자와 append, insert, extend의 차이 
* 연결 연산자는 원본에 아무런 영향을 주지 않는 '비파괴적'이지만, 
* append, insert, extendsms 는 리스트에 직접적인 영향을 주는 '파괴적'이다

## 리스트 요소 제거하기 : del, pop

* 인덱스로 제거하기 및 값으로 제거하기가 있다 

인덱스로 제거하기 : del, pop

* 사용법
* del 리스트명\[인덱스\]
* 리스트명.pop\(인덱스\)

```python
list_a = [0, 1, 2, 3, 4, 5]
print("# 리스트의 요소 하나 제거하기")
# 제거 방법[1] – del
del list_a[1]
print("del list_a[1]:", list_a) # [0, 2, 3, 4, 5]
# 제거 방법[2] – pop()
list_a.pop(2)
print("pop(2):", list_a) # [0, 2, 4, 5]
```

* 범위를 지정하여 제거할 수 있다 

  ```python
  list_b = [0, 1, 2, 3, 4, 5]
  del list_b[3:5]
  print("del list_b[3:5]:", list_b) # [0, 1, 2, 5]
  list_c = [0, 1, 2, 3, 4, 5]
  del list_c[:3]
  print("del list_c[:3]:", list_c) # [3, 4, 5]
  list_d = [0, 1, 2, 3, 4, 5]
  del list_d[3:]
  print("del list_d[3:]:", list_d) # [0, 1, 2]
  ```

## 값으로 제거하기 : remove

* 사용법 
* 리스트.remove\(값\)

```python
list_e = [1, 2, 1, 2]
list_e.remove(2)
print(list_e) # [1, 1, 2]
```

## 모두 제거하기 : clear

* 사용법
* 리스트.clear\(\)

```python
list_f = [0, 1, 2, 3, 4, 5]
list_f.clear()
print(list_f) #[]
```

## 리스트 정렬 : sort

* 리스트의 요소를 순서대로 정렬한다 \(문자 역시 알파벳 순서로 정렬\)

```python
a = [1, 4, 3, 2]
a.sort()
print(a)
# [1, 2, 3, 4]
b = ['a', 'c', 'b']
b.sort()
print(b)
# ['a', 'b', 'c']
```

## 리스트 뒤집기 : reverse

* reverse 함수는 리스트를 역순으로 뒤집어 준다\(단, 정렬해서 리스트를 뒤집는 것이 아니다\)

```python
a = [1, 4, 3, 2]
a.sort()
print(a)
# [2, 3, 4, 1]
```

## 위치 반환 : index

* 리스트에 x 값이 있으면 x의 위치 값을 돌려준다 

```python
a = [1, 2, 3]
a.index(3) 
2
# index(3)이라는 숫자는 위치에서 a[2]이므로 2를 돌려준다
# 이때 리스트에 존재하지 않는 값을 입력하면, 존재하지 않기 떄문에 값 오류 (ValueError)가 발생
```

## 리스트 내부에 있는지 확인하기 : in/not in 연산자

* 사용법 
* 값 in 리스트 / 값 not in 리스트 

```python
list_a = [273, 32, 108, 57, 52]
print("내부에 있을 때 : in")
print(273 in list_a) # True
print(99 in list_a) # False
print(100 in list_a) # False
print(52 in list_a) # True
print("------------------------------------")
print("내부에 없을 때 : not in")
print(273 not in list_a) # False
print(99 not in list_a) # True
print(100 not in list_a) # True
print(52 not in list_a) # False
```

## list와 tuple의 비교

* 리스트와 튜플의 기술적 차이점은 불변성에 있다. 리스트는 가변적\(mutable, 변경 가능\)이며 튜플은 불변적\(immutable, 변경 불가\)이다. 

```python
list = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
tuple = (1, 2, 3, 4, 5, 6, 7, 8, 9, 10)

list[0] = "Hello"  # various_list = ["Hello", 2, 3, 4, 5, 6, 7, 8, 9, 10]
tuple[0] = "Hello" # 'tuple' object does not support item assignment
```

* 따라서, ist는 딕셔너리의 key값\(해쉬값\)으로 쓸 수 없지만, tuple은 가능하다.

```python
my_dict = {list: "List"}  # TypeError: unhashable type: 'list'
my_dict = {tuple: "Tuple"}  # Ture
```

