### module 

### module Overview
모듈(module) : 각종 변수, 함수, 클래스를 담고 있는 파일
패키지(Package) : 여러 모듈을 묶어 놓은 것, 모듈에 namespace를 제공
라이브러리(Python Standard Library, PSL) : 모듈, 패키지, 내장 함수를 묶어서 말한다

- 표준 모듈 : 파이썬에 기본적으로 내장되어 있는 모듈
- 외부 모듈 : 다른 사람들이 만들어 공개한 모듈

### import 사용법 : from, as
- from 구문 
: from 모듈 이름 import 가져오고 싶은 변수 또는 함수 
```
from 모듈이름 import 모듈함수
```
``` python
from math import sin, cos, tan, floor, ceil
from math import * # (모두 가져오기)
from math import sin, cos, tan, floor, ceil
print(math.sin(1))
```

- as 구문 
: 모듈을 가져올때 이름 출동을 방지하기 위해서 사용
```python
import math as m
print(m.sin(1))
```
### if __name__ == "__main__" 의 의미
: 프로그램의 시작점일 때만 코드를 실행한다는 의미로, __name__ 변수의 값이 __main__인지 확인하는 
코드는 현재 스크립트 파일이 프로그램의 시작점이 맞는지 판단하는 작업
즉, 직접 이 파일을 실행했을 때는 __name__ == "__main__"이 참이 되어 if문 다음 문장이 수행된다.
반대로 대화형 인터프리터나 다른 파일에서 이 모듈을 불러서 사용할 때는 
__name__ == "__main__"이 거짓이 되어 if문 다음 문장이 수행되지 않는다.

```python
# 직접 실행할 때
# module1.py
def add(a, b): 
    return a+b
def sub(a, b): 
    return a-b
if __name__ == "__main__":
    print(add(2, 10)) # 12
    print(sub(10, 2)) # 8
```
```python
# 대화형 인터프리터
import module1

print(module1.add(4,10)) # 14
print(module1.sub(10,4)) # 6
```
### math
: 수학과 관련된 기능 
- math.sin(), math.cos(), math.tan(), math.log(x.[base])
- math.ceil() - 올림
- math.floor() - 내림
- math.round() - 반올림, 단 홀수인 것들은 올림이 되고, 짝수는 내림이 된다.
```python
import math 
print(math.sin(1))
```

### random(randint, choice, shuffle) 
: 난수(규칙이 없는 임의의 수)를 발생시키는 모듈
- random : 0.0에서 1.0 사이의 실수 중에서 난수 값을 돌려준다
- randint : 정의된 정수 중에서 난수 값을 돌려준다 
- choice : 입력으로 받은 리스트에서 무작위로 하나를 선택하여 돌려준다
- shuffle : 리스트의 항목을 무작위로 섞고 싶을 때 사용
- uniform(min, max): 지정한 범위 사이의 float를 리턴
- randrange(): 지정한 범위의 int를 리턴합니다.
    - randrange(max): 0부터 max 사이의 값을 리턴합니다.
    - randrange(min, max): min부터 max 사이의 값을 리턴합니다.
- sample(list, k=<숫자>): 리스트의 요소 중에 k개를 뽑습니다.
```python
import random

print("- random: ", random.random())
print("- randinit: ", random.randint(1, 10)) 
print("- uniform: ", random.uniform(10, 20))
print("- randrange: ", random.randrange(10))
print("- choice: ", random.choice([1, 2, 3, 4, 5]))
print("- shuffle: ", random.shuffle([1, 2, 3, 4, 5]))
print("- sample: ", random.sample([1, 2, 3, 4, 5], k=2))

def random_pop(data):
    num = random.randint(0, len(data)-1)
    return data.pop(num)
if __name__ == "__main__":
    data = [1, 2, 3, 4, 5]
    while data:
        print(random_pop(data))
```

### sys
: 시스템과 관련된 정보를 가지고 있는 모듈 

