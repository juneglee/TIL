# String

## String 문자열

## Heap 메모리 영역에 String 인스턴스를 생성하는 방법

```java
String s1 = new String("Hello"); 
String s2 = new String("Hello");
System.out.println(s1 == s2);  false
```

=&gt; 내용물의 동일 여부를 검사하지 않고 무조건 인스턴스를 생성한다. =&gt; garbage가 되면 garbage collection에 의해 제거된다.

## string constant pool 메모리 영역에 String 인스턴스를 생성하는 방법

```java
String x1 = "Hello";  String 인스턴스의 주소를 리턴한다.
String x2 = "Hello";  기존의 String 인스턴스 주소를 리턴한다.
System.out.println(x1 == x2);  true
```

=&gt; Heap 이 아닌 String 상수풀에 생성한다. =&gt; 기존 인스턴스의 주소를 리턴, 중복 데이터를 갖는 인스턴스를 생성하지 않는다. =&gt; JVM이 끝날 때까지 메모리에 유지된다.

### String vs StringBuffer 비교에 따른 차이점

```java
String s1 = new String("Hello"); 
String s2 = new String("Hello");
String s3 = "Hello";
System.out.println(s1.equals(s2));  // 결과: true  인스턴스 주소로 비교하여 값이 동일
System.out.println(s1.equals(s3));  // 결과: true  String 클래스에서 equals()를 오버라이딩
// --------------------------------------------------------------------------------------------------------
StringBuffer b1 = new StringBuffer("Hello");
StringBuffer b2 = new StringBuffer("Hello");
System.out.println(b1 == b2);  // 결과 : false  b1, b2 인스턴스가 다르니까 당연히 결과는 false이다.
System.out.println(b1.equals(b2));  // 결과 : false 상속 받은 equals()를 오버라이딩 않고 Object의 equals()를 사용
```

### 해결책?

```java
 System.out.println(b1.toString().equals(b2.toString()));
// => StringBuffer에서 String을 꺼내 비교하라! 
// --------------------------------------------------------------------------------------
String s1 = new String("Hello");
System.out.println(s1);  결과값 : Hello
System.out.println(s1.toString());  결과값 : Hello

String s2 = s1.toString()
System.out.println(s1 == s2); true
```

=&gt; 위의 코드는 프로젝트의 toString 과정이랑 동일한 과정을 가지고 있다 s1이 String이기 때문에 toString\(\)은 따로 String을 만들지 않고 그냥 s1 주소를 리턴한다. 결국 인스턴스이 주소를 비교하여 동일한 값이 되게 된다

## String - mutable vs immutable 객체

* String 객체는 immutable 객체이다. 즉 한 번 객체에 값을 담으면 변경할 수 없다.
* StringBuffer는 mutable 객체이다. 원래의 문자열을 변경하고 싶을 때 사용하는 클래스이다.

### StringBuffer를 사용할 때 주의사항!

* StringBuffer의 내용물을 비교할 때 equals\(\) 사용해봐야 소용없다. == 연산자와 같은 결과를 출력한다.
* Stringbuffer은 object에서 상속 받은 equals\(\)를 오버라이딩하지 않았기 때문에오버라이딩을 하지 않은 object의 equals\(\) 적용되게 된다

## 다형적 변수와 toString

```java
Object obj = new String("Hello");  인스턴스 주소가 100이라 가정하자;
String x1 = (String) obj;  x1 = 100
String x2 = obj.toString();  x2 = 100
System.out.println(x1 == x2);
```

=&gt; 레퍼런스를 통해 메서드를 호출할 때 항상 원래 객체의 클래스부터 메서드를 찾아 올라간다. =&gt; 따라서 obj가 가리키는 객체의 클래스가 String이기 때문에 obj.toString\(\)은 String 클래스부터 해당 메서드를 찾는다. =&gt; String 클래스는 toString\(\)을 오버라이딩 했기 때문에 결국 obj.toString\(\)은 String 클래스에서 오버라이딩 한 toString\(\)을 호출하는 것이다.

```java
Object (최상위)
toString()

A (상위)
toString(), m1()

B (하위, 상속)
toString(), m1(), m2()

// 컴파일러는 Object obj의 메서드만 확인하며, tpye 따라서만 확인한다

Object obj = new Object();
obj.toString(); O - object에 있는 toString()를 가져와서 사용한 것이다
obj.m1(); X object에는 m1라는 메서드가 선언된 것이 없기 때문에 m2 은 사용할 수 없다

// 컴파일러가 메서드를 찾을 때는 해당 클래스부터 찾는다

Object obj = new A();
obj.toString(); O - B에 있는 toString()를 가져와서 사용한 것이다
obj.m1(); O - B에 있는 m1()를 가져와서 사용한 것이다
obj.m2(); X

// 해당 클래스에 선언된 메스드가 없으면 상위 클래스에서 선언된 것을 사용한다 

Object obj = new B();
obj.toString(); O - A에 있는 toString()를 가져와서 사용한 것이다
obj.m1(); O - B에 있는 m1()를 가져와서 사용한 것이다
obj.m2(); O
```

* 이런 과정을 거치기 때문에 객체지향은 반복으로 사용하기 때문에 C보다 느리다

## 다형적 변수와 형변환, toLoverCaser\(\)

* obj를 통해 원래 인스턴스 메서드를 호출

```java
Object obj = new String("Hello");

// 1. 원래 타입으로 형변환하라.
String str = ((String)obj).toLowerCase();
System.out.println(str);
// 2. 원래 타입의 레퍼런스에 저장한 다음 사용하라.
String x1 = (String) obj;
str = x1.toLowerCase();
System.out.println(str);
```

## Wrapper 클래스

래퍼 클래스의 주요 용도:   
 =&gt; primitive data type의 값을 객체로 주고 받을 때 사용한다.  
 =&gt; primitive data type의 값을 객체에 담아 전달하고 싶다면 언제든 wrapper 클래스의 인스턴스를 만들면 된다.  


```java
Byte b2 = Byte.valueOf((byte)100); 
Short s2 = Short.valueOf((short)20000); 
Integer i2 = Integer.valueOf(3000000); 
Long l2 = Long.valueOf(60000000000L); 
Float f2 = Float.valueOf(3.14f); 
Double d2 = Double.valueOf(3.14159); 
Boolean bool2 = Boolean.valueOf(true); 
Character c2 = Character.valueOf((char)0x41);
```

```java
 int ==> Integer  Integer.valueOf  오토박싱(auto-boxing) - 자동으로 
int i1 = 100;
Integer obj1 = Integer.valueOf(i1);
```

```java
 Integer ==> int  obj2.intValue
Integer obj2 = Integer.valueOf(200);
int i2 = obj2.intValue();
```

* auto-boxing/auto-unboxing 기능이 있기 때문에 한 개의 메서드로 primitive data type과 클래스를 모두 처리할 수 있는 것이다

Integer obj1 = new Integer\(100\);

* new를 생성하여 Heap에 인스턴스를 저장하는 것이 주소가 아니라 Data의 값이기 때문에 ==를 통해 비교하면 동일한 값이 나오지 않는다 

Integer obj1 = 100;

* 정수 리터럴을 이용하여 auto-boxing으로 객체를 생성할 경우 constants pool에 생성
* 같은 값을 가지는 Integer 객체가 여러 개 존재해야 할 필요가 없다.

Integer obj5 = Integer.valueOf\(100\);

* 위와 동일한 코드이다

int i2 = obj2.intValue\(\);

* auto-unboxing ???

