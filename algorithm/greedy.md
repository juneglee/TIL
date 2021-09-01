# Greedy

## Greedy

## 그리디\(탐욕\) 알고리즘 \(Greedy\)

: 그 순간순간마다 최적이라고 생각되는 결정을 하는 방식으로 진행하여 최종 해답에 도달하는 문제 해결 방식  
 경우의 수가 존재할 경우, 경우를 선택해야할 때 최선이라고 생각하는 경우를 선택하는 알고리즘

* 그리디 알고리즘 예 

  : 지불해야 하는 값이 있을때, 동전으로 동전 수가 가장 적게 지불하는 방식 

### 최소 신장 트리 \(MinimumSpanningTree, MST\)

: 사용된 간선들의 가중치 합이 최소인 트리

### MST의 특징

* 간선의 가중치의 합이 최소여야한다 
* n개의 정점을 가지는 그래프에 대해 반드시 \(n-1\)개의 간선만을 사용해야 한다 
* 사이클이 포함되어서는 안된다 

MST의 종류 : Greedy, Prim's, Kruskal's

### 그리디 알고리즘 예제\(Baek5585\)

* 타로는 자주 JOI잡화점에서 물건을 산다. 
* JOI잡화점에는 잔돈으로 500엔, 100엔, 50엔, 10엔, 5엔, 1엔이 충분히 있고,
* 언제나 거스름돈 갯수가 가장 적게 잔돈을 준다. 타로가 JOI잡화점에서 물건을 사고 카운터에서 1000엔 지폐를 한장 냈을 때, 
* 받을 잔돈에 포함된 잔돈의 갯수를 구하는 프로그램을 작성하시오

```java
// 입력 : 380 출력 : 4
public class Baek5585 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in); 
        int money = 1000 - sc.nextInt();
        int[] array = { 500, 100, 50, 10, 5, 1 };
        int idx = 0;
        int ans = 0;
        while (money != 0) {
            int change = money / array[idx];
            money -= change * array[idx++];
            ans += change;
        }
        System.out.println(ans);
    }
}
```

```python
a = 1000 - int(input())
b = [500, 100, 50, 10, 5, 1]
count = 0
for i in b:
    count += a // i
    a %= i
print(count)
```