```python
import sys
# 명령 행에서 인수 전달하기 : sys.argv
print(sys.argv) 
# 자신이 만든 모듈 불러와 사용하기 : - sys.path
sys.path
# 경로의 이름을 추가 : sys.path.append("")
sys.path.append("c:/user/python")
# 컴퓨터 환경과 관련된 정보를 출력합니다.
print("getwindowsversion:()", sys.getwindowsversion())
print("copyright:", sys.copyright)
print("version:", sys.version)
# 프로그램을 강제로 종료합니다.
sys.exit()
```
### os
: 환경 변수나 디렉터리, 파일 등의 OS 자원을 제어할 수 있게 해주는 모듈
```python
import os
# 기본 정보를 몇 개 출력해 봅시다.
print("현재 운영체제:", os.name)
print("현재 폴더:", os.getcwd()) # 디렉터리 위치 돌려받기 
print("현재 폴더 내부의 요소:", os.listdir())
# 내 시스템의 환경 변수값을 알고 싶을 때 - os.environ
# 디렉터리 위치 변경하기 - os.chdir
# 디렉터리 위치 돌려받기 - os.getcwd
# 시스템 명령어 호출하기 - os.system

# 폴더를 만들고 제거합니다[폴더가 비어있을 때만 제거 가능].
os.mkdir("hello") # 디렉터리 생성
os.rmdir("hello") # 데렉터리 삭제, 단 디렉터리가 비어있어야 삭제가 가능하다 

# 파일을 생성하고 + 파일 이름을 변경 : rename(기존 이름, 변경할 이름)
with open("original.txt", "w") as file:
    file.write("hello")
os.rename("original.txt", "new.txt")

# 파일을 제거 : remove, unlink
os.remove("new.txt")
# os.unlink("new.txt")

# 시스템 명령어 실행 : dir
os.system("dir")

# 실행한 시스템 명령어의 결과값 돌려 받기 : popen
f = os.popen("dir")
 print(f.read())
```
### datetime
: date(날짜), time(시간) 과 관련된 모듈
```python
import datetime

# 현재 시각을 구하고 출력하기
print("# 현재 시각 출력하기")
now = datetime.datetime.now()
print(now.year, "년")
print(now.month, "월")
print(now.day, "일")
print(now.hour, "시")
print(now.minute, "분")
print(now.second, "초")
print()

# 시간 출력 방법
print("# 시간을 포맷에 맞춰 출력하기")
output_a = now.strftime("%Y.%m.%d %H:%M:%S")
output_b = "{}년 {}월 {}일 {}시 {}분 {}초".format(now.year,\
now.month,\
now.day,\
now.hour,\
now.minute,\
now.second)
output_c = now.strftime("%Y{} %m{} %d{} %H{} %M{} %S{}").format(*"년월일시분초")
print(output_a)
print(output_b)
print(output_c)
print()

# 시간 처리하기 
import datetime
now = datetime.datetime.now()

# 특정 시간 이후의 시간 구하기
print("# datetime.timedelta로 시간 더하기")
after = now + datetime.timedelta(\
weeks=1,\
days=1,\
hours=1,\
minutes=1,\
seconds=1)
print(after.strftime("%Y{} %m{} %d{} %H{} %M{} %S{}").format(*"년월일시분초"))
print()

# 특정 시간 요소 교체하기
print("# now.replace()로 1년 더하기")
output = now.replace(year=(now.year + 1))
print(output.strftime("%Y{} %m{} %d{} %H{} %M{} %S{}").format(*"년월일시분초"))
```

### time
: 시간과 관련된 time 모듈 함수 
- time.time
:  UTC(Universal Time Coordinated 협정 세계 표준시)를 사용하여 현재 시간을 실수 형태로 돌려주는 함수이다. 1970년 1월 1일 0시 0분 0초를 기준으로 지난 시간을 초 단위로 돌려준다.
- time.localtime
: time.time()이 돌려준 실수 값을 사용해서 연도, 월, 일, 시, 분, 초, ... 의 형태로 바꾸어 주는 함수
```python
time.localtime(time.time())
```
- time.asctime
:time.localtime에 의해서 반환된 튜플 형태의 값을 인수로 받아서 날짜와 시간을 알아보기 쉬운 형태로 돌려주는 함수
```python
time.asctime(time.localtime(time.time()))
```
- time.ctime
:항상 현재 시간만을 돌려준다
```python
time.ctime()
```
- time.strftime
:시간에 관계된 것을 세밀하게 표현하는 여러 가지 포맷 코드를 제공
```python
time.strftime('출력할 형식 포맷 코드', time.localtime(time.time()))
```
- time.sleep
:일정한 시간 간격을 두고 루프를 실행
```python
import time
print("지금부터 5초 동안 정지합니다!")
time.sleep(5)
print("프로그램을 종료합니다")
```

### calendor
: 달력을 볼 수 있게 해주는 모듈
```python
print(calendar.calendar(2015))
calendar.prcal(2015) 
calendar.prmonth(2015, 12) 
calendar.weekday(2015, 12, 31) #  0 ~ 6, 월요일은 0, 화요일은 1, 수요일은 2, 목요일은 3, 금요일은 4, 토요일은 5, 일요일은 6
calendar.monthrange(2015,12) #  1일이 무슨 요일인지와 그 달이 며칠까지 있는지를 튜플 형태로 돌려준다
```
### urllib
: URL을 다루는 라이브러리 
```python
from urllib import request
# urlopen() 함수로 구글의 메인 페이지를 읽습니다.
target = request.urlopen("https://google.com")
output = target.read()
print(output)
```

### pickle
:객체의 형태를 그대로 유지하면서 파일에 저장하고 불러올 수 있게 하는 모듈

### shutil
: 파일을 복사해 주는 파이썬 모듈
```python
 import shutil
shutil.copy("src.txt", "dst.txt")
# 동일한 이름이 있으면 덮어쓴다
```
### glob
: 디렉터리에 있는 파일들을 리스트로 만들기
```python
import glob
glob.glob("c:/user/python*")
```
### tempfile
:파일을 임시로 만들어서 사용할 때
```python
import tempfile
filename = tempfile.mkstemp()
 # 중복되지 않는 임시 파일의 이름을 무작위로 만들어서 돌려준다
print(filename)
f = tempfile.TemporaryFile() 
# 임시 저장 공간으로 사용할 파일 객체를 돌려준다. 기본적으로 바이너리 쓰기 모드(wb) 
f.close() # 종료 호출이 되면 파일 객체는 자동으로 사라진다
```
### webbrowser
: 자신의 시스템에서 사용하는 기본 웹 브라우저를 자동으로 실행하는 모듈