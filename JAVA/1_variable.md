# 변수 (Variable)

: 하나의 값을 저장할 수 있는 기억공간(메모리 공간)

메모리 종류(타입) | 메모리 별명(변수)
--- | --- 
[Data type] | [Variables]
ex) int | ex) i
기본형 (Primitive type) | 참조형 (Reference type)
8개 (byte, short, int, long, char, boolean, float, double) <br>
- 실제 값을 저장 | 기본형을 제외한 나머지(String, Thread) <br>
- 다른 메모리의 주소를 저장하는 변수

### 자바의 기본형 (Primitive type)
 | 1Byte (8bit) | 2Byte( 16bit) | 4Byte (32bit) | 8Byte (64bit)
--- | --- | --- | --- | ---
논리형|boolean|||
문자형||char|| 
정수형|byte|short|int|long
실수형||float|double

### 변수의 저장
```java
int score; // 변수 선언
score = 90;  // 값을 저장
int score = 90;  // 변수 선언과 동시에 값을 저장
```

여러 개의 변수 선언과 값 초기화 시키기
```java
int i = 100, j, k = 300;
```

새 값으로 변경
```java
int = i;
i = 100;
i = 200;  
```
변수는 사용전에 반드시 선언
```java
i = 100; // 컴파일 오류
int i, j; 
j = 200; // 새 값으로 변경된다
```

- 변수는 선언된 블록 내에서만 사용이 가능하다 
- 변수는 중괄호 {} 블록 내에서 선언되고 사용되며, 메서드 블록 내에서도 여라가지 중괄호 {} 블록들이 있을 수 있기 때문에,
  어떤 범위에서 사용될 것인지 생각하고, 선언 위치를 결정해야 한다.

### 변수의 명명 규칙(Naming convention)
1. 대소문자가 구분되며 길이에 제한이 없다 
    - True와 true는 서로 다른 것으로 간주된다
2. 예약어 (Reserved Word)를 사용해서는 안된다.
    - true 는 예약어라 사용할 수 없지만, True는 가능하다
3. 숫자로 시작해서는 안된다.
4. 특수문자는 ‘_’ 와 ‘$’만을 허용한다