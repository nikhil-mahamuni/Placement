# Topological Sort valid only for directed acyclic graph

```java

 public static ArrayList<Integer> topologicalSort(ArrayList<ArrayList<Integer>> edges, int v, int e) 
    {
        // Write your code here
        Map<Integer, List<Integer>> map = new HashMap<>();
        for(int i = 0; i < e; i++){
            int src = edges.get(i).get(0);
            int dest = edges.get(i).get(1);

            map.putIfAbsent(src, new ArrayList<>());
            map.get(src).add(dest);
        }

        boolean[] visited = new boolean[v+1];
        Deque<Integer> stack = new ArrayDeque<>();

        for (int i = 0; i < v; i++) {
            if (!visited[i]) {
                func(map, i, visited, stack);
            }
        }
        
        ArrayList<Integer> ans = new ArrayList<>();
        while(!stack.isEmpty()) ans.add(stack.pop());

        return ans;
    }

    static void func(Map<Integer, List<Integer>> map, int u, boolean[] visited, Deque<Integer> stack){
        visited[u] = true;

        for(int v: map.getOrDefault(u, new ArrayList<>())){
            if(!visited[v]){
                func(map, v, visited, stack);
            }
        }

        stack.push(u);
    }
