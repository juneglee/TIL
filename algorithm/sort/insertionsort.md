# insertionSort

## insertion Sort

## 삽입 정렬

: 자료 배열의 모든 요소를 앞에서부터 차례대료 이미 정렬된 배열 부분과 비교하여, 자신의 위치를 찾아 삽입

* 다른 정렬 방식은 무조건 위치를 바꾸는 방식이였다면 삽입 정렬은 필요할 때만 위치를 바꾸게 된다 
* 삽입 정렬은 비교적 느린 정렬 알고리즘에 속하며, 복잡한 구조를 가지고 있다 
* 만약, 정렬이 되었다고 가장하면 특정한 경우에 따라 빠른 속도를 가지게 되며, 
* 삽입 정렬의 시간 복잡도는 O\(N^2\)이다 

## 정렬 방법

![InsertionSort](../../.gitbook/assets/InsertionSort.png)   
 ![InsertionSort](../../.gitbook/assets/InsertionSort.gif)   


* 다음과 같이 앞에서 부터 차례대로 정렬된 부분과 비교하여, 적절한 위치를 찾아가는 것을 볼 수 있다.
* 특징으로는 계속 비교하므로 리스크 크기가 크면 불리하며, 정렬이 비교적 완성된 데이터의 경우에는 더 유리하다

```java
public class InsertionSort {
    public static void main(String[] args) {
        int i, j, temp;
        int[] arr = { 1, 10, 5, 8, 7, 6, 4, 3, 2, 9 };
        for (i = 0; i < arr.length-1 ; i++) { 
            j = i; 
            while (j >= 0 && arr[j] > arr[j + 1]) {
                temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
                j--; 
            }
        }
        for ( i = 0; i < arr.length ; i++) {
            System.out.printf("%d ", arr[i]);
        }
    }
}
```

```python
array = [1, 10, 5, 8, 7, 6, 4, 3, 2, 9]

for i in range(1, len(array)):
    for j in range(i, 0, -1): # 인덱스 i부터 1까지 1씩 감소하며 반복하는 문법
        if array[j] < array[j - 1]: # 한 칸씩 왼쪽으로 이동
            array[j], array[j - 1] = array[j - 1], array[j]
        else: # 자기보다 작은 데이터를 만나면 그 위치에서 멈춤
            break

print(array)
```

[Reference : Wikipedia](https://ko.wikipedia.org/wiki/%EC%82%BD%EC%9E%85_%EC%A0%95%EB%A0%AC#JAVA)

