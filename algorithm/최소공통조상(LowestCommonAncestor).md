### 최소공통조상(LCA)란?
- 최소 공통 조상은 트리 구조에서 임의의 두 정점이 갖는 가장 가까운 조상 정점을 의미한다.

### 예시
| 노드 | 부모 | 깊이 (루트=1) | 비고 |
| :---: | :---: |:---------:| :---: |
| 1 | - |     0     | 루트 |
| 2 | 1 |     1     | |
| 3 | 1 |     1     | |
| 4 | 2 |     2     | |
| 5 | 2 |     2     | |
| 6 | 3 |     2     | |
| 7 | 4 |     3     | |
| 8 | 4 |     3     | |
- LCA(7,8) = 4
- LCA(7,5) = 2

### 알고리즘
1. 모든 노드에 대한 깊이를 계산
2. 최소 공통 조상을 찾을 두 노드를 확인
3. 먼저 두 노드의 깊이가 동일하도록 거슬러 올라감
4. 부모가 같아질 때 까지 반복적으로 두 노드의 부모 방향으로 거슬러 올라감
5. 모든 LCA(a,b) 연산에 대하여 3~4번의 과정을 반복.

### 알고리즘
```java
/* 깊이를 저장하고, 윗부모와 연결하는 메소드
 * @param node : 현재 노드
 * @param depth : 깊이
 */
public void dfs(int node, int d) {
    visit[node] = true;
    depth[node] = d;
    for (int next : tree[node]) {
        if (visit[next]) {
            continue;
        }
        parent[next] = node;
        dfs(next, d + 1);
    }
}

public int lca(int a, int b){
    if(depth[a]<depth[b]){
        int temp = a;
        a = b;
        b = temp;
    }
    while(depth[a]!=depth[b]){
        a = parent[a];
    }
    while(a!=b){
        a = parent[a];
        b = parent[b];
    }
    return a;
}
```
