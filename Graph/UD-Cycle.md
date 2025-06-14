### 🚀 BFS Cycle Detection

```java
static boolean bfs(Map<Integer, List<Integer>> map, boolean[] visited, int u) {
    
    Deque<Integer> queue = new ArrayDeque<>();
    Map<Integer, Integer> parent = new HashMap<>();

    queue.offer(u);
    visited[u] = true;        // Mark source as visited
    parent.put(u, -1);        // Source node has no parent

    while (!queue.isEmpty()) {
        int curr = queue.poll();

        // Traverse all adjacent nodes of current node
        for (int v : map.getOrDefault(curr, new ArrayList<>())) {
            
            if (!visited[v]) {
                visited[v] = true;     // Mark as visited before enqueuing
                parent.put(v, curr);   // Set parent
                queue.offer(v);
            } 
            // If already visited and not coming from parent, it's a cycle
            else if (parent.get(curr) != v) {
                return true;
            }
        }
    }

    return false;  // No cycle found in this component
}



## 🚀 DFS Cycle Detection

static boolean dfs(Map<Integer, List<Integer>> map, int u, int parent, boolean[] visited){
        visited[u] = true;

        for(int v: map.getOrDefault(u, new ArrayList<>())){
            if(!visited[v]){
                boolean isCycle = dfs(map, v, u, visited);
                if(isCycle) return true;
            } else if (parent != v){
                return true;
            }
        }

        return false;
    }
