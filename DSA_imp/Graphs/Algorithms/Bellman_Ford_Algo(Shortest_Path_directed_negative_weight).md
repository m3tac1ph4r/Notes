# Bellman Ford Algorithm (Shortest Path in graphs having negative weights)

#algorithm #graphAlgo #shortestPath_graph

**Bellman Ford works for :**

1. Directed Graph
   1. Negative weights
   2. Positive weights
2. Undirected Graph - You have to convert undirected to directed using bidirectional edges.

**Condition for Bellman Ford to work :** There should not be a negative cycle in graph

![[bellman_ford_negative_cycle.png]]

> **Bellman Ford Algo is used to find the shortest path in graph and also finds the negative cycle in graph**

### Approach :

1. Create a distance array of size N with default value 1e9. Mark distance[src]=0

2. Then ignore all the nodes before source. Then update the distance of node[v] in u->v edges.

3. Do STEP 2 n-1 times. Because suppose we have n vertices and in each iteration only one edge is updated then we need total n-1 iteration to get shortest path from source.

> **How to check CYCLE is PRESENT OR NOT ?**
> After n-1 iteration we will have shortest distance. But we will do one more iteration after (n-1). In that extra iteration if any node update it's shortest distance then we can say that **CYCLE IS PRESENT** else **NOT**

```cpp

int bellmonFord(int n, int m, int src, int dest, vector<vector<int>> &edges)
{
    // Write your code here.
    vector<int> distance(n + 1, 1e9);
    distance[src] = 0;
    for (int j = 1; j <= n; j++)
    {
        for (int i = 0; i < m; i++)
        {
            int u = edges[i][0];
            int v = edges[i][1];
            int w = edges[i][2];

            if (distance[u] == 1e9)
                continue;
            else if (distance[u] + w < distance[v])
                distance[v] = distance[u] + w;
        }
    }
    for (int i = 0; i < edges.size(); i++)
    {
        int u = edges[i][0];
        int v = edges[i][1];
        int w = edges[i][2];

        if (distance[u] == 1e9)
            continue;
        else if (distance[u] + w < distance[v])
            return 1e9;
    }
    return distance[dest];
}
```

### Question :

https://www.codingninjas.com/codestudio/problems/2041977

### Reference :

https://youtu.be/ijpVpsmpJtQ?list=PLDzeHZWIZsTobi35C3I-tKB3tRDX6YxuA
