# DFS(Depth-First-Search) Traversal

**Depth First Traversal** is a traversal technique/algorithm, used to traverse through all the nodes in the given graph.

It starts traversal through any one of its neighbour nodes and explores the farthest possible node in each path/branch and then starts Back-tracking.

Backtracking happens when the DFS algorithm reaches a particular node that has no neighbours to visit further, once it reaches that node with no neighbours to be visited it’ll backtrack to its previous node (say N) and from this node N algorithm will start searching for unvisited neighbour nodes and starts visiting them.

---

**Problem Statement:** Given a graph, traverse through all the nodes in the graph using **Depth First Search**.

**Example 1:**

![[DFS_ex1.png]]
**Output:** 0 1 2 3
**Explanation**:
0 is connected to 1 , 3.
1 is connected to 2.
2 is connected to 1.
3 is connected to 0.
so starting from 0, it will go to 1 then 2
then back to 0 then 0 to 3
thus dfs will be 0 1 2 3.

**Example1:**
![[DFS_traversal_ex2.png]]

**Output:** 2 4 1 3 5

**Explanation:** Note: For above I/P we started DFS from Node 2,We can start from any node.

### Approach (Recursion) :

- In DFS we only choose one adjacent neighbour. And proceed further.
  ![[DFS_app1.png]]

```cpp
void dfs(int node, unordered_map<int, list<int>> &adj, vector<int> &visited, vector<int> &component)
{
    component.push_back(node);
    visited[node] = 1;
    for (auto i : adj[node])
    {
        if (!visited[i])
            dfs(i, adj, visited, component);
    }
}
vector<vector<int>> depthFirstSearch(int V, int E, vector<vector<int>> &edges)
{
    unordered_map<int, list<int>> adj;
    vector<int> visited(V + 1, 0);

    vector<vector<int>> ans;
    for (int i = 0; i < edges.size(); i++)
    {
        int u = edges[i][0];
        int v = edges[i][1];
        adj[u].push_back(v);
        adj[v].push_back(u);
    }
    for (int i = 0; i < V; i++)
    {
        if (!visited[i])
        {
            vector<int> component;
            dfs(i, adj, visited, component);
            ans.push_back(component);
        }
    }
    return ans;
}
```

> **Time Complexity :** O(N+E), Where N is the time taken for visiting N nodes and E is for travelling through adjacent nodes.
> **Space Complexity :** O(N+E)+O(N)+O(N) , Space for adjacency list, Array,Auxiliary space.

### Question :

https://practice.geeksforgeeks.org/problems/depth-first-traversal-for-a-graph/1
https://www.codingninjas.com/codestudio/problems/dfs-traversal_630462

### Reference :

https://youtu.be/aJa3U-hydXc?list=PLDzeHZWIZsTobi35C3I-tKB3tRDX6YxuA
