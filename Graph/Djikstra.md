# DJIKSTRA ALGORITHM
````java

public class Dijkstra {
    static class Edge {
        int node, weight;
        Edge(int node, int weight) {
            this.node = node;
            this.weight = weight;
        }
    }

    public static int[] dijkstra(int n, List<List<Edge>> graph, int start) {
        int[] dist = new int[n + 1]; // Use n for 0-indexed, n+1 for 1-indexed
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[start] = 0;

        PriorityQueue<Edge> pq = new PriorityQueue<>((a, b) -> a.weight - b.weight);
        pq.offer(new Edge(start, 0));

        while (!pq.isEmpty()) {
            Edge curr = pq.poll();
            int u = curr.node;
            int d = curr.weight;

            if (d > dist[u]) continue;

            for (Edge neighbor : graph.get(u)) {
                int v = neighbor.node;
                int w = neighbor.weight;

                if (dist[v] > dist[u] + w) {
                    dist[v] = dist[u] + w;
                    pq.offer(new Edge(v, dist[v]));
                }
            }
        }

        return dist; // dist[i] gives shortest distance from start to node i
    }
}


