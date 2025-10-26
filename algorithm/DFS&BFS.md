### DFS란?
- 루트 노드 혹은 임의 노드에서 다음 브랜치로 넘어가기 전에, 해당 브랜치를 모두 탐색하는 방법
- 스택 or 재귀함수를 통해 구현
- 모든 경로를 방문해야 할 경우에 적합

### DFS 시간 복잡도
- 인접 행렬의 경우 O(V^2)
- 인접 리스트의 경우 O(V+E)
- V는 접점, E는 간선

```java
// Inorder로 트리를 dfs 순회
void dfs(Node n){
    if(n==null) return;
    dfs(n.left);
    System.out.println(n.value);
    dfs(n.right);
}
```

### BFS란?
- 루트 노드 또는 임의 노드에서 인접한 노드부터 먼저 탐색하는 방법
- 큐를 통해 구현한다. 
- 최소 비용 (모든 곳을 탐색하는 것보다 최소 비용이 우선일 때)에 적합

### BFS 시간 복잡도
- 인접 행렬 : O(V^2)
- 인접 리스트 : O(V+E)

```java
void bfs(Node start) {
    ArrayDeque<Node> deque = new ArrayDeque<>();
    HashSet<Node> visited = new HashSet<>();

    deque.offer(start);
    visited.add(start);

    while (!deque.isEmpty()) {
        Node cur = deque.poll();
        System.out.println(cur.value);

        for (Node neighbor : cur.neighbors) { 
            if (!visited.contains(neighbor)) {
                visited.add(neighbor);
                deque.offer(neighbor);
            }
        }
    }
}
```
