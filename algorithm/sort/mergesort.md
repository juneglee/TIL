# mergeSort

## Merge Sort

## 병합 정렬\(Merge Sort\)

: 주어진 배열을 원소가 하나 밖에 남지 않을 때까지 계속 둘로 쪼갠 후에 다시 크기 순으로 재배열 하면서 원래 크기의 배열로 합친다

* 병합 정렬은 분할 정복 기법과 재귀 알고리즘을 이용한 정렬 알고리즘
* 시간 복잡도는 O\(NlogN\)이다 
* 공간 복잡도는 O\(N\)
* 다른 정렬 알고리즘과 달리 인접한 값들 간에 상호 자리 교대\(swap\)이 일어나지 않는다  

## 정렬 방법

리스트의 길이가 1 이하이면 이미 정렬된 것으로 본다. 그렇지 않은 경우에는 1. 분할\(divide\) : 정렬되지 않은 리스트를 절반으로 잘라 비슷한 크기의 두 부분 리스트로 나눈다. 2. 정복\(conquer\) : 각 부분 리스트를 재귀적으로 합병 정렬을 이용해 정렬한다. 3. 결합\(combine\) : 두 부분 리스트를 다시 하나의 정렬된 리스트로 합병한다. 이때 정렬 결과가 임시배열에 저장된다. 4. 복사\(copy\) : 임시 배열에 저장된 결과를 원래 배열에 복사한다.

![MergeSort](../../.gitbook/assets/MergeSort.gif)

```java
public class MergeSort {
    private static void sort(int[] arr, int low, int high) {
        if (high - low < 2) {
            return;
        }

        int mid = (low + high)/2;
        sort(arr, 0, mid);
        sort(arr, mid, high);
        merge(arr, low, mid, high);
    }

    private static void merge(int[] arr, int low, int mid, int high) {
        int[] temp = new int[high - low];
        int t = 0;
        int l = low;
        int m = mid;

        while(l < mid && m < high) {
            if (arr[l] < arr[m]) {
                temp[t++] = arr[l++];
            } else {
                temp[t++] = arr[m++];
            }
        }

        while (l < mid) {
            temp[t++] = arr[l++];
        }

        while (m < high) {
            temp[t++] = arr[m++];
        }

        for (int i = low; i < high; i++) {
            arr[i] = temp[i - low];
        }
    }

    public static void main(String[] args) {
        int[] x = { 1, 10, 5, 8, 7, 6, 4, 3, 2, 9 };

        sort(x, 0, x.length);

        for (int i = 0; i <  x.length; i++)
            System.out.println("x[" + i + "]＝" + x[i]);

    }
}
```

[Reference : Wikipedia](https://ko.wikipedia.org/wiki/%ED%95%A9%EB%B3%91_%EC%A0%95%EB%A0%AC)

