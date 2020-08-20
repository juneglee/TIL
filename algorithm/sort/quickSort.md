### Quick Sort

### 퀵 정렬 (Quick Sort)
: 특정한 값을 기준(피벗)으로 큰 숫자와 작은 숫자를 서료 교환한 뒤에 배열을 반으로 나눈다 
- 대표적인 분할 정복 알고리즘으로 평균 속도가 O(N*logN)이다 
- 하지만 퀵 정렬 최악 시간 복잡도는 O(N^2)이다

### 정렬 방법 
퀵 정렬은 분할 정복(divide and conquer) 방법을 통해 리스트를 정렬한다.
1. 리스트 가운데서 하나의 원소를 고른다. 이렇게 고른 원소를 피벗이라고 한다.
2. 피벗 앞에는 피벗보다 값이 작은 모든 원소들이 오고, 피벗 뒤에는 피벗보다 값이 큰 모든 원소들이 오도록 피벗을 기준으로 리스트를 둘로 나눈다. 
이렇게 리스트를 둘로 나누는 것을 분할이라고 한다. 분할을 마친 뒤에 피벗은 더 이상 움직이지 않는다.
3. 분할된 두 개의 작은 리스트에 대해 재귀(Recursion)적으로 이 과정을 반복한다. 재귀는 리스트의 크기가 0이나 1이 될 때까지 반복된다.
재귀 호출이 한번 진행될 때마다 최소한 하나의 원소는 최종적으로 위치가 정해지므로, 이 알고리즘은 반드시 끝난다는 것을 보장할 수 있다.

![QuickSort](../../img/algorithm/QuickSort.gif) <br>

```java
public class QuickSort {
	// a[idx1]와 a[idx2]의 값을 바꿉니다.
	static void swap(int[] a, int idx1, int idx2) {
		int t = a[idx1];
		a[idx1] = a[idx2];
		a[idx2] = t;
	}

	// 퀵 정렬
	static void quickSort(int[] a, int left, int right) {
		int pl = left; // 왼쪽 커서
		int pr = right; // 오른쪽 커서
		int x = a[(pl + pr) / 2]; // 피벗

		do {
			while (a[pl] < x)
				pl++;
			while (a[pr] > x)
				pr--;
			if (pl <= pr)
				swap(a, pl++, pr--);
		} while (pl <= pr);

		if (left < pr)
			quickSort(a, left, pr);
		if (pl < right)
			quickSort(a, pl, right);
	}
	
	public static void main(String[] args) {
		int[] x = { 1, 10, 5, 8, 7, 6, 4, 3, 2, 9 };

		quickSort(x, 0, x.length - 1); // 배열 x를 퀵 정렬

		for (int i = 0; i <  x.length; i++)
			System.out.println("x[" + i + "]＝" + x[i]);
	}
}
```

[Reference : Wikipedia](https://ko.wikipedia.org/wiki/%EC%82%BD%EC%9E%85_%EC%A0%95%EB%A0%AC#JAVA){: target="_blank"}