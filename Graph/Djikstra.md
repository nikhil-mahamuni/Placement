### DIJKSTRA 

```java

import java.util.*;

public class Solution {

    static class Node {
        int vertex;
        int weight;

        Node(int vertex, int weight) {
            this.vertex = vertex;
            this.weight = weight;
        }
    }

    public static ArrayList<Integer> dijkstra(ArrayList<ArrayList<Integer>> edges, int vertices, int edgeCount, int source) {
        // Build adjacency map
        Map<Integer, List<Node>> graph = new HashMap<>();
        for (int i = 0; i < edgeCount; i++) {
            int u = edges.get(i).get(0);
            int v = edges.get(i).get(1);
            int w = edges.get(i).get(2);

            graph.putIfAbsent(u, new ArrayList<>());
            graph.putIfAbsent(v, new ArrayList<>());

            graph.get(u).add(new Node(v, w));
            graph.get(v).add(new Node(u, w)); // Undirected graph
        }

        // Distance array
        int[] dist = new int[vertices];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[source] = 0;

        // Min-heap to get the node with the smallest distance
        PriorityQueue<Node> pq = new PriorityQueue<>((a, b) -> Integer.compare(a.weight, b.weight));
        pq.offer(new Node(source, 0));

        while (!pq.isEmpty()) {
            Node current = pq.poll();
            int u = current.vertex;
            int currentDist = current.weight;

            // Skip if we already found a better path
            if (currentDist > dist[u]) continue;

            for (Node neighbor : graph.getOrDefault(u, new ArrayList<>())) {
                int v = neighbor.vertex;
                int weight = neighbor.weight;

                if (dist[v] > dist[u] + weight) {
                    dist[v] = dist[u] + weight;
                    pq.offer(new Node(v, dist[v]));
                }
            }
        }

        // Convert dist[] to ArrayList<Integer>
        ArrayList<Integer> result = new ArrayList<>();
        for (int d : dist) result.add(d);

        return result;
    }
}
