# class

### Class

클래스 기반의 객체 지향 프로그래밍 언어는 클래스라는 것을 기반으로 객체를 만들고, 그러한 객체를 우선으로 생각해서 프로그래밍하는 것을 이념으로 삼고 있다

* 핵심 키워드 

  객체 : 속성을 가질 수 있는 모든 것을 의미

  객체 지향 프로그래밍 언어 : 객체를 기반으로 프로그램을 만드는 프로그래밍 언어 

  추상화 : 복잡한 자료, 모듈, 시스템 등으로부터 핵심적인 개념 도는 기능을 간추려 나는 것 

  클래스 : 객체를 쉽고 편리하게 생성하기 위해 만드렁진 구문

  인스턴스 : 클래스를 기반으로 생성한 객체를 의미 

  생성자 : 클래스 이름과 같은 인스턴스

  메소드 : 클래스가 가진 함수 

### 추상화

* 프로그램에서 필요한 요소만을 사용해서 객체를 표현하는 것 
* 복잡한 자료, 모듈, 시스템 등으로부터 핵심적인 개념 도는 기능을 간추려 나는 것

  ```python
  students = [
    { "name": "윤인성", "korean": 87, "math": 98, "english": 88, "science": 95 },
    { "name": "연하진", "korean": 92, "math": 98, "english": 96, "science": 98 },
    { "name": "구지연", "korean": 76, "math": 96, "english": 94, "science": 90 },
    { "name": "나선주", "korean": 98, "math": 92, "english": 96, "science": 92 },
    { "name": "윤아린", "korean": 95, "math": 98, "english": 98, "science": 98 },
    { "name": "윤명월", "korean": 64, "math": 88, "english": 92, "science": 92 }
  ]
  print("이름", "총점", "평균", sep="\t")
  for student in students:
    score_sum = student["korean"] + student["math"] +\
        student["english"] + student["science"]
    score_average = score_sum / 4
    print(student["name"], score_sum, score_average, sep="\t")
  ```

## 객체를 만드는 함수 \(1\)

```python
def create_student(name, korean, math, english, science):
    return {
        "name": name,
        "korean": korean,
        "math": math,
        "english": english,
        "science": science
    }
students = [
    create_student("윤인성", 87, 98, 88, 95),
    create_student("연하진", 92, 98, 96, 98),
    create_student("구지연", 76, 96, 94, 90),
    create_student("나선주", 98, 92, 96, 92),
    create_student("윤아린", 95, 98, 98, 98),
    create_student("윤명월", 64, 88, 92, 92)
]

print("이름", "총점", "평균", sep="\t")
for student in students:
    score_sum = student["korean"] + student["math"] +\
        student["english"] + student["science"]
    score_average = score_sum / 4
    print(student["name"], score_sum, score_average, sep="\t")
```

## 객체를 처리하는 함수 \(2\)

```python
# 딕셔너리를 리턴하는 함수를 선언합니다.
def create_student(name, korean, math, english, science):
    return {
        "name": name,
        "korean": korean,
        "math": math,
        "english": english,
        "science": science
    }

# 학생을 처리하는 함수를 선언합니다.
def student_get_sum(student):
    return student["korean"] + student["math"] +\
        student["english"] + student["science"]

def student_get_average(student):
    return student_get_sum(student) / 4

def student_to_string(student):
    return "{}\t{}\t{}".format(
        student["name"],
        student_get_sum(student),
        student_get_average(student))

students = [
    create_student("윤인성", 87, 98, 88, 95),
    create_student("연하진", 92, 98, 96, 98),
    create_student("구지연", 76, 96, 94, 90),
    create_student("나선주", 98, 92, 96, 92),
    create_student("윤아린", 95, 98, 98, 98),
    create_student("윤명월", 64, 88, 92, 92)
]

print("이름", "총점", "평균", sep="\t")
for student in students:
    print(student_to_string(student))
```

### 클래스

사용법

```text
class 클래스 이름:
     클래스 내용 
class Student:
```

### 인스턴스

사용법 인스턴스 이름\(변수 이름\) = 클래스 이름\(\) \# 생성자 함수라고 부른다

```text
class Student: # 클래스 선언
   psss
```

