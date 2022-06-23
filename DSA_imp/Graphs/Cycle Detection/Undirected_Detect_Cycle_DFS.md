# Check cycle in undirected graph using DFS

1. We will start a for loop from 1 to N vertex
2. Then check if i is not visited then call DfsIsCyclic() for i node
3. In DfsisCyclic()
	1. Mark node as visited and find all adjacent neighbours
	2. Then call recursive function DfsIsCyclic() for them
	3. Now node *it* is visited and equal to parent of front_node mean front_node came from *it* node.
	4. Else if *it* is visited and not equal to parent means another node visited *it*, means there is **cycle**

### Approach (Recursion) ;


![[undirected_detect_cycle_DFS.png]]


```C++
bool DfsIsCyclic(int node, int parent, vector<bool> &visited, unordered_map<int, list<int>> &adj)
{
    visited[node] = true;
    for (auto it : adj[node])
    {
        if (!visited[it])
        {
            visited[it] = true;
            bool ans = DfsIsCyclic(it, node, visited, adj);
            if (ans == true)
                return true;
        }
        else if (visited[it] == true and it != parent)
            return true;
    }
    return false;
}
string cycleDetection(vector<vector<int>> &edges, int n, int m)
{
    // create an adjacency list
    unordered_map<int, list<int>> adj;
    for (int i = 0; i < m; i++)
    {
        int u = edges[i][0];
        int v = edges[i][1];

        adj[u].push_back(v);
        adj[v].push_back(u);
    }
    vector<bool> visited(n, false);
    for (int i = 0; i < n; i++)
    {
        if (!visited[i])
        {
            bool ans = DfsIsCyclic(i, -1, visited, adj);
            if (ans == true)
                return "Yes";
        }
    }
    return "No";
}
```

### Question :

https://www.codingninjas.com/codestudio/problems/1062670


### Reference :

https://youtu.be/1cSzxlhxOw8?list=PLDzeHZWIZsTobi35C3I-tKB3tRDX6YxuA
https://youtu.be/Y9NFqI6Pzd4?list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw