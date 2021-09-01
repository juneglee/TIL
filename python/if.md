# if

## if

```text
If <조건문>:
    <수행할 문장1> 
    <수행할 문장2>
    ...
elif <조건문>:
    <수행할 문장1>
    <수행할 문장2>
    ...
elif <조건문>:
    <수행할 문장1>
    <수행할 문장2>
    ...
...
else:
   <수행할 문장1>
   <수행할 문장2>
   ...
```

* 조건문 다음에 콜론\(:\)을 잊지 말자!

### if 조건문의 기본사용

```python
number = input("정수 입력> ")
number = int(number)

#0 일때 
if number == 0:
    print("0입니다.")
#양수 조건
if number > 0:
    print("양수입니다.")
#음수 조건
if number < 0:
    print("음수입니다.")
```

### if~else 와 elif

```python
# if 조건문에 else 구문을 추가해서 짝수와 홀수 구분
number = input("정수 입력> ")
number = int(number)

if number % 2 == 0:
    # 조건이 참일 때, 즉 짝수 조건
    print("짝수입니다")
else:
    # 조건이 거짓일 때, 즉 홀수 조건
    print("홀수입니다")
```

```python
pocket = ['paper', 'cellphone']
card = True
if 'money' in pocket:
    print("돈으로 택시를 타고가라")
elif card: 
    print("카드로 택시를 타고가라")
else:
    print("걸어가라")
# 카드로 택시를 타고가라
```

### if 조건문을 효율적으로 사용하기

```python
score = float(input("학점 입력> "))

#조건으로 구현하기 1
if score == 4.5:
    print("신")
elif 4.2 <= score < 4.5:
    print("교수님의 사랑")
elif 3.5 <= score < 4.2:
    print("현 체제의 수호자")
elif 2.8 <= score < 3.5:
    print("일반인")
elif 2.3 <= score < 2.8:
    print("일탈을 꿈꾸는 소시민")
elif 1.75 <= score < 2.3:
    print("오락문화의 선구자")
elif 1.0 <= score < 1.75:
    print("불가촉천민")
elif 0.5 <= score < 1.0:
    print("자벌레")
elif 0 < score < 0.5:
    print("플랑크톤")
elif score == 0:
    print("시대를 앞서가는 혁명의 씨앗")

#조건으로 구현하기 2
if score == 4.5:
    print("신")
elif 4.2 <= score:
    print("교수님의 사랑")
elif 3.5 <= score:
    print("현 체제의 수호자")
elif 2.8 <= score:
    print("일반인")
elif 2.3 <= score:
    print("일탈을 꿈꾸는 소시민")
elif 1.75 <= score:
    print("오락문화의 선구자")
elif 1.0 <= score:
    print("불가촉천민")
elif 0.5 <= score:
    print("자벌레")
elif 0 < score:
    print("플랑크톤")
else:
    print("시대를 앞서가는 혁명의 씨앗")
```

### False로 변환되는 값

* None / '0' / 빈 컨테이너는 False로 반환된다.

  \`\`\`python

  **if 조건문에 0 넣기**

  if 0:

    print\("0은 True로 변환됩니다"\)

  else:

    print\("0은 False로 변환됩니다"\)

  **0은 False로 변환됩니다**

## if 조건문에 빈 문자열 넣기

if "": print\("빈 문자열은 True로 변환됩니다"\) else: print\("빈 문자열은 False로 변환됩니다"\)

## 빈 문자열은 False로 변환됩니다

```text
### Pass 키워드 
- 골격을 잡아놓고 나중에 처리하기 위해서 만들어짐
```python
number = input("정수 입력> ")
number = int(number)

# 빈 공간을 사용할 경우 indentationError가 발생한다 
# if number > 0:
    # 양수일 때: 아직 미구현 상태입니다.
# else:
    # 음수일 때: 아직 미구현 상태입니다.

# 이때 사용하기 위해서 pass를 사용하여 골격을 잡아 놓을 수 있다 
if number > 0:
    pass
else:
    pass

# raise NotImplementedError : 아직 구현하지 않은 부분이라고 오류를 강제로 발생할 수 있다 
if number > 0:
    raise NotImplementedError 
else:
    raise NotImplementedError
```

### 날짜/시간 활용하기 \(if, format\)

```python
import datetime
now = datetime.datetime.now()

# 날짜/시간 출력하기 : if
print(now.year , "년")
print(now.month , "월")
print(now.day , "일")
print(now.hour , "시")
print(now.minute , "분")
print(now.second , "초")

# 날짜/시간을 한줄로 출력하기 : format
print("{}년 {}월 {}일 {}시 {}분 {}초".format(
    now.year,
    now.month,
    now.day,
    now.hour,
    now.minute,
    now.second
))

# 오전과 오후를 구분하기
if now.hour < 12:
    print("현재 시간은 {}시로 오전입니다.".format(now.hour))
if now.hour > 12:
    print("현재 시간은 {}시로 오후입니다.".format(now.hour))

# 계절을 구분하기
if 3 <= now.month <= 5:
    print("이번 시간은 {}월로 봄입니다.".format(now.month))
if 6 <= now.month <= 8:
    print("이번 시간은 {}월로 여름입니다.".format(now.month))
if 9 <= now.month <= 11:
    print("이번 시간은 {}월로 가을입니다.".format(now.month))
if now.month == 12 or 1 <= now.month <= 2:
    print("이번 시간은 {}월로 겨울입니다.".format(now.month))
```

### elif를 이용하여 계절구하기

```python
import datetime

# 현재 날짜/시간을 구하고 쉽게 사용할 수 있게 월을 변수에 저장합니다.
now = datetime.datetime.now()
month = now.month

# 조건문으로 계절을 확인합니다.
if 3 <= month <= 5:
    print("현재는 봄입니다.")
elif 6 <= month <= 8:
    print("현재는 여름입니다.")
elif 9 <= month <= 11:
    print("현재는 가을입니다.")
else:
    print("현재는 겨울입니다.")
```

### 끝자리로 짝수와 홀수 구분하기

```python
number = input("정수 입력> ")

last_character = number[-1] #마지막 자리 숫자를 추출
last_number = int(last_character) # 숫자로 변환하기 

# 짝수 확인
if last_number == 0 \
    or last_number == 2 \
    or last_number == 4 \
    or last_number == 6 \
    or last_number == 8:
    print("짝수 입니다")
# 홀수 확인
if last_number == 1 \
    or last_number == 3 \
    or last_number == 5 \
    or last_number == 7 \
    or last_number == 9:
    print("홀수 입니다")

# in 문자열 연산자를 활용해서 짝수와 홀수 구분
if last_character in "02468":
    print("짝수 입니다")
if last_character in "13579":
    print("홀수 입니다")

# 나머지 연산자를 활용해서 짝수와 홀수 구분
number = int(number)
if number % 2 == 0:
    print("짝수 입니다")
if number % 2 == 1:
    print("홀수 입니다")
```

