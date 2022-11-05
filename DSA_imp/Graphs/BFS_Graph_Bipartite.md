# Graph Bipartite using BFS

A graph is **bipartite** if the nodes can be partitioned into two independent sets `A` and `B` such that **every** edge in the graph connects a node in set `A` and a node in set `B`.
Return `true` *if and only if it is* **bipartite**\_.

**Example 1:**
![[bipartile_ex1.png]]

**Input:** graph = [ [1,2,3],[0,2],[0,1,3],[0,2]]
**Output:** false

**Example 2:**
![[bfs_bipartile_ex2.png]]

**Input:** graph = [ [1,3],[0,2],[1,3],[0,2]]
**Output:** true

### Approach :

![[graph_bipartile_bfs_app.png]]
**Node 2 will have the color=0**

1. Make adjacency list
2. Then create a vector< int > with default value -1 to store the color 0,1
3. We will use queue to store the adjacent neighbours of node.
4. Then store node in the queue and color_0 . Then give opposite color to their adjacent nodes.
5. If color there is a cylcle and color matches then return false

```cpp
bool isBipartite(vector<vector<int>> &graph)
{
    queue<int> q;
    unordered_map<int, list<int>> adj;
    vector<int> color(graph.size(), -1);
    for (int i = 0; i < graph.size(); i++)
    {
        for (auto it : graph[i])
        {
            adj[i].push_back(it);
        }
    }

    for (int i = 0; i < graph.size(); i++)
    {
        if (color[i] == -1)
        {
            q.push(i);
            color[i] = 1;
            while (!q.empty())
            {
                int front = q.front();
                q.pop();
                int front_color = color[front];
                for (auto it : adj[front])
                {
                    if (color[it] == -1)
                    {
                        color[it] = !(front_color);
                        q.push(it);
                    }
                    else if (color[it] == front_color)
                        return false;
                }
            }
        }
    }
    return true;
}
```

### Question :

https://leetcode.com/problems/is-graph-bipartite/

### Reference :

https://youtu.be/nbgaEu-pvkU?list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw

### Application of Bipartile Graph :

https://leetcode.com/problems/possible-bipartition/
