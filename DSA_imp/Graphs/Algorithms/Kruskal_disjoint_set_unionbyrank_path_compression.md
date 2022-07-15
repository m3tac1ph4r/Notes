# Kruskal Algorithm (Disjoint Set,Union by Rank, Path Compression)
#graphAlgo #algorithm 

We will use Kruskal Algorithm to find the **minimum spanning tree** of a given graph.

As mentioned earlier, the Kruskal algorithm is used to generate a minimum [spanning tree](https://www.simplilearn.com/tutorials/data-structure-tutorial/spanning-tree-in-data-structure "spanning tree") for a given graph. But, what exactly is a minimum spanning tree? A minimum spanning tree is a subset of a graph with the same number of vertices as the graph and edges equal to the number of vertices -1. It also has a minimal cost for the sum of all edge weights in a spanning tree.

Kruskal’s algorithm sorts all the edges in increasing order of their edge weights and keeps adding nodes to the tree only if the chosen edge does not form any cycle. Also, it picks the edge with a minimum cost at first and the edge with a maximum cost at last. Hence, you can say that the Kruskal algorithm makes a locally optimal choice, intending to find the global optimal solution. That is why it is called a [Greedy Algorithm.](https://www.simplilearn.com/tutorials/data-structure-tutorial/greedy-algorithm "Greedy Algorithm.")

### Approach :

Any MST algorithm revolves around determining whether adding an edge would result in a loop or not. Union Find is the most popular algorithm for determining this. The Union-Find algorithm separates vertices into clusters, allowing you to determine whether two vertices belong to the same cluster and hence if adding an edge will produce a cycle.

The strategy to implement the Kruskal algorithm using Union-Find is given below:

-   Construct a structure to keep track of the source and destination nodes, as well as their weight.
-   Sort all the edges of a graph according to their edge-weight values.
-   Create three distinct sets to maintain nodes of a graph, their hierarchy in a tree, and corresponding ranks for every node.
-   Primarily, initialize all rank values to 0 and parent values to -1 (representing each node as its own tree itself).
-   For each insertion of an edge in MST, you will update the rank and parent of each node.
-   Do not insert the edge connecting two nodes if they have the same parent node, as this will cause a cycle in the tree structure.

```C++

bool comp(vector<int> &a, vector<int> &b)
{
    return a[2] < b[2];
}
int findParent(int node, vector<int> &parent)
{
    if (parent[node] == node)
        return node;
    return parent[node] = findParent(parent[node], parent); // path compression
    // we will update the parent. Suppose parent of 6 is 4 and parent of 4 is 1. This will make parent[6]=1
}
void unionSet(int u, int v, vector<int> &rank, vector<int> &parent)
{
    if (rank[u] < rank[v])
    {
        parent[u] = v;
        rank[v]++;
    }
    else if (rank[v] < rank[u])
    {
        parent[v] = u;
        rank[u]++;
    }
    else // if rank[u]==rank[v]
    {
        parent[u] = v;
        rank[v]++;
    }
}
int kruskalMST(int n, int m, vector<vector<int>> &graph)
{
    vector<int> parent(n + 1);
    vector<int> rank(n + 1, 0);
    for (int i = 0; i <= n; i++)
        parent[i] = i;
    int min_wt = 0;
    sort(graph.begin(), graph.end(), comp); // sort the graph acc to weight
    for (int i = 0; i < m; i++)
    {
        int u = findParent(graph[i][0], parent);
        int v = findParent(graph[i][1], parent);
        int wt = graph[i][2];
        if (u != v)
        {
            min_wt += wt;
            unionSet(u, v, rank, parent);
        }
    }
    return min_wt;
}
```

>**Time Complexity :** O(ELogE)
>**Space Complexity :** O(N)


### Question :

https://www.codingninjas.com/codestudio/problems/1082553

### Reference :

https://youtu.be/KxLtIrCyXwE?list=PLDzeHZWIZsTobi35C3I-tKB3tRDX6YxuA
https://bit.ly/3IHkHf5