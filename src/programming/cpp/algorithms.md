### A Basic Dijkstra's Algorithm Using a Brute Force Approach

```cpp
// C++ program for Dijkstra single source shortest path algorithm.
// source : https://www.geeksforgeeks.org/dijkstras-shortest-path-algorithm-greedy-algo-7/

#include <iostream>
#include <limits.h>
using namespace std;

const int V = 9;

int minDistance(int dist[], bool sptset[]) {
    int min = INT_MAX, min_index;

    for (int v = 0; v < V; ++v)
        if (sptset[v] == false && dist[v] <= min)
            min = dist[v], min_index = v;

    return min_index;
}

void printSolution(int dist[]) {
    cout << "Vertex \t Distance from Source\n";
    for (int i = 0; i < V; ++i)
        cout << i << "\t\t\t" << dist[i] << "\n";
}

void dijkstra(int graph[V][V], int src) {
    int dist[V];
    bool sptset[V];

    for (int i = 0; i < V; ++i)
        dist[i] = INT_MAX, sptset[i] = false;

    dist[src] = 0;

    for (int count = 0; count < V - 1; ++count) {
        int u = minDistance(dist, sptset);

        sptset[u] = true;

        for (int v = 0; v < V; ++v)
            if (!sptset[v] && graph[u][v]
                && dist[u] != INT_MAX
                && dist[u] + graph[u][v] < dist[v])
                dist[v] = dist[u] + graph[u][v];
    }

    printSolution(dist);
}

int main() {
    int graph[V][V] = { { 0, 4, 0, 0, 0, 0, 0, 8, 0 },
                        { 4, 0, 8, 0, 0, 0, 0, 11, 0 },
                        { 0, 8, 0, 7, 0, 4, 0, 0, 2 },
                        { 0, 0, 7, 0, 9, 14, 0, 0, 0 },
                        { 0, 0, 0, 9, 0, 10, 0, 0, 0 },
                        { 0, 0, 4, 14, 10, 0, 2, 0, 0 },
                        { 0, 0, 0, 0, 0, 2, 0, 1, 6 },
                        { 8, 11, 0, 0, 0, 0, 1, 0, 7 },
                        { 0, 0, 2, 0, 0, 0, 6, 7, 0 } };
    
    dijkstra(graph, 0);

    return 0;
}
```