```python
student = Student() # 학생을 선언

students =[ # 학생 리스트 선언
   Student(),
   Student(),
   Student(),
   Student(),
   Student(),
   Student()
]
```

### 생성자

```text
class 클래스 이름:
   def __init__(self, 추가적인 매개변수):
      pass
# 여기서 self 는 자기 자신을 나타내는 딕셔너리
# 접근할 때는 self.<식별자> 형태로 접근
```

```python
class Student:
    def __init__(self, name, korean, math, english, science):
        self.name = name
        self.korean = korean
        self.math = math
        self.english = english
        self.science = science

students = [
    Student("윤인성", 87, 98, 88, 95),
    Student("연하진", 92, 98, 96, 98),
    Student("구지연", 76, 96, 94, 90),
    Student("나선주", 98, 92, 96, 92),
    Student("윤아린", 95, 98, 98, 98),
    Student("윤명월", 64, 88, 92, 92)
]

print(students[0].name)
print(students[1].name)
print(students[2].name)
print(students[3].name)
print(students[4].name)
print(students[5].name)
```

### 소멸자

생성자와 반대로 인스턴스가 소멸될 때 호출되는 함수

```text
def __del__
```

### 메서드

```text
class 클래스 이름:
   def 메소드 이름 (self, 추가적인 매개변수):
      pass
```

```python
# 클래스내부에 함수(메서드) 선언하기 
class Student:
    def __init__(self, name, korean, math, english, science):
        self.name = name
        self.korean = korean
        self.math = math
        self.english = english
        self.science = science

    def get_sum(self):
        return self.korean + self.math +\
            self.english + self.science

    def get_average(self):
        return self.get_sum() / 4

    def to_string(self):
        return "{}\t{}\t{}".format(\
            self.name,\
            self.get_sum(),\
            self.get_average())

students = [
    Student("윤인성", 87, 98, 88, 95),
    Student("연하진", 92, 98, 96, 98),
    Student("구지연", 76, 96, 94, 90),
    Student("나선주", 98, 92, 96, 92),
    Student("윤아린", 95, 98, 98, 98),
    Student("윤명월", 64, 88, 92, 92)
]

print("이름", "총점", "평균", sep="\t")
for student in students:
    print(student.to_string())
```

### 어떤 클래스의 인스턴스인지 확인하기 : isinstance

```text
isinstance(인스턴스, 클래스) 확인 
isinstance(student, Student) : true
# 단순 인스턴스 확인
# type(student) == Student
# 이때 isinstance() 함수는 상속관계까지 확인하고, 
# 반면 type() 함수는 상속관계를 확인하지 않는다
```

```python
class Student:
    def study(self):
        print("공부를 합니다.")
class Teacher:
    def teach(self):
        print("학생을 가르칩니다.")

classroom = [Student(), Student(), Teacher(), Student(), Student()]

for person in classroom:
    if isinstance(person, Student):
        person.study()
    elif isinstance(person, Teacher):
        person.teach()
```

### 특수한 이름의 메소드 : **str**\(\) 함수

객체를 문자열로 변환할 수 있으며, to\_String\(\) 함수를 대신하여 사용

```python
class Student:
    def __init__(self, name, korean, math, english, science):
        self.name = name
        self.korean = korean
        self.math = math
        self.english = english
        self.science = science
    def get_sum(self):
        return self.korean + self.math +\
            self.english + self.science
    def get_average(self):
        return self.get_sum() / 4
    def __str__(self):
        return "{}\t{}\t{}".format(
            self.name,
            self.get_sum(),
            self.get_average()) 
students = [
    Student("윤인성", 87, 98, 88, 95),
    Student("연하진", 92, 98, 96, 98),
    Student("구지연", 76, 96, 94, 90),
    Student("나선주", 98, 92, 96, 92),
    Student("윤아린", 95, 98, 98, 98),
    Student("윤명월", 64, 88, 92, 92)
]
print("이름", "총점", "평균", sep="\t")
for student in students:
    print(str(student))
```

### 특수한 이름의 메소드 : 비교함수

| 함수 | 정의 |
| :--- | :--- |
| eq | equal \(같다\) |
| ne | not equal \(다르다\) |
| gt | greater than \(크다\) |
| ge | greater than or equal \(크거나 같다\) |
| it | less than \(작다\) |
| le | less than or equal \(작거나 같다\) |

