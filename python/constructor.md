# Constructor

## Constructor

## 생성자 \(Constructor\)

* 객체를 생성할 때 호출되는 함수로서, 객체 생성시 초기화 작업을 위해 존재

```python
class 클래스명: 
    def __init__(self): 
        문장
```

* 다음과 같이  **init**라는 이름으로 미리 정의되며, 생성자를 통해서 객체가 생성될때 어떤 변수의 값을 세팅하는 등 여러가지 작업을 할수 있다 

```python
class example:
    def __init__(self, sentence): 
        self.name = sentence 
        print("객체가 생성: " + sentence + "입니다.") 

object= example("사과") # 객체가 생성: 사과입니다.
```

```python
class Student:
    def __init__(self, name, age): 
        self.name = name
        self.age = age
    def introduction(self):
        print("제 이름은 " + self.name + "이며, 제 나이는 " + str(self.age) + "살입니다.")

objectStudent = Student("원빈", 28)
objectStudent.introduction() # 제 이름은 원빈이며, 제 나이는 28살입니다.
```

### 소멸자 \(Destructor\)

* 생성자와 반대로 객체가 소멸할때 호출되는 소멸자가 있다 
* **del**으로 정의 되어 있으며, 리소스 해체 등의 종료 작업을 하기 위해 사용

```python
class 클래스명: 
    def __del__(self): 
        문장
```

```python
class Student:
    def __init__(self, name, age): 
        self.name = name
        self.age = age
        print("객체 생성 : 제 이름은 " + self.name + "이며, 제 나이는 " + str(self.age) + "살입니다.")

    def __del__(self):
        print("객체 소멸")

objectStudent = Student("원빈", 28)
# 객체 생성 : 제 이름은 원빈이며, 제 나이는 28살입니다.
print(objectStudent) # <__main__.Student object at 0x0000029D72681F48>
del objectStudent
# 객체 소멸
# print(objectStudent) # name 'objectStudent' is not defined
```

