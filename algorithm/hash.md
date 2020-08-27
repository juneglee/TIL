### Hash
: 검색과 더불어 데이터의 추가와 삭제도 효율적으로 수행할 수 있는 방법 <br>
요소 이동에 필요한 시간 복잡도는 O(n)이며, 삭제 할떄도 같은 비용으로 발생

```
F(key) -> Hashcode -> index -> value
```
- 검색하고자 하는 키값을 받아서 해쉬함수로 돌려서 반환받은 hashcode를 이용해서 배열의 index를 이용해서 데이터의 자료에 접근하는 방법 key 값은 숫자, 문자열, 파일 등에 해당한다 
- 해쉬 테이블은 hashcode % size로 나누어 인덱스로 사용한다 
- 들어올때마다 linkedList로 저장하고 찾는다 

- 충돌의 따라서 분류(Collision)
- O(1) -> O(N)까지 복잡도가 늘어난다 
- 체인법 : 같은 해시 값을 갖는 요소를 연결 리스트로 관리 
- 오픈 주소법 : 빈 버킷을 찾을 때까지 해시를 반복 

### 해시와 해시 함수에 대하여 
만약 충돌이 전형 발생하지 않는다면 해시 함수로 인덱스를 찾는 것만으로 검색, 추가, 삭제가 거의 완료 되므로 시간 복잡도는 어느 것이나 O(1)이 된다 <br>
해시 테이블을 크게 하면 충돌 발생을 억제 할 수 있지만 다른 한편으로 메모리를 쓸데없이 많이 차지한다 즉, 시간과 공간의 절출(trade-Off)이라는 문제가 항상 따라 다닙니다. <br>
충돌을 피하기 위해 해시 함수는 해시 테이블 크기 이하의 정수를 되도록 한쪽으로 치우치지 않고 고르게 만들어야 한다 그래서 해시 테이블 크기는 소수가 좋다고 알려져있다 <br>
키 값이 정수가 아닌 경우 해시 값을 구할 떄는 좀 더 신경을 써 방법으 모색해야 한다.  예건대 실수 키 값에 대해 비트 연산(bitwise operation)을 하는 방법, <br>
문자열 키 값에 대해 각 문자 코드에 곱셈과 덧셈을 하는 앙법이 있다 <br>

### 오픈 주소법에 의한 해시