```python
class Student:
    def __init__(self, name, korean, math, english, science):
        self.name = name
        self.korean = korean
        self.math = math
        self.english = english
        self.science = science

    def get_sum(self):
        return self.korean + self.math +\
            self.english + self.science

    def get_average(self):
        return self.get_sum() / 4

    def __str__(self, student):
        return "{}\t{}\t{}".format(
            self.name,
            self.get_sum(student),
            self.get_average(student))

    def __eq__(self, value): 
        return self.get_sum() == value.get_sum()
    def __ne__(self, value): 
        return self.get_sum() != value.get_sum()
    def __gt__(self, value):
        return self.get_sum() > value.get_sum()
    def __ge__(self, value):
        return self.get_sum() >= value.get_sum()
    def __lt__(self, value):
        return self.get_sum() < value.get_sum()
    def __le____(self, value):
        return self.get_sum() <= value.get_sum()

students = [
    Student("윤인성", 87, 98, 88, 95),
    Student("연하진", 92, 98, 96, 98),
    Student("구지연", 76, 96, 94, 90),
    Student("나선주", 98, 92, 96, 92),
    Student("윤아린", 95, 98, 98, 98),
    Student("윤명월", 64, 88, 92, 92)
]

student_a = Student("윤인성", 87, 98, 88, 95),
student_b = Student("연하진", 92, 98, 96, 98),

print("student_a == student_b = ", student_a == student_b)
print("student_a != student_b = ", student_a != student_b)
print("student_a >  student_b = ", student_a >  student_b)
print("student_a >= student_b = ", student_a >= student_b)
print("student_a <  student_b = ", student_a <  student_b)
print("student_a <= student_b = ", student_a <= student_b)
```

### 클래스 변수와 메소드

클래스 변수

```python
# 사용
class 클래스 이름:
    클래스 변수 = 값
# 접근
클래스 이름.변수 이름
```

```python
class Student:
    count = 0

    def __init__(self, name, korean, math, english, science):
        self.name = name
        self.korean = korean
        self.math = math
        self.english = english
        self.science = science

        Student.count += 1
        print("{}번째 학생이 생성되었습니다.".format(Student.count))


students = [
    Student("윤인성", 87, 98, 88, 95),
    Student("연하진", 92, 98, 96, 98),
    Student("구지연", 76, 96, 94, 90),
    Student("나선주", 98, 92, 96, 92),
    Student("윤아린", 95, 98, 98, 98),
    Student("윤명월", 64, 88, 92, 92)
]

print()
print("현재 생성된 총 학생 수는 {}명입니다.".format(Student.count))
```

```python
# 사용
class 클래스 이름:
    @classmethod
    클래스 변수 = 값
# 접근
클래스 이름.변수 이름(매개변수 )
# @classmethod : 데코레이터 
# @로 시작하는 것을 파이썬에서는 데코레이터라고 하며 "꾸며주는 것"이라는 의미를 가진다 
# 함수 데코레이터와 클래스 데코레이터로 나뉜다.
```

```python
class Student:
    count = 0
    students = []

    @classmethod
    def print(cls):
        print("------ 학생 목록 ------")
        print("이름\t총점\t평균")
        for student in cls.students:
            print(str(student))
        print("------- ------- -------")

    def __init__(self, name, korean, math, english, science):
        self.name = name
        self.korean = korean
        self.math = math
        self.english = english
        self.science = science
        Student.count += 1
        Student.students.append(self)

    def get_sum(self):
        return self.korean + self.math +\
            self.english + self.science

    def get_average(self):
        return self.get_sum() / 4

    def __str__(self):
        return "{}\t{}\t{}".format(\
            self.name,\
            self.get_sum(),\
            self.get_average())

Student("윤인성", 87, 98, 88, 95)
Student("연하진", 92, 98, 96, 98)
Student("구지연", 76, 96, 94, 90)
Student("나선주", 98, 92, 96, 92)
Student("윤아린", 95, 98, 98, 98)
Student("윤명월", 64, 88, 92, 92)
Student("김미화", 82, 86, 98, 88)
Student("김연화", 88, 74, 78, 92)
Student("박아현", 97, 92, 88, 95)
Student("서준서", 45, 52, 72, 78)

Student.print()
```

