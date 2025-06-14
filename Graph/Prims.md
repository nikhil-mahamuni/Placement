### Prims Algo

```java

import java.util.*;
import java.io.*;

public class Solution {

    static class Node {
        int vertex, weight;
        Node(int vertex, int weight) {
            this.vertex = vertex;
            this.weight = weight;
        }
    }

    public static int primsMST(ArrayList<ArrayList<Integer>> vec, int vertices, int edges) {
        // Step 1: Build adjacency list
        Map<Integer, List<Node>> map = new HashMap<>();
        for (int i = 0; i < edges; i++) {
            int u = vec.get(i).get(0);
            int v = vec.get(i).get(1);
            int w = vec.get(i).get(2);

            map.putIfAbsent(u, new ArrayList<>());
            map.putIfAbsent(v, new ArrayList<>());

            map.get(u).add(new Node(v, w));
            map.get(v).add(new Node(u, w)); // Since it's undirected
        }

        // Step 2: Min-heap (weight, vertex)
        PriorityQueue<Node> pq = new PriorityQueue<>((a, b) -> Integer.compare(a.weight, b.weight));
        boolean[] visited = new boolean[vertices];
        pq.offer(new Node(0, 0)); // Start from node 0

        int mstWeight = 0;

        while (!pq.isEmpty()) {
            Node curr = pq.poll();
            int u = curr.vertex;
            int w = curr.weight;

            if (visited[u]) continue;

            visited[u] = true;
            mstWeight += w;

            for (Node neighbor : map.getOrDefault(u, new ArrayList<>())) {
                if (!visited[neighbor.vertex]) {
                    pq.offer(new Node(neighbor.vertex, neighbor.weight));
                }
            }
        }

        return mstWeight;
    }
}