```java
public class OpenHash<K,V> {
	// 버킷의 상태
	enum Status {OCCUPIED, EMPTY, DELETED};		// {데이터 저장, 비어 있음, 삭제 마침}

	// 버킷
	static class Bucket<K,V> {
		private K key;							// 키 값
		private V data;							// 데이터
		private Status stat;					// 상태

		// 생성자
		Bucket() {
			stat = Status.EMPTY;				// 버킷은 비어 있음
		}

		// 모든 필드에 값을 설정합니다.
		void set(K key, V data, Status stat) {
			this.key  = key;					// 키 값
			this.data = data;					// 데이터
			this.stat = stat;					// 상태
		}

		// 상태를 설정합니다.
		void setStat(Status stat) {
			this.stat = stat;
		}

		// 키 값을 반환합니다.
		K getKey() {
			return key;
		}

		// 데이터를 반환합니다.
		V getValue() {
			return data;
		}

		// 키의 해시 값을 반환합니다.
		public int hashCode() {
			return key.hashCode();
		}
	}

	private int size;						// 해시 테이블의 크기
	private Bucket<K,V>[] table;			// 해시 테이블

	// 생성자
	public OpenHash(int size) {
		try {
			table = new Bucket[size];
			for (int i = 0; i < size; i++)
				table[i] = new Bucket<K,V>();
			this.size = size;
		} catch (OutOfMemoryError e) {		// 테이블을 생성할 수 없음
			this.size = 0;
		}
	}

	// 해시 값을 구함
	public int hashValue(Object key) {
		return key.hashCode() % size;
	}

	// 재해시값을 구함
	public int rehashValue(int hash) {
		return (hash + 1) % size;
	}

	// 키 값 key를 갖는 버킷의 검색
	private Bucket<K,V> searchNode(K key) {
		int hash = hashValue(key);				// 검색할 데이터의 해시값
		Bucket<K,V> p = table[hash];			// 선택 버킷

		for (int i = 0; p.stat != Status.EMPTY && i < size; i++) {
			if (p.stat == Status.OCCUPIED && p.getKey().equals(key))
				return p;
			hash = rehashValue(hash);			// 재해시
			p = table[hash];
		}
		return null;
	}

	// 킷값 key를 갖는 요소의 검색 (데이터를 반환)
	public V search(K key) {
		Bucket<K,V> p = searchNode(key);
		if (p != null)
			return p.getValue();
		else
			return null;
	}

	// 키 값 key, 데이터 data를 갖는 요소의  추가
	public int add(K key, V data) {
		if (search(key) != null)
			return 1;							// 이 키 값은 이미 등록됨

		int hash = hashValue(key);				// 추가할 데이터의 해시 값
		Bucket<K,V> p = table[hash];			// 선택 버킷
		for (int i = 0; i < size; i++) {
			if (p.stat == Status.EMPTY || p.stat == Status.DELETED) {
				p.set(key, data, Status.OCCUPIED);
				return 0;
			}
			hash = rehashValue(hash);			// 재해시
			p = table[hash];
		}
		return 2;								// 해시 테이블이 가득 참
	}

	// 키 값 key를 갖는 요소의 삭제
	public int remove(K key) {
		Bucket<K,V> p = searchNode(key);		// 선택 버킷
		if (p == null)
			return 1;							// 이 키 값은 등록되지 않음

		p.setStat(Status.DELETED);
		return 0;
	}

	// 해시 테이블을 덤프
	public void dump() {
		for (int i = 0; i < size; i++) {
			System.out.printf("%02d ", i);
			switch (table[i].stat) {
			 case OCCUPIED : 
				System.out.printf("%s (%s)\n", 
										table[i].getKey(), table[i].getValue());
				break;

			 case EMPTY :
			 	System.out.println("-- 미등록 --");	break;

			 case DELETED :
			 	System.out.println("-- 삭제 마침 --");	break;
			}
		}
	}
}
```

