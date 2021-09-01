# numpy

## numpy

: 넘파이\(Numpy\)는 수치 데이터를 다루는 파이썬 패키지로써, 주로 배열이나 행렬 계산에 사용된다. Numpy의 핵심이라고 불리는 다차원 행렬 자료구조의 ndarray를 통해 벡터 및 행렬을 사용하는 선형 대수 계산에서 주로 사용. 넘파일 배열은 N차원 배열을 작성할 수 있습니다. 1차원 배열, 2차원 배열, 3차원 배열 처럼 원하는 차수의 배열을 만들수 있다. 수학에서는 1차원 배열을 벡터 vector, 2차원 배열을 행렬 matrix이라고 부른다. 또 벡터와 행렬을 일반화한 것을 텐서\(tensor\)라 한다. 일반적으로 2차원 배열을 행렬, 3차원 이상의 배열을 다차원 배열이라 한다.

```text
import numpy as np
```

## Numpy의 주요 모듈

| 모듈 | 기능 |
| :--- | :--- |
| np.array\(\) | 리스트, 튜플, 배열로 부터 adarray를 생성 |
| np.asarray\(\) | 기존의 array로 부터 adarray를 생성 |
| np.arange\(\) | range와 비슷 |
| np.linspace\(start, end, num\) | \[start, end\] 균일한 간격으로 num개 생성 |
| np.logspace\(start, end, num\) | \[start, end\] log scale 간격으로 num개 생성 |

## np.array\(\)

np.array\(\) 는 파이썬의 리스트를 인수로 받아 넘파이 라이브러리가 제공하는 특수한 형태의 배열 \(numpy.ndarray\)을 반환

```python
x = np.array([1.0, 2.0, 3.0])
print(x) #[1, 2, 3]
type(x) <class 'numpy.ndarray'>
```

## 넘파이 N차원 배열

: 넘파이는 1차원 배열\(1줄로 늘어선 배열\)뿐 아니라 다차원 배열도 작성할 수 있다

* shape : 행렬의 형상 \(예. 2 x 2\) 
* ndim : 행렬의 차원 출력 
* dtype : 행렬에 담긴 원소의 자료형

```python
import numpy as np

x = np.array([[1, 2], [3, 4]])
print(x)
# [[1 2]
#  [3 4]]
print(x.shape) # (2, 2)
print(x.ndim) # 2
print(x.dtype) # int32

y = np.array([[3, 0], [0, 6]])
print(x + y) 
# [[ 4  2]
#  [ 3 10]]
print(x * y)
# [[ 3  0]
#  [ 0 24]]
```

## 넘파이 산술 연산

```python
import numpy as np

x = np.array([1.0, 2.0, 3.0])
y = np.array([4.0, 5.0, 6.0])
print(x + y) # [5. 7. 9.]
print(x - y) # [-3. -3. -3.]
print(x * y) # [ 4. 10. 18.]
print(x / y) # [0.25 0.4  0.5 ]
```

Numpy에서 벡터와 행렬의 곱 또는 행렬곱을 위해서는 dot\(\)을 사용

```python
a = np.array([[1,2],[3,4]])
b = np.array([[5,6],[7,8]])
c = np.dot(a, b) print(c)
# [[19 22]
#  [43 50]]
```

## ndnumpy의 초기화 : zeros\(\), ones\(\), full\(\), eye\(\)

* zeros\(\): 해당 배열에 모두 0을 삽입
* ones\(\) : 해당 배열에 모두 1을 삽입
* full\(\) : 배열에 사용자가 지정한 값을 넣는데 사용
* eye\(\) : 대각선으로는 1이고 나머지는 0인 배열을 생성

```python
import numpy as np

a = np.zeros((2, 3))
print(a)
# [[0. 0. 0.]
#  [0. 0. 0.]]

a = np.ones((2, 3))
print(a)
# [[1. 1. 1.]
#  [1. 1. 1.]]

a = np.full((2, 3), 7)
print(a)
# [[7 7 7]
#  [7 7 7]]

a = np.eye(2)
print(a)
# [[1. 0.]
#  [0. 1.]]
```

## np.arange\(\)

```text
numpy.arange(start, stop, step, dtype)
np.arange(n)       # 0부터 n-1까지 범위의 지정.
np.arange(i, j, k) # i부터 j-1까지 k씩 증가하는 배열.
```

```python
a = np.arange(10) #0부터 9까지
print(a) # [0 1 2 3 4 5 6 7 8 9]
a = np.arange(1, 10, 2) #1부터 9까지 +2씩 적용되는 범위
print(a) # [1 3 5 7 9]
```

## reshape\(\)

: arange\(n\) 함수에 배열을 다차원으로 변형하는 reshape\(\)를 통해 배열을 생성

```python
import numpy as np

a = np.array(np.arange(1, 30, 2)).reshape((3,5))
# 여기서 reshape의 범위는 arange와 동일해야 한다 
print(a)
# [[ 1  3  5  7  9]
#  [11 13 15 17 19]
#  [21 23 25 27 29]]
```

## 브로드 캐스트

: 원소별 계산뿐 아니라 넘파일 배열과 수치 하나\(스칼라값\)의 조합으로 된 산술로 연산이 가능하다

```python
import numpy as np
x = np.array([[1, 2], [3, 4]])
y = np.array([10, 20])
print(x + y)
```

## 넘파이 원소 접근

```python
import numpy as np

x = np.array([[1, 2], [3, 4], [5, 6]])
print(x)
print(x[0]) # 0행의 원소, [1 2]
print(x[0][1]) # (0, 1)의 원소, 2

for row in x:
    print(row)
# [1 2]
# [3 4]
# [5 6]

# x를 1차원 배열로 변환(평탄화)
y = x.flatten() 
print(y) # [1 2 3 4 5 6]
# 인덱스가 0, 2, 4인 원소 얻기 
print(y[np.array([0, 2, 4])]) # [1 3 5]
```

