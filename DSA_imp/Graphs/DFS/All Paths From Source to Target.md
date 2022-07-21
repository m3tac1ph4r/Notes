# All Paths From Source to Target

Given a directed acyclic graph (**DAG**) of `n` nodes labeled from `0` to `n - 1`, find all possible paths from node `0` to node `n - 1` and return them in **any order**.

The graph is given as follows: `graph[i]` is a list of all nodes you can visit from node `i` (i.e., there is a directed edge from node `i` to node `graph[i][j]`).

**Example 1:**
![[all_path_ex1.png]]

**Input:** graph = [ [1,2],[3],[3],[] ]
**Output:** [ [0,1,3],[0,2,3] ]
**Explanation:** There are two paths: 0 -> 1 -> 3 and 0 -> 2 -> 3.

**Example 2:**
![[all_path_ex2.png]]

**Input:** graph = [ [4,3,1],[3,2,4],[3],[4],[] ]
**Output:** [ [0,4],[0,3,4],[0,1,3,4],[0,1,2,3,4],[0,1,4] ]

### Approach (Using DFS and Backtracking) :

```cpp

void solve(int node, int n, unordered_map<int, list<int>> &adj, vector<int> temp, vector<vector<int>> &ans)
{
    if (node == n - 1)
    {
        temp.push_back(node);
        ans.push_back(temp);
        return;
    }

    temp.push_back(node);
    for (auto it : adj[node])
    {
        solve(it, n, adj, temp, ans);
    }
}
vector<vector<int>> allPathsSourceTarget(vector<vector<int>> &graph)
{
    vector<vector<int>> ans;

    unordered_map<int, list<int>> adj;
    int n = graph.size();
    for (int i = 0; i < n; i++)
    {
        for (int j = 0; j < graph[i].size(); j++)
        {
            int v = graph[i][j];
            adj[i].push_back(v);
        }
    }

    vector<int> temp;
    solve(0, n, adj, temp, ans);
    return ans;
}
```

### Question :

https://leetcode.com/problems/all-paths-from-source-to-target/