```java

public class OpenHashTester {

	static Scanner stdIn = new Scanner(System.in);

	// 데이터 (회원번호 + 이름)
	static class Data {
		static final int NO   = 1;		// 번호를 읽어 들일까요?
		static final int NAME = 2;		// 이름을 읽어 들일까요?

		private Integer no;				// 회원번호 (키 값)
		private String  name;			// 이름

		// 키 값
		Integer keyCode() {
			return no;
		}

		// 문자열을 반환합니다.
		public String toString() {
			return name;
		}

		// 데이터를 입력합니다.
		void scanData(String guide, int sw) {
			System.out.println(guide + "할 데이터를 입력하세요.");

			if ((sw & NO) == NO) {
				System.out.print("번호：");
				no = stdIn.nextInt();
			}
			if ((sw & NAME) == NAME) {
				System.out.print("이름：");
				name = stdIn.next();
			}
		}
	}

	// 메뉴 열거형
	enum Menu {
		ADD(      "추가"),
		REMOVE(   "삭제"),
		SEARCH(   "검색"),
		DUMP(     "출력"),
		TERMINATE("종료");

		private final String message;			// 나타낼 문자열 

		static Menu MenuAt(int idx) {			// 서수가 idx인 열거를 반환합니다.
			for (Menu m : Menu.values())
				if (m.ordinal() == idx)
					return m;
			return null;
		}

		Menu(String string) {					// 생성자
			message = string;
		}

		String getMessage() {					// 나타낼 문자열을 반환
			return message;
		}
	}

	// 메뉴 선택
	static Menu SelectMenu() {
		int key;
		do {
			for (Menu m : Menu.values())
				System.out.printf("(%d) %s  ", m.ordinal(), m.getMessage());
			System.out.print("：");
			key = stdIn.nextInt();
		} while (key < Menu.ADD.ordinal() || key > Menu.TERMINATE.ordinal());

		return Menu.MenuAt(key);
	}

	public static void main(String[] args) {
		Menu menu;								// 메뉴
		Data data;								// 추가용 데이터 참조
		Data temp = new Data();					// 입력용 데이터

		OpenHash<Integer, Data> hash = new OpenHash<Integer, Data>(13);

		do {
			switch (menu = SelectMenu()) {
			 case ADD :									// 추가
				data = new Data();
				data.scanData("추가", Data.NO | Data.NAME);
			 	int k = hash.add(data.keyCode(), data);
			 	switch (k) {
			 	 case 1: System.out.println("그 키 값은 이미 등록되어 있습니다.");
			 	 			break;
			 	 case 2: System.out.println("해시 테이블이 가득 찼습니다.");
			 	 			break; 
			 	}
			 	break;

			 case REMOVE :								// 삭제
			 	temp.scanData("삭제", Data.NO);
			 	hash.remove(temp.keyCode());
			 	break;

			 case SEARCH :								// 검색
				temp.scanData("검색", Data.NO);
			 	Data t = hash.search(temp.keyCode());
			 	if (t != null)
			 		System.out.println("그 키를 갖는 데이터는 " + t + "입니다.");
				else
		 			System.out.println("그 데이터가 없습니다.");
			 	break;

			 case DUMP : 								// 출력
			 	hash.dump();
			 	break;
			}
		} while (menu != Menu.TERMINATE);
	}
}
```

### 체인법

```java
public class ChainHash<K,V> {
	// 해시를 구성하는 노드
	class Node<K,V> {
		private K key;					// 키 값
		private V data;					// 데이터
		private Node<K,V> next;			// 다음 노드에 대한 참조

		// 생성자
		Node(K key, V data, Node<K,V> next) {
			this.key  = key;
			this.data = data;
			this.next = next;
		}

		// 키 값을 반환합니다.
		K getKey() {
			return key;
		}

		// 데이터를 반환합니다.
		V getValue() {
			return data;
		}

		// 키의 해시값을 반환합니다.
		public int hashCode() {
			return key.hashCode();
		}
	}

	private int	size;						// 해시 테이블의 크기
	private Node<K,V>[] table;				// 해시 테이블

	// 생성자
	public ChainHash(int capacity) {
		try {
			table = new Node[capacity];
			this.size = capacity;
		} catch (OutOfMemoryError e) {		// 테이블을 생성할 수 없음
			this.size = 0;
		}
	}

	// 해시값을 구함
	public int hashValue(Object key) {
		return key.hashCode() % size;
	}

	// 키 값 key를 갖는 요소의 검색 (데이터를 반환)
	public V search(K key) {
		int hash = hashValue(key);			// 검색할 데이터의 해시값
		Node<K,V> p = table[hash];			// 선택 노드

		while (p != null) {
			if (p.getKey().equals(key))
				return p.getValue();		// 검색 성공
			p = p.next;						// 다음 노드에 주목
		}
		return null;						// 검색 실패
	}

	// 키 값 key, 데이터 data를 갖는 요소의  추가
	public int add(K key, V data) {
		int hash = hashValue(key);			// 추가할 데이터의 해시값
		Node<K,V> p = table[hash];			// 선택 노드

		while (p != null) {
			if (p.getKey().equals(key))		// 이 키 값은 이미 등록됨
				return 1;
			p = p.next;						// 다음 노드에 주목
		}
		Node<K,V> temp = new Node<K,V>(key, data, table[hash]);
		table[hash] = temp;					// 노드를 삽입
		return 0;
	}

	// 키 값 key를 갖는 요소의 삭제
	public int remove(K key) {
		int hash = hashValue(key);			// 삭제할 데이터의 해시 값
		Node<K,V> p = table[hash];			// 선택 노드
		Node<K,V> pp = null;				// 바로 앞의 선택 노드

		while (p != null) {
			if (p.getKey().equals(key)) {	//  찾으면
				if (pp == null)
					table[hash] = p.next;
				else
					pp.next = p.next;
				return 0;
			}
			pp = p;
			p = p.next;						// 다음 노드를 가리킴
		}
		return 1;							// 그 키 값은 없습니다. 
	}

	// 해시 테이블을 덤프
	public void dump() {
		for (int i = 0; i < size; i++) {
			Node<K,V> p = table[i];
			System.out.printf("%02d  ", i);
			while (p != null) {
				System.out.printf("→ %s (%s)  ", p.getKey(), p.getValue());
				p = p.next;
			}
			System.out.println();
		}
	}
}
```

