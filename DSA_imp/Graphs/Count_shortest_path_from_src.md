# Count Shortest Path and Distance From Source for all nodes
#shortestPath_graph


>**Using Dijkastra Algorithm**

Given a [weighted undirected graph](https://www.geeksforgeeks.org/graph-and-its-representations/) [](https://www.geeksforgeeks.org/graph-data-structure-and-algorithms/)**G** and an integer **S**, the task is to print the distances of the shortest paths and the count of the [number of the shortest paths](https://www.geeksforgeeks.org/number-shortest-paths-unweighted-directed-graph/) for each node from a given vertex, **S.**

![[count_shortest_path_example.png]]


### Approach :

```C++

vector<int> countShortestDistance(vector<vector<int>> edges, int n, int m, int src)
{
    unordered_map<int, list<pair<int, int>>> adj;
    for (int i = 0; i < m; i++)
    {
        int u = edges[i][0];
        int v = edges[i][1];
        int w = edges[i][2];
        adj[u].push_back({v, w});
        adj[v].push_back({u, w});
    }

    vector<int> distance(n + 1, INT_MAX);
    vector<int> path(n + 1, 0);

    set<pair<int, int>> st;
    st.insert({0, 1});
    distance[1] = 0;
    path[1] = 1;

    while (!st.empty())
    {
        auto top = *(st.begin());
        st.erase(st.begin());
        int u = top.second;
        for (auto nbr : adj[u])
        {
            int v = nbr.first;
            int wt = nbr.second;
            if (distance[v] > distance[u] + wt)
            {
                auto findNode = st.find({distance[v], v});
                if (findNode != st.end())
                    st.erase(findNode);

                distance[v] = distance[u] + wt;
                path[v] = path[u];
                st.insert({distance[v], v});
            }
            else if (distance[v] == distance[u] + wt)
            {
                path[v] = path[u] + path[v];
            }
        }
    }
    return distance;
}
```



> _**Time Complexity:** O(N * log(M))_    
_**Auxiliary Space:** O(N)_


### Reference :
https://www.geeksforgeeks.org/number-of-shortest-paths-in-an-undirected-weighted-graph/