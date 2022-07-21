# Shortest Path in Directed Acyclic Graph(DAG)

#shortestPath_graph

What do we mean by the Shortest Path in a directed acyclic graph?

Well, it’s a trivial question, but still, for the sake of clarity, we’ll define that let

**G = (V, E)** be a directed graph with **E** edges and **V** vertices.

Let **T** be the shortest path between any 2 vertices in the graph such that there is no other path in the graph between any 2 vertices whose sum of edge weights is less than **T’**s sum of edge weights.

**NOTE**: shortest path between 2 vertices is defined only when the vertices are in the same graph, i.e., the graph should not be disconnected.

![[shortest_path_DAG_ex1.png]]

### Approach :

> **Why we are using Topological Sort ?**
> Topological sort ensures that we are picking up nodes that come first while travelling from the source, this, in turn, will ensure that every node will have at least one condition that it can be reached from the source.
> Topological sort ensures that we are picking up nodes that come first while travelling from the source, this, in turn, will ensure that every node will have at least one condition that it can be reached from the source. As we are setting dist[src] = 0, it will start from there, the condition dis[node] != infinity will not let any node other than src enter that condition first. Because of topological sort nodes coming before src will be discarded.

1. Firstly we will find toposort of the graph
2. Then create a distance array with value _INT_MAX_ and mark _dist[src]=0_
3. From toposort we will have a stack. Pop the top element from stack and check if _dist[top_node]!=INT_MAX_
4. Then start a for loop for top_node neighbours and find the minimum distance from top_node to their neighbours
   1. _dist[neighbour]=min(dist[neighbour],dist[top_node]+dist[top_node_to_neighbour])_

![[shortest_distance_DAG_approach.png]]

```cpp

void findTopoSort(int node, vector<bool> &visited, stack<int> &st, vector<pair<int, int>> adj[])
{
    visited[node] = true;
    for (auto it : adj[node])
    {
        if (!visited[it.first])
            findTopoSort(it.first, visited, st, adj);
    }

    st.push(node);
}
void shortestPath(int src, int N, vector<pair<int, int>> adj[])
{
    stack<int> st;
    vector<bool> visited(N, false);
    for (int i = 0; i < N; i++)
    {
        if (!visited[i])
            findTopoSort(i, visited, st, adj);
    }
    vector<int> dist(N, INT_MAX);
    dist[src] = 0;

    while (!st.empty())
    {
        int top_node = st.top();
        st.pop();
        if (dist[top_node] != INT_MAX)
        {
            for (auto it : adj[top_node])
            {
                dist[it.first] = min(dist[top_node] + it.second, dist[it.first]);
            }
        }
    }
    for (auto i : dist)
    {
        (i == INT_MAX) ? cout << "INF " : cout << i << " ";
    }
}

int main()
{
    int n, m;
    cin >> n >> m;
    vector<pair<int, int>> adj[n];
    for (int i = 0; i < m; i++)
    {
        int u, v, wt;
        cin >> u >> v >> wt;
        adj[u].push_back({v, wt});
    }

    shortestPath(0, n, adj);

    return 0;
}
```

### Reference :

https://youtu.be/CrxG4WJotgg?list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw
