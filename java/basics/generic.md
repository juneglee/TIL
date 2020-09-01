### Generic

### 제네릭 (Generic)
```
일반 메서드 --> Object(다형적 변수)  --> 제네릭 (Object 단점 극복)
```
- 같은 클래스에서 다루는 객체의 타입이 달라서 타입별로 만들어야 할 메서드 및 출력이 무한정으로 늘어나게 된다
- 다양한 객체 저장할 수 있도록 다형성의 다형적 변수 특징을 이용하여 값을 저장하는 인스턴스 변수를 Object 타입으로 정의하여 사용한다. 근데 Object를 사용하게 되면 의도와 다른 타입의 값을 저장하는 것이 있을 수 있다
- 이러한 단점을 극복하기 위해서 제네릭(Generic)을 사용하여 지정한 한개의 클래스로 다양한 타입의 객체를 제한적으로 다룰 수 있도록 한다. 제네릭을 사용하면 각 타입 별로 따로 클래스를 정의한 효과가 있다 

### 제네릭 사용 이유
- 일반 메서드로 출력

```java
ObjectBox box1= new ObjectBox();
box1.set(new Member("홍길동",20));
Member m= (Member) box1.get(); // 값을 꺼낼 때 형변환해야 한다
System.out.println(m);
```

- 의도와 다른 타입의 값을 저장하는 것이 있을 수 있다 (Object 단점)

```java
MemberBox box1= new MemberBox();
box1.set(new Member("홍길동",20)); 
box1.set(new String("Hello"));
```
- 위의 member로 메서드를 정의했기 때문에 사용을 할 수 없지만, set에서는 object로 정의했기 때문에 String을 받을 수 있게 되어서 의도하지 않기 다른 타입의 값을 저장

### 제네릭 사용 

1. 다루는 타입을 제한할 수 있다. 
- 어떤 종류(타입,클래스)의 객체를 저장할 것인지 지정할 수 있으며, 지정된 타입 이외는 저장할 수 없다.
- 방법 : 클래스명<타입명> : 

```
ArrayList<Member> list = new ArrayList</*Member*/>();
list.add(new Member("홍길동", 20));
```
    - 제네릭 문법으로 레퍼런스 변수를 선언할 때는 타입명을 생략할 수 없다
    - 레퍼런스 선언에 제네릭 정보가 있다면 new 연산자에서는 생략할 수 있다.
       

2. 제네릭을 지정하면 그와 관련된 메서드의 타입 정보가 자동으로 바뀐다.
- 형변환하는 번거로움이 없다. (타입 변환(casting)을 제거 한다 )

3. T변수 = "타입 파라미터" - 클래스의 객체 타입 (ex> element, obj, datatype)
 element = E, type = T, key = K,  number = N, value = v ,<br>
 s= 2번째  U =3번째  v=4번째 파라미터  <br>
 ex) class Box <T, S, U, V> 
