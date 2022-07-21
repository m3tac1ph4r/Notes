# Detect Cycle in undirected graph using BFS

**Intuition:** The intuition behind this is to check for the visited element if it is found again, this means the cycle is present in the given undirected graph.

<pre>
for(i= 1->N)

{

if(!vis[i]) 

  if(cyclebfs(i)) // if cycle is found , we return true

                   Return True; 
}
</pre>

![[un_cycle_detect_BFS.png]]

### Approach (Queue) :

![[undirected_detect_cycle_BFS.png]]

```cpp
bool check_cycle(int node, vector<bool> &visited, unordered_map<int, list<int>> &adj, unordered_map<int, int> parent)
{
    queue<int> q;
    visited[node] = true;
    parent[node] = -1; // because root does't have parent
    q.push(node);

    while (!q.empty())
    {
        int front_node = q.front();

        q.pop();

        for (auto it : adj[front_node])
        {
            if (!visited[it])
            {
                visited[it] = true;
                q.push(it);
                parent[it] = front_node;
            }

            else if (visited[it] == true and it != parent[front_node]) // means neighbour of it is already visited by another node
                return true;
        }
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
    unordered_map<int, int> parent;
    vector<bool> visited(n, false);
    for (int i = 0; i < n; i++)
    {
        if (!visited[i])
        {
            bool ans = check_cycle(i, visited, adj, parent);
            if (ans == true)
                return "Yes";
        }
    }
    return "No";
}
```

> **Time Complexity :** O(N+E)
> **Space Complexity :** O(N+E) + O(N) + O(N)

### Question :

https://www.codingninjas.com/codestudio/problems/1062670

### Reference :

https://youtu.be/1cSzxlhxOw8?list=PLDzeHZWIZsTobi35C3I-tKB3tRDX6YxuA
https://youtu.be/A8ko93TyOns?list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw
