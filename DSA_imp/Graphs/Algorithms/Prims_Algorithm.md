# Prims Algorithm
#algorithm #graphAlgo 

### Minimum Spanning Tree (MST) :

Suppose we have given a graph. And if we can  made a tree with **n vertices and n-1 edges and all vertices can visit  each other** then it will be called a spanning Tree.
 **And minimum spanning tree does not have a cycle**

Minimum Spanning Tree means *spanning tree which will be having minimum number of weight* is called minimum spanning tree.

![[Minimum_spanning_tree.png]]


> **Importance of Prim's Algorithm ?**
> We will be using Prims algoritm to find the minimum spanning tree of a given graph.


> **Why does Prims Algo doesn't works for DIRECTED GRAPH ?**
> https://www.geeksforgeeks.org/why-prims-and-kruskals-mst-algorithm-fails-for-directed-graph/

### Approach (Bruteforce) :


1. We will be using 3 vectors.
	1. Key intialize with infinite value (for distance)
	2. MST intialize with False values
	3. Parent intialize with -1 value
2. We will start with 0. Mark **key[0]=0** and **parent[key]=-1** 
3. Then find the index which is having minimum value in key array. Mark **MST[index]=TRUE** 
4. FInd the **adjacent neighbours of indexNode** and **update the distance of neighbourNode in key array**  and **update parent[neighbourNode] to indexNode**
5. Again do from STEP 3

![[prims_app1.jpeg]]

![[prims_app2.jpeg]]

![[prims_app3.jpeg]]

```C++

vector<pair<pair<int, int>, int>> calculatePrimsMST(int n, int m, vector<pair<pair<int, int>, int>> &g)
{
    unordered_map<int,list<pair<int,int>>> adj;
    // first int-u second int-v third int-w
    
    // creating adjacency list
    for(int i=0;i<g.size();i++)
    {
        int u=g[i].first.first;
        int v=g[i].first.second;
        int w=g[i].second;
        
        adj[u].push_back({v,w});
        adj[v].push_back({u,w});
    }
    
    // create vectors
    vector<int> key(n+1,INT_MAX);
    vector<bool> mst(n+1,false);
    vector<int> parent(n+1,-1);
    
    key[1]=0;
    for(int i=1;i<=n;i++)
    {
        int mini=INT_MAX;
        int u;
        
        // finding minimum element in key
        for(int j=1;j<=n;j++)
        {
            if(mst[j]==false and key[j]<mini)
            {
                u=j;
                mini=key[j];
            }
        }
        mst[u]=true;
        for(auto neighbour:adj[u])
        {
            int v=neighbour.first;
            int w=neighbour.second;
            
            if(mst[v]==false and w<key[v])
            {
                key[v]=w;
                parent[v]=u;
            }
        }
    }
    vector<pair<pair<int, int>, int>> res;
    for(int i=2;i<=n;i++)
    {
        res.push_back({{parent[i],i},key[i]});
    }
    return res;
}

```


> **Time Complexity :** greater than O(N^2)
> **Space Complexity :** O(N) 3 arrays of N size


### Approach (Optimized Approach using Priority Queue)

**We will create a min-heap priority queue that arranges elements in ascending order. It's syntax is**

```
	priority_queue<type, vector<type>, greater<type>> pq;
  	priority_queue<int, vector<int>, greater<int>> pq_integers;
```

We will be storing **{key[i],i}** in the priority queue.

```C++

vector<pair<pair<int, int>, int>> calculatePrimsMST(int n, int m, vector<pair<pair<int, int>, int>> &g)
{
    unordered_map<int, list<pair<int, int>>> adj;
    // first int-u second int-v third int-w

    // creating adjacency list
    for (int i = 0; i < g.size(); i++)
    {
        int u = g[i].first.first;
        int v = g[i].first.second;
        int w = g[i].second;

        adj[u].push_back({v, w});
        adj[v].push_back({u, w});
    }

    // create vectors
    vector<int> key(n + 1, INT_MAX);
    vector<bool> mst(n + 1, false);
    vector<int> parent(n + 1, -1);

    // first int - key[i](distance)  and second int - i
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;

    key[1] = 0;
    pq.push({0, 1});
    while (!pq.empty())
    {
        // finding minimum element in key
        int u = pq.top().second;
        mst[u] = true;
        pq.pop();
        for (auto neighbour : adj[u])
        {
            int v = neighbour.first;
            int w = neighbour.second;

            if (mst[v] == false and w < key[v])
            {
                parent[v] = u;
                key[v] = w;
                pq.push({key[v], v});
            }
        }
    }
    vector<pair<pair<int, int>, int>> res;
    for (int i = 2; i <= n; i++)
    {
        res.push_back({{parent[i], i}, key[i]});
    }
    return res;
}
```

> **Time Complexity :** O(nlogn)
> **Space Complexity :** O(n)


### Resources :

https://youtu.be/rnYBi9N_vw4?list=PLDzeHZWIZsTobi35C3I-tKB3tRDX6YxuA
https://youtu.be/oNTsS8lGDHw?list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw


### Question :

https://practice.geeksforgeeks.org/problems/minimum-spanning-tree/1#
https://www.codingninjas.com/codestudio/problems/1095633