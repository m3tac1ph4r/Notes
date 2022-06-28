# Topological Sort DFS

>**A directed acyclic graph (DAG) G has at least one vertex with the indegree zero and one vertex with the out-degree zero.**


A Directed Acyclic Graph (DAG) is a directed graph that contains no cycles.

Topological Sorting of DAG is a linear ordering of vertices such that for every directed edge from vertex ‘u’ to vertex ‘v’, vertex ‘u’ comes before ‘v’ in the ordering. Topological Sorting for a graph is not possible if the graph is not a DAG.

![[topo_dfs_ex.png]]

**For every u->v , u always appear before v in topological sorting**

### Approach (DFS) :

1. We will use one additional data structure i.e **stack** in this.
2. Firstly we will create the adjacency list. 
3. Then traverse 0 to v. And mark visited[i] and call recursive function for adjacent neighbour.  When there is no neighbour for node i. Then add that node in the stack before recursion call ends

![[topoSOrt_dfs_approach.png]]

```C++
void topoSort(int node, vector<bool> &visited, stack<int> &s, unordered_map<int, list<int>> &adj)
{
    visited[node] = true;
    for (auto it : adj[node])
    {
        if (!visited[it])
            topoSort(it, visited, s, adj);
    }
    s.push(node);
}
vector<int> topologicalSort(vector<vector<int>> &edges, int v, int e)
{
    // Write your code here
    unordered_map<int, list<int>> adj;
    for (int i = 0; i < edges.size(); i++)
    {
        int u = edges[i][0];
        int v = edges[i][1];
        adj[u].push_back(v);
    }
    vector<int> ans;
    vector<bool> visited(v, false);
    stack<int> s;
    for (int i = 0; i < v; i++)
    {
        if (!visited[i])
            topoSort(i, visited, s, adj);
    }
    while (!s.empty())
    {
        ans.push_back(s.top());
        s.pop();
    }
    return ans;
}
```




### Question :
https://www.codingninjas.com/codestudio/problems/982938

### Reference :

https://youtu.be/T_boOrr0rvk?list=PLDzeHZWIZsTobi35C3I-tKB3tRDX6YxuA