# file

## 파일 열고 닫기 : open\(\), close\(\)

* 파일 처리

  파일은 크게 텍스트 파일과 바이너리 파일로 나뉨

  파일을 처리하려면 일단 파일열기를 하고, 파일을 열면 파일 읽기 또는 파일 쓰기를 한다 

* open\(\) : 파일 객체 = open\(문자열: 파일경로, 문자열: 모드\)
* close\(\) : 파일객체.close\(\)

  | 파일열기모드 | 설명 |
  | :--- | :--- |
  | w | write모드 \(새로쓰기 모드\) |
  | a | append 모드 \(뒤에 이어서 쓰기 모드\) |
  | r | read 모드 \(읽기 모드\) |

```python
file = open("basic.txt", "w") # w : write모드 (새로쓰기 모드)
file.write("Hello Python Programming...!")
file.close()
```

## with 키워드

* open\(\) 함수와 close\(\) 함수 사이에 많으 코드가 들어가, 열고 닫지 않는 실수하는 경우가 생기는 것을 방지하는 기능

  ```text
  with open(문자열: 파일경로, 문자열: 모드) as 파일 객체:
      문장
  ```

  ```python
  with open("basic.txt", "w") as file:
    file.write("Hello Python Programming...!")
  ```

## 텍스트 읽기 : read\(\)

```text
파일 객체.read()
```

```python
with open("basic.txt", "r") as file:
    contents = file.read()
print(contents)
```

## 텍스트 읽기 : readline\(\)

* readline\(\)을 사용해서 파일의 첫 번째 줄을 읽어 출력하는 경우

  ```python
  f = open("C:/user/새파일.txt", 'r')
  line = f.readline()
  print(line)
  f.close()
  ```

## 텍스트 읽기 :readlines\(\)

* readlines 함수는 파일의 모든 줄을 읽어서 각각의 줄을 요소로 갖는 리스트로 돌려준다.

  ```python
  f = open("C:/user/새파일.txt", 'r')
  lines = f.readlines()
  for line in lines:
    print(line)
  f.close()
  ```

## 텍스트 한 줄씩 읽기 : CSV

* 데이터를 구조적으로 표현할 수 있는 방법으로 CSV, XML, JSON 등이 있다 
* CSV 파일은 한줄에 하나의 데이터를 나타내며, 각각의 줄은 쉼표를 사용해 데이터를 구분

  \`\`\`python

  import random

  hanguls = list\("가나다라마바사아자차카타파하"\)

with open\("info.txt", "w"\) as file: for i in range\(1000\): name = random.choice\(hanguls\) + random.choice\(hanguls\) weight = random.randrange\(40, 100\) height = random.randrange\(140, 200\) file.write\("{}, {}, {}\n".format\(name, weight, height\)\)

```text
### 데이터를 한줄 씩 읽어 들일 때는 for 반복문을 사용
```

for 한줄을 나타내는 문자열 in 파일 객체 처리

```text
```python 
with open("info.txt", "r") as file:
    for line in file:
        (name, weight, height) = line.strip().split(", ")

        # 데이터가 문제없는지 확인합니다: 문제가 있으면 지나감
        if (not name) or (not weight) or (not height):
            continue

        # 결과를 계산
        bmi = int(weight) / ((int(height) / 100) **2)
        result = ""
        if 25 <= bmi:
            result = "과체중"
        elif 18.5 <= bmi:
            result = "정상 체중"
        else:
            result = "저체중"

        print('\n'.join([
            "이름: {}",
            "몸무게: {}",
            "키: {}",
            "BMI: {}",
            "결과: {}"
        ]).format(name, weight, height, bmi, result))
        print()
```

