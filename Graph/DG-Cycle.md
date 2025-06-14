### 🚀 Cycle detection in Directed Graph

``` java

static boolean dfs(Map<Integer, List<Integer>> map, int u, Map<Integer, Boolean> currentDfs, Map<Integer, Boolean> visited){
        visited.put(u, true);
        currentDfs.put(u, true);

        for(int v: map.getOrDefault(u, new ArrayList<>())){
            if(!visited.containsKey(v)){
                boolean result = dfs(map, v, currentDfs, visited);
                if(result) return true;
            } else if (currentDfs.containsKey(v)){
                return true;
            }
        }

        currentDfs.remove(u);
        return false;
    }
