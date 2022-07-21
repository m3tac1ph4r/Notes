# BSF(Breadth First Search) Traversal {level order traversal}

**Problem Statement**

You are given an undirected and disconnected graph G(V, E) having V vertices numbered from 0 to V-1 and E edges. Your task is to print its BFS traversal starting from the 0th vertex.
BFS or Breadth-First Traversal of a graph is an algorithm used to visit all of the nodes of a given graph. In this traversal algorithm, one node is selected, and then all of the adjacent nodes are visited one by one.
An undirected graph is a graph where all the edges are bidirectional, i.e., they point from source to destination and destination to source.
A graph is disconnected if at least two vertices of the graph are not connected by a path.

**Example 1 :**
**INPUT :**

```
4 4
0 1
0 3
1 2
2 3
```

**OUTPUT :**

```
0 1 3 2
```

![[BSF_EX1.png]]

**Example 2:**
**Input :**
![[BSF_EX2.png]]

**OUTPUT :**

```
Starting from 0, it is connected to 1 and 3, which will be printed. The remaining node is 2, which will be printed at the end.
```

### Approach (Queue) :

1. Start for loop from 0 to n check node i should not be visited
2. Add node in the queue
3. mark it visited pop the element and add all adjacency neighbour in the queue if not visited and mark all the neighbours visited
4. Add element in the answer vector

-> We need to have this before proceeding :

1.  Queue Data structure
2.  Visited Array – An array with all values initialised with 0**.**

-> We will start a for loop to do BFS traversal for every node , so that every node will be visited
-> We will push the 1st node into the queue data structure and mark it as visited. After this, we will find its adjacent nodes. If we get some unvisited node, we will simply push this adjacent node into the queue data structure

-> Now since the work of the 1st node is done, we will pop out this node from the queue. Now, this process goes on until the queue is not empty.

![[BSF_appraoch1.png]]
![[BSF_appraoch2.png]]

```cpp
void makeAdjList(unordered_map<int, list<int>> &adj, vector<pair<int, int>> &edges)
{
    for (int i = 0; i < edges.size(); i++)
    {
        int u = edges[i].first;
        int v = edges[i].second;

        adj[u].push_back(v);
        adj[v].push_back(u);
    }
}
vector<int> BFS(int vertex, vector<pair<int, int>> edges)
{
    unordered_map<int, list<int>> adj;
    makeAdjList(adj, edges);

    vector<int> visited(vertex, 0);
    vector<int> ans;
    // this is when you are getting TLE
    // for (int i = 0; i < vertex; i++)
    //     adj[i].sort();
    for (int i = 0; i < vertex; i++)
    {
        if (!visited[i])
        {
            queue<int> q;
            q.push(i);
            visited[i] = 1;
            while (!q.empty())
            {
                int node = q.front();
                ans.push_back(node);
                q.pop();
                for (auto j : adj[node])
                {
                    if (!visited[j])
                    {
                        q.push(j);
                        visited[j] = 1;
                    }
                }
            }
        }
    }
    return ans;
}
```

> **Time Complexity :** O(N+E)
> N = Nodes , E = travelling through adjacent nodes
> **Space Complexity :** O(N+E) + O(N) + O(N) 
> Space for adjacency list, visited array, queue data structure

### Question :

https://www.codingninjas.com/codestudio/problems/bfs-in-graph_973002

### Reference :

https://takeuforward.org/data-structure/breadth-first-searchbfs-level-order-traversal/
https://youtu.be/b5kij1Akf9I?list=PLDzeHZWIZsTobi35C3I-tKB3tRDX6YxuA
