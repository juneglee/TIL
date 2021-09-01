# pandas

## pandas

## series

: 시리즈 클래스는 1차원의 배열 구조를 가진다. 배열과 다른 점은 인덱스 레이블\(label\)에 이름을 붙여 처리 할 수 있다는 점이다

### 시리즈 객체 만들기

```python
import pandas as pd
s = pd.Series([1, 2, 3, 4], index=list("abcd"))

print(s)
# a    1
# b    2
# c    3
# d    4

# 시리즈는 내부의 데이터를 values 속성으로 조회 가능하다 
print(s.values) 
# dtype: int64
# [1 2 3 4]
```

### 시리즈의 메타 정보 확인

: index의 속성확인, 배열의 형상, 차원, 크기 정보를 속성으로 관리할 수 있다

```python
import pandas as pd
s = pd.Series([1, 2, 3, 4], index=list("abcd"))

print(s.index) # Index(['a', 'b', 'c', 'd'], dtype='object')
print(s.shape) # (4,)
print(s.ndim) # 1
print(s.size) # 4
```

### 색인 검색

```python
import pandas as pd
s = pd.Series([1, 2, 3, 4], index=list("abcd"))

print(s[0], s['a']) # 1 1
```

### 슬라이스 검색

```python
import pandas as pd
import numpy as np

s = pd.Series([1, 2, 3, 4], index=list("abcd"))

print(s[0:2]) 
# a    1
# b    2
# dtype: int64
print(s['a':'c'])
# a    1
# b    2
# c    3
# dtype: int64
sv = s['a':'c'] # 슬라이스 검색해서 변수에 할당 
print(np.may_share_memory(sv, s)) # True
```

슬라이스로 생성한 객체는 사본객체가 아니며, 원본의 뷰\(view\)를 제공하는 것이다   
 원본과 슬라이스 검색한 사본의 데이터가 공유되는지 may\_share\_memory함수로 확인   
 판다스의 모든 객체는 슬라이스 검색하면 데이터를 공휴하는 하나의 뷰를 제공   


### 레이블을 사용해서 색인 연산으로 원소 추가

```python
import pandas as pd
s = pd.Series([1, 2, 3, 4], index=list("abcd"))

s['e'] = 100 # 없는 레이블을 색인 연산에 넣고 추가가 가능하다 
# s[5] = 300 # 정수 인덱스를 사용해서는 시리즈에 새로운 원소를 추가할 수 없다 
print(s) 

d = s.to_frame()
print(d)
```

시리즈는 판다스 모듈의 가장 기본적인 클래스이다.   
 시리즈를 to\_frame메소드로 데이터프레임으로 변환하면 하나의 열을 가진 데이터 프레임으로 변환한다

## 데이터프레임\(DataFrame\) 구조

: 시리즈는 1차원 배열이므로 행 단위로 처리하지만, 데이터프레임은 2차원 배열이라 열을 기준으로 처리한다.

### 데이터 프레임 생성

```python
import pandas as pd

df = pd.DataFrame([[1, 2, 3, 4], [5, 6, 7 ,8]], index=list('ab'), columns =list('abcd'))
print(df)
#    a  b  c  d
# a  1  2  3  4
# b  5  6  7  8
print(df.values) # [[1 2 3 4]  [5 6 7 8]]
print(type(df.values)) # <class 'numpy.ndarray'>
```

### 행과 열의 인덱스 정보와 배열의 메타 정보 확인

```python
import pandas as pd
df = pd.DataFrame([[1, 2, 3, 4], [5, 6, 7 ,8]], index=list('ab'), columns =list('abcd'))

print(df.index) # Index(['a', 'b', 'c', 'd'], dtype='object')
print(df.columns) # Index(['a', 'b', 'c', 'd'], dtype='object')
print(df.shape) # (2, 4)
print(df.ndim) # 2
print(df.size) # 8
```

### 색인 검색

```python
import pandas as pd
df = pd.DataFrame([[1, 2, 3, 4], [5, 6, 7 ,8]], index=list('ab'), columns =list('abcd'))

# print(df[0]) # 주의 

print(df['a'])
# a    1
# b    5
# Name: a, dtype: int64
```

* 데이터프래임을 색인 검색 할 때는 주의해야 한다.   


  데이터프래임은 색인 검색할 때 열의 레이블을 검색하는 방식이므로, 정수 0을 지정해서 검색하면 아무것도 조회되지 않는다  

* 첫번째 열의 이름을 넣고 색인 연산을 수행하면 2개의 행을 출력한다. 

### 데이터프레임의 행으로 검색

: 데이터 프레임의 행을 검색하려면 별도의 인덱서\(indexer\)를 사용, 행의 레이블로 색인 연삭할때는 loc 인덱서를 사용

```python
import pandas as pd
df = pd.DataFrame([[1, 2, 3, 4], [5, 6, 7 ,8]], index=list('ab'), columns =list('abcd'))

print(df.loc['a'])
print(df.loc['a', :]) # 하나의 행을 조회하는 것은 행의 이름 하나와 모든 열을 슬라이스 하는 것과 같다 
# a    1
# b    2
# c    3
# d    4
# Name: a, dtype: int64
print(df.loc['a': ,'b': 'c'])
#    b  c
# a  2  3
# b  6  7
```

* 모든 행을 슬라이스하고, 열은 b와 c를 슬라이스하면 레이블 이름에 해당하는 열이 모두 조회된다

### 슬라이스 검색을 통한 부분 집합일 때 메모리 공유

```python
import pandas as pd
import numpy as np
df = pd.DataFrame([[1, 2, 3, 4], [5, 6, 7 ,8]], index=list('ab'), columns =list('abcd'))

dfv = df.loc['a': ,'b': 'c']
print(np.may_share_memory(dfv, df)) # true
```

* 데이터 프레임도 시리즈와 마찬가지로 슬라이스 검색은 뷰를 제공해서 원과 동일한 메모리를 공유한다 

### 인덱스 숫자 정보로 검색

: 데이터 프레임의 행을 조회할 때 정수 인덱스로 색인 연산을 할 수 있다.   
 이 때는 정수 인덱스로 검색할 수 있는 인덱서 iloc를 사용해야 한다

```python
import pandas as pd
import numpy as np
df = pd.DataFrame([[1, 2, 3, 4], [5, 6, 7 ,8]], index=list('ab'), columns =list('abcd'))

print(df.iloc[0])
# a    1
# b    2
# c    3
# d    4
# Name: a, dtype: int64
print(df.iloc[0,0])
# 1
s = df.iloc[:, 0]
print(np.may_share_memory(s, df)) # True
```

* 정수 인덱스를 처리할 때도 메모리를 공유되는 것을 알 수 있다 

