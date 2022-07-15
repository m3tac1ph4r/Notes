# Kosaraju Algorithm(Strongly Connected Component)
#algorithm #graphAlgo 


**Kosaraju's Algorithm is used to find the strongly connected component**
> **What is Strongly Connected Component (SCC) ?**
>  A strongly connected component is the portion of a directed graph in which there is a path from each vertex to another vertex. **It is applicable only on** directed graph.
>  So if you start from node x. And starting from node x you visit some node and came back to starting node x. Means that is *Strongly Connected Component*



**Example 1:**

![[SCC1.png]]

As you can see in the above graph. 
1. If you start  from 0 , 0 ->2->1->0. You came back to the starting node so. So this is the *first SCC*.  And if you go 0->2->3->4 . Now 4 doesn't have any neighbour. You cannot go back to starting from node4. So this is not SCC
2. And if you start from 2->3->4. Same you cannot go back to starting node. So this is *not the SCC*
3. If you start from 3. 3->4. Same cannot go back to starting node so this is *not the SCC*
4. So node 3 is the *second SCC*
5. And node 4 is the *third SCC*

**Example 2:**

![[SCC2.png]]

1. If you start from 1. 1->4->0->1. This is the *first SCC*
2. If you start from 2. 2->3->2. This is the *second SCC*


### Approach :

1. Find the **adjacency list.**
2. Then find the **topologicalSort using DFS**. And from there you will get the stack which will have toposort vertices.
3. Then **transpose the graph** i.e change the direction of edges. u -> v changed to v -> u
4. Then do **DFS of transpose graph** using topoSort stack.

![[Kosaraju_approach.png]]

```C++

void topoSort(int node, unordered_map<int, list<int>> &adj, unordered_map<int, bool> &visited, stack<int> &st)
{
    visited[node] = true;
    for (auto it : adj[node])
    {
        if (!visited[it])
            topoSort(it, adj, visited, st);
    }
    st.push(node);
}
void dfs(int node, unordered_map<int, bool> &visited, unordered_map<int, list<int>> &transpose)
{
    visited[node] = true;
    for (auto it : transpose[node])
    {
        if (!visited[it])
        {
            dfs(it, visited, transpose);
        }
    }
}
int stronglyConnectedComponents(int v, vector<vector<int>> &edges)
{
    // base case if there is no edge means only one component
    if (v == 1)
        return 1;

    // create adjacency list
    unordered_map<int, list<int>> adj;
    for (int i = 0; i < edges.size(); i++)
    {
        int u = edges[i][0];
        int v = edges[i][1];
        adj[u].push_back(v);
    }

    // find topologicalSort
    stack<int> st;
    unordered_map<int, bool> visited;
    for (int i = 0; i < v; i++)
    {
        if (!visited[i])
            topoSort(i, adj, visited, st);
    }

    // find transpose of graph i.e reverse all the edges of graph {v->u}
    int count = 0;
    unordered_map<int, list<int>> transpose;
    for (int i = 0; i < v; i++)
    {
        visited[i] = false;
        for (auto it : adj[i])
            transpose[it].push_back(i);
    }

    // dfs of transpose graph
    while (!st.empty())
    {
        int top = st.top();
        st.pop();
        if (!visited[top])
        {
            count++;
            dfs(top, visited, transpose);
        }
    }
    return count;
}
```

### Question :

https://www.codingninjas.com/codestudio/problems/count-strongly-connected-components-kosaraju-s-algorithm_1171151

https://www.codingninjas.com/codestudio/problems/985311

### References :
https://youtu.be/ndfjV_yHpgQ