```java

class ChainHashTester {
	static Scanner stdIn = new Scanner(System.in);

	// 데이터 (회원번호 + 이름)
	static class Data {
		static final int NO   = 1;		// 번호를 읽어 들일까요?
		static final int NAME = 2;		// 이름을 읽어 들일까요?

		private Integer no;				// 회원번호 (키 값)
		private String  name;			// 이름

		// 키 값
		Integer keyCode() {
			return no;
		}

		// 문자열 표현을 반환합니다.
		public String toString() {
			return name;
		}

		// 데이터를 입력합니다.
		void scanData(String guide, int sw) {
			System.out.println(guide + "할 데이터를 입력하세요.");

			if ((sw & NO) == NO) {
				System.out.print("번호：");
				no = stdIn.nextInt();
			}
			if ((sw & NAME) == NAME) {
				System.out.print("이름：");
				name = stdIn.next();
			}
		}
	}

	// 메뉴 열거형
	enum Menu {
		ADD(      "추가"),
		REMOVE(   "삭제"),
		SEARCH(   "검색"),
		DUMP(     "출력"),
		TERMINATE("종료");

		private final String message;		// 나타낼 문자열 

		static Menu MenuAt(int idx) {		// 서수가 idx인 열거를 반환
			for (Menu m : Menu.values())
				if (m.ordinal() == idx)
					return m;
			return null;
		}

		Menu(String string) {				// 생성자
			message = string;
		}

		String getMessage() {				// 나타낼 문자열을 반환
			return message;
		}
	}

	// 메뉴 선택
	static Menu SelectMenu() {
		int key;
		do {
			for (Menu m : Menu.values())
				System.out.printf("(%d) %s  ", m.ordinal(), m.getMessage());
			System.out.print("：");
			key = stdIn.nextInt();
		} while (key < Menu.ADD.ordinal() || key > Menu.TERMINATE.ordinal());

		return Menu.MenuAt(key);
	}

	public static void main(String[] args) {
		Menu menu;								// 메뉴
		Data data;								// 추가용 데이터 참조
		Data temp = new Data();					// 입력용 데이터

		ChainHash<Integer, Data> hash = new ChainHash<Integer, Data>(13);

		do {
			switch (menu = SelectMenu()) {
			 case ADD :							// 추가
					data = new Data();
					data.scanData("추가", Data.NO | Data.NAME);
			 		hash.add(data.keyCode(), data);
			 		break;

			 case REMOVE :						// 삭제
			 		temp.scanData("삭제", Data.NO);
			 		hash.remove(temp.keyCode());
			 		break;

			 case SEARCH :						// 검색
					temp.scanData("검색", Data.NO);
			 		Data t = hash.search(temp.keyCode());
			 		if (t != null)
			 			System.out.println("그 키를 갖는 데이터는 " + t + "입니다.");
					else
			 			System.out.println("그 데이터가 없습니다.");
			 		break;

			 case DUMP : 						// 출력
			 		hash.dump();
			 		break;
			}
		} while (menu != Menu.TERMINATE);
	}
}
```