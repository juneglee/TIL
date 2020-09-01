### recursion

### 재귀를 이용한 한자릿수 만들기 

```java
// input 자연수 n이 주어졌을 때
// ex1) 10 일 경우 1 + 0 => 1
// ex2) 456789 일 경우 4 + 5 + 6 + 7 + 8 + 9 => 39
//                     39 = > 3 + 9 = > 12 
//                     12 = > 1 + 2 => 3
public class recursion {
	public static int compute(int source) {
		if (source < 10) {
			return source;
		}
		
		String sourceStr = Integer.toString(source);
		
		int sum = 0;
		for (int i = 0 ; i < sourceStr.length(); i ++) {
			char ch = sourceStr.charAt(i);
			int num = (int) ch - 48; // 아스키 코드
			sum +=num;
		}
		return compute(sum); // 재귀 호출 
	}
	
	public static void main(String[] args) {
		int num = compute(456789);
		System.out.println(num); // 3
	}
}

```