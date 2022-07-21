# Detect Cycle in Directed graph using BFS

> **Application of Kahn's Algorithm**

1. If **number of vertex == number of elements in the array**
   then it means **No Cycle Present**
2. If **number of vertex != number of elements in the array**
   then it means **Cycle Present**

You are given a directed graph having ‘N’ nodes. A matrix ‘EDGES’ of size M x 2 is given which represents the ‘M’ edges such that there is an edge directed from node EDGES[i][0] to node EDGES[i][1].

Find whether the graph contains a cycle or not, return true if a cycle is present in the given directed graph else return false.

```cpp
bool topoSort(int V, vector<int> adj[])
{

    vector<int> indegree(V, 0);
    for (int i = 0; i < V; i++)
    {
        for (auto it : adj[i])
            indegree[it]++;
    }

    queue<int> q;
    int count = 0;
    for (int i = 0; i < V; i++)
    {
        if (indegree[i] == 0)
            q.push(i);
    }

    while (!q.empty())
    {
        int front = q.front();
        q.pop();
        count++;
        for (auto it : adj[front])
        {
            indegree[it]--;
            if (indegree[it] == 0)
                q.push(it);
        }
    }
    if (count == V)
        return false;
    else
        return true;
}
```

### Question :

https://www.codingninjas.com/codestudio/problems/1062626

### Reference :

https://youtu.be/X2_tYUuthH8?list=PLDzeHZWIZsTobi35C3I-tKB3tRDX6YxuA
