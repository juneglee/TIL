### BreadthFirstSearch


### 너비 우선 탐색(BFS, Breadth-First Search)
: 루트 노드(혹은 다른 임의의 노드)에서 시작해서 인접한 노드를 먼저 탐색하는 방법 ( 즉, 깊게(deep) 탐색하기 전에 넓게(wide) 탐색) <br>
두 노드 사이의 최단 경로 혹은 임의의 경로를 찾고 싶을 때 이 방법을 선택한다.

### 너비 우선 탐색(BFS)의 특징
- 직관적이지 않은 면이 있다.(BFS는 시작 노드에서 시작해서 거리에 따라 단계별로 탐색한다고 볼 수 있다.)
- BFS는 재귀적으로 동작하지 않는다.
- BFS는 방문한 노드들을 차례로 저장한 후 꺼낼 수 있는 자료 구조인 큐(Queue)를 사용한다.(즉, 선입선출(FIFO) 원칙으로 탐색)
- ‘Prim’, ‘Dijkstra’ 알고리즘과 유사하다.

![BFS](../../img/algorithm/BFS.gif) <br>

```java
public class BFSGraph {
	private int V; // 노드의 개수
	private LinkedList<Integer> adj[]; // 인접 리스트

	/* 생성자 */
	public BFSGraph(int v) {
		V = v;
		adj = new LinkedList[v];
		for (int i = 0; i < v; ++i) // 인접 리스트 초기화
			adj[i] = new LinkedList();
	}

	/* 노드를 연결 */
	void addEdge(int v, int w) {
		adj[v].add(w);
	}

	/* s를 시작 노드로 한 BFS로 탐색하면서 탐색한 노드들을 출력 */
	void BFS(int s) {
		// 노드의 방문 여부를 판단
		boolean visited[] = new boolean[V];
		// BFS 구현을 위한 큐 (Queue) 생성
		LinkedList<Integer> queue = new LinkedList<Integer>();

		// 현재 노드를 방문한 것을 큐에 삽입 (enqueue)
		visited[s] = true;
		queue.add(s);

		// 모두가 출력 할 때까지 Queue를 반복
		while (queue.size() != 0) {
			// 방문한 노드를 큐에서 추출(dequeue)하고 값을 출력
			s = queue.poll();
			System.out.print(s + " ");

			// 방문한 도으와 인업한 모든 노드를 가져온다
			Iterator<Integer> i = adj[s].listIterator();
			while (i.hasNext()) {
				int n = i.next();
				// 방문하지 않는 노드면 방문한 것으로 표시하고 큐에 삽입
				if (!visited[n]) {
					visited[n] = true;
					queue.add(n);
				}
			}
		}
	}

	public static void main(String[] args) {
		BFSGraph g = new BFSGraph(4);

		g.addEdge(0, 1);
		g.addEdge(0, 2);
		g.addEdge(1, 2);
		g.addEdge(2, 0);
		g.addEdge(2, 3);
		g.addEdge(3, 3);
		
		System.out.println("vertax 2에서 시작하는 BFS(너비 우선 탐색)");
		g.BFS(2); /* 주어진 노드를 시작 노드로 BFS 탐색 */
		// 2 0 3 1 
	}
}
```