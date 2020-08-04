# String format 

### format 
- 문자열을 가지고 있는 함수 
- "{}".format(10) 형식이며 
-  중괄호의 개수와 괄호안의 매개변수의 개수가 반드시 같아야한다
```python
String_a = "{}".format(10)
String_b = "{} {}".format(10, 20)
String_c = "{} {} {}".format(10, 20, 30)  
print(String_a) # 10
print(String_b) # 10 20 
print(String_c) # 10 20 30
```

### 문자열 포맷 코드
| 코드 | 설명 |
| --- | --- |
| %s | 문자열(String) |
| %c | 문자 1개(Character) |
| %d | 정수(Integer) |
| %f | 부동소수(floating-point) |
| %o | 8진수 |
| %x | 16진수 |
| %% | Literal % (문자 % 자체) |

### 포맷 코드 사용
    ```python
    >>> "I eat %s apples." % "five"
    'I eat five apples.'
    ```
    ```python
    >>> "I eat %d apples." % 3
    'I eat 3 apples.'
    ```
    ```python
    >>> number = 3
    >>> "I eat %d apples." % number
    'I eat 3 apples.'
    ```
    ```python
    >>> number = 10
    >>> day = "three"
    >>> "I ate %d apples. so I was sick for %s days." % (number, day)
    'I ate 10 apples. so I was sick for three days.'
    ```
- 정렬과 공백 
    ```python
    >>> "%10s" % "hi"
    '        hi'
    ```
    ```python
    >>> "%-10sjane." % 'hi'
    'hi        jane.'
    ```
    ```python
    >>> "%0.4f" % 3.42134234
    '3.4213'
    ```
    ```python
    >>> "%10.4f" % 3.42134234
    '    3.4213'
    ```

### format 함수를 사용 : "{}".format(x)
- 숫자 대입
```python
>>> "I eat {0} apples".format(3) 
# {0}은 인덱스로 format 함수의 0번째 값으로 입력하고 출력한다 
'I eat 3 apples'
```

- 문자열 대입
```python
"{0} coffee".format("five")
'five coffee'
```

- 2개상의 값 넣기
```python
>>> "I ate {number} apples. so I was sick for {day} days.".format(number=10, day=3)
'I ate 10 apples. so I was sick for 3 days.'
```

- 소수점 표현하기
```python
>>> y = 3.42134234
>>> "{0:0.4f}".format(y)
'3.4213'
>>> "{0:10.4f}".format(y)
'    3.4213'
```

- { 또는 } 문자 표현하기
```python
>>> "{{ and }}".format()
'{ and }'
```

### format 함수의 정렬과 공백
- 왼쪽 정렬 (:<) 
```python
>>> "{0:<10}".format("hi")
'hi        '
```

- 오른쪽 정렬 (:>)
```python
>>> "{0:>10}".format("hi")
'        hi'
```

- 가운데 정렬 (:^)
```python
>>> "{0:^10}".format("hi")
'    hi    '
```

- 정렬 후 공백채우기 
```python
>>> "{0:=^10}".format("hi")
'====hi===='
>>> "{0:!<10}".format("hi")
'hi!!!!!!!!'
```

### format 함수와 슬라이싱 이용
- format() 함수의 다양한 기능
```python
output_a = "{:d}".format(52)     #52
```

- 특정 칸에 출력
```python
output_b = "{:5d}".format(52)    #   52
output_c = "{:10d}".format(52)   #        52
```

- 빈칸을 0으로 채우기 
```python
output_d = "{:05d}".format(52)   #00052
output_e = "{:05d}".format(-52)  #-0052
```

- 기호와 함께 출력하기
```python
output_f = "{:+d}".format(52)    #+52 
output_g = "{:+d}".format(-52)   #-52 
output_h = "{: d}".format(52)    # 52 # 공백이 채워지지 않는다  
output_i = "{: d}".format(-52)   #-52 
```

- 조합하기
```python
output_j = "{:+5d}".format(52)   #  +52 
output_k = "{:+5d}".format(-52)  #  -52
output_l = "{:=+5d}".format(52)  #+  52
output_m = "{:=-5d}".format(-52) #-  52 
output_n = "{:+05d}".format(52)  #+0052
output_o = "{:-05d}".format(-52) #-0052 
```

- 부동 소수점 출력의 다양한 형태
```python
output_1 = "{:f}".format(52.273) #52.273000 # 정수와 유사하다 
output_2 = "{:15.3f}".format(52.273) # ... 52.273
output_3 = "{:15.2f}".format(52.273) # ...  52.27
output_4 = "{:15.1f}".format(52.273) # ...   52.2
```

-  의미 없는 부동 소수점 제거  
```python
output_g1 = 52.0
output_g2 = "{:g}".format(output_g1)
print(output_g1) # 52.0 
print(output_g2) # 52
```