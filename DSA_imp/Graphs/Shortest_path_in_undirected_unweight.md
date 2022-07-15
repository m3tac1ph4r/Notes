# Shortest path in an unweighted graph in undirected graph(unit weight)

> **BFS Traversal** had a property that it can find the shortest path of undirected and unweight graph

The city of Ninjaland is analogous to the unweighted graph. The city has ‘N’ houses numbered from 1 to ‘N’ respectively and are connected by M bidirectional roads. If a road is connecting two houses ‘X’ and ‘Y’ which means you can go from ‘X’ to ‘Y’ or ‘Y’ to ‘X’. It is guaranteed that you can reach any house from any other house via some combination of roads. Two houses are directly connected by at max one road.

A path between house ‘S’ to house ‘T’ is defined as a sequence of vertices from ‘S’ to ‘T’. Where starting house is ‘S’ and the ending house is ‘T’ and there is a road connecting two consecutive houses. Basically, the path looks like this: (S , h1 , h2 , h3 , ... T). you have to find the shortest path from ‘S’ to ‘T’.

For Example

```
In the below map of Ninjaland let say you want to go from S=1 to T=8, the shortest path is (1, 3, 8). You can also go from S=1 to T=8  via (1, 2, 5, 8)  or (1, 4, 6, 7, 8) but these paths are not shortest.
```

![[shortest_path_undirect_ex.png]]


### Approach (Using BFS) :

1. We will use queue for BFS traversal. Then create visited array and parent array. Parent array will store the parent of node.
2. Then create an adjacency list
3. Push source in the queue. Mark true in visited[source] and **parent[source] =  -1**
4. Then  mark visited for all it's adjacent neighbours and mark their parent as node.
5. Now you have to find parent of target  till the source
6. Reverse the path bcz it is from target to source

![[shortest_path_bfs_undirected_app.png]]

```C++

vector<int> shortestPath( vector<pair<int,int>> edges , int n , int m, int s , int t){
    unordered_map<int,list<int>> adj;
    for(int i=0;i<edges.size();i++)
    {
        int u=edges[i].first;
        int v=edges[i].second;
        
        adj[u].push_back(v);
        adj[v].push_back(u);
    }
    
    vector<bool> visited(n,false);
    unordered_map<int,int> parent;
    queue<int> q;
    
            q.push(s);
            visited[s]=true;
            parent[s]=-1;
            while(!q.empty())
            {
                int front=q.front();
                q.pop();
                for(auto it:adj[front])
                {
                    if(!visited[it])
                    {
                        visited[it]=true;
                        parent[it]=front;
                        q.push(it);
                    }
                }
            }
    
            vector<int> ans;
            int curr=t;
            ans.push_back(t);
            while(curr!=s)
            {
                curr=parent[curr];
                ans.push_back(curr);
            }
            reverse(ans.begin(),ans.end());
            return ans;
}
```


### Question :

https://www.codingninjas.com/codestudio/problems/shortest-path-in-an-unweighted-graph_981297

### Reference :

https://youtu.be/abIEXKFpLNE?list=PLDzeHZWIZsTobi35C3I-tKB3tRDX6YxuA