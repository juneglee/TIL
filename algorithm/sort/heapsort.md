# heapSort

## Heap Sort

## 힙정렬 \(Heap Sort\)

: 힙트리 구조 \(Heap Tree Structure\) 를 이용하는 정렬 방법   
 힙은 이진트리 \(Binart Tree: 데이터를 각 노드\(node\)에 담은 뒤에 노드를 두개씩 이어 붙이는 구조\)

## 정렬 방법

1. n개의 노드에 대한 완전 이진 트리를 구성한다. 이때 루트 노드부터 부모노드, 왼쪽 자식노드, 오른쪽 자식노드 순으로 구성한다.
2. 최대 힙을 구성한다. 최대 힙이란 부모노드가 자식노드보다 큰 트리를 말하는데, 단말 노드를 자식노드로 가진 부모노드부터 구성하며 아래부터 루트까지 올라오며 순차적으로 만들어 갈 수 있다.
3. 가장 큰 수\(루트에 위치\)를 가장 작은 수와 교환한다.
4. 2와 3을 반복한다.

![HeapSort](../../.gitbook/assets/HeapSort.gif)

```java
class HeapSort {
    // 배열 요소 a[idx1]과 a[idx2]의 값을 바꿉니다. 
    static void swap(int[] a, int idx1, int idx2) {
        int t = a[idx1];  
        a[idx1] = a[idx2];  
        a[idx2] = t;
    }

    // a[left] ~ a[right]를 힙으로 만듭니다. 
    // a[left] 이외에는 모두 힙상태라고 가정하고 a[left]를 아랫부분의 알맞은 위치로 옯겨 힙 상태를 만든다 
    static void downHeap(int[] a, int left, int right) {
        int temp = a[left];                // 루트
        int child;                        // 큰 값을 가진 노드
        int parent;                        // 부모

        for (parent = left; parent < (right + 1) / 2; parent = child) {
            int cl = parent * 2 + 1;                            // 왼쪽 자식
            int cr = cl + 1;                                    // 오른쪽 자식
            child = (cr <= right && a[cr] > a[cl]) ? cr : cl;    // 큰 값을 가진 노드를 자식에 대입 
            if (temp >= a[child])
                break;
            a[parent] = a[child];
        }
        a[parent] = temp;
    }

    // 힙 정렬
    // 요소의 개수가 n개인 배열 a를 힙 정렬하는 메서드 이다 
    // downHeap메서드를 사용하여 배열 a를 힙으로 만든다 
    // 루트(a[0]) 에 있는 가장 큰 값을 빼내어 마지막 요소와 바꾸고 배열의 나머비 부분을 다시 힙으로 만드는 과정을 반복하여 정렬을 수행 
    static void heapSort(int[] a, int n) {
        for (int i = (n - 1) / 2; i >= 0; i--)    // a[i] ~ a[n-1]를 힙으로 만들기
            downHeap(a, i, n - 1);

        for (int i = n - 1; i > 0; i--) {
            swap(a, 0, i);                // 가장 큰 요소와 아직 정렬되지 않은 부분의 마지막 요소를 교환
            downHeap(a, 0, i - 1);        // a[0] ~ a[i-1]을 힙으로 만듭니다.
        }
    }

    public static void main(String[] args) {
        int[] x = { 1, 10, 5, 8, 7, 6, 4, 3, 2, 9 };

        heapSort(x, 10); // 배열 x를 퀵 정렬

        for (int i = 0; i <  x.length; i++)
            System.out.println("x[" + i + "]＝" + x[i]);
    }
}
```

