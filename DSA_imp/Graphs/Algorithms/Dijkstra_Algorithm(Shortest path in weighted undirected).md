# Dijkstra Algorithm (Shortest Path in undirected weighted graph)

#algorithm #graphAlgo #shortestPath_graph

**This algorithm does not works for negative weights.**

> **What does Dijkstra Algorithm finds ?**
> Dijkstra Algorithm finds shortest path in directed and undirected graph having weights

### Approach :

![[dijkstra_approach.png]]

1. We would be using set(sorted) and a distance array of size N initialized with infinity (indicating that at present none of the nodes are reachable from the source node) and initialize the distance to source node as 0.
2. We push the source node to the set
3. For every node at the top of the set we pop that element out and look out for its adjacent nodes. If the current reachable distance is better than the previous distance indicated by the distance array, we update the distance and push it in the queue. And check if entry for the node is already there in the set or not. If YES then delete that entry and push the updated one
4. A node with a lower distance would be at the top of the set as opposed to a node with a higher distance. By following the steps 3, until our set becomes empty, we would get the minimum distance from the source node to all other nodes. Here’s a quick demonstration of the same.

```cpp
vector<int> dijkstra(vector<vector<int>> &vec, int vertices, int edges, int source)
{
    unordered_map<int, list<pair<int, int>>> adj; // in pair first int will be for vertex and second is for weight

    for (int i = 0; i < edges; i++)
    {
        int u = vec[i][0];
        int v = vec[i][1];
        int weight = vec[i][2];

        adj[u].push_back(make_pair(v, weight));
        adj[v].push_back(make_pair(u, weight));
    }

    vector<int> distance(vertices, INT_MAX);

    distance[source] = 0;

    set<pair<int, int>> st;
    st.insert(make_pair(0, source));

    while (!st.empty())
    {
        auto top = *(st.begin());
        st.erase(st.begin());

        int nodeDist = top.first;
        int node = top.second;

        for (auto neighbour : adj[node])
        {
            if (nodeDist + neighbour.second < distance[neighbour.first])
            {
                auto find_node = st.find(make_pair(distance[neighbour.first], neighbour.first));
                if (find_node != st.end())
                    st.erase(find_node);

                distance[neighbour.first] = nodeDist + neighbour.second;

                st.insert(make_pair(distance[neighbour.first], neighbour.first));
            }
        }
    }
    return distance;
}
```

> **Time Complexity :** O(ElogV) because set do operation in log
> **Space Complexity :** O(N+E)

### Approach 2 : (Using min-heap Priority Queue)

**We will create a min-heap priority queue that arranges elements in ascending order. It's syntax is**

```
	priority_queue<type, vector<type>, greater<type>> pq;
  	priority_queue<int, vector<int>, greater<int>> pq_integers;
```

```cpp

vector<int> dijkstra(vector<vector<int>> &vec, int vertices, int edges, int source)
{
    unordered_map<int, list<pair<int, int>>> adj; // in pair first int will be for vertex and second is for weight

    for (int i = 0; i < edges; i++)
    {
        int u = vec[i][0];
        int v = vec[i][1];
        int weight = vec[i][2];

        adj[u].push_back(make_pair(v, weight));
        adj[v].push_back(make_pair(u, weight));
    }

    vector<int> distance(vertices, INT_MAX);

    distance[source] = 0;
    // min heap priority queue
    // 	priority_queue<type, vector<type>, greater<type>> pq;
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    pq.push(make_pair(0, source));

    while (!pq.empty())
    {
        auto top = pq.top();
        pq.pop();

        int nodeDist = top.first;
        int node = top.second;

        for (auto neighbour : adj[node])
        {
            if (nodeDist + neighbour.second < distance[neighbour.first])
            {
                distance[neighbour.first] = nodeDist + neighbour.second;

                pq.push({distance[neighbour.first], neighbour.first});
            }
        }
    }
    return distance;
}
```

**Some times youu might get TLE in Approach 1**

> **Time Complexity :** O((N+E)\* logN). Going through N nodes and E edges and log N for priority queue
> **Space Complexity :** O(N). Distance array and priority queue

### Reference :

https://youtu.be/dVUR3Rm6biE?list=PLDzeHZWIZsTobi35C3I-tKB3tRDX6YxuA
https://www.codingninjas.com/codestudio/problems/920469
