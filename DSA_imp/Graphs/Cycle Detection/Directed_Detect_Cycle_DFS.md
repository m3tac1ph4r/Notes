# Cycle Detection in Directed Graph using DFS

**Why we didn't used the undirected graph algorithm ?**

![[Directed_DFS_why.png]]

As you can this algorithm is saying that 3,7,8  is a cycle but it's not.

> To avoid this we will add one vector name **bag** which will check which node is a part of recursion call and which are not.
> When we made recursion call for node "x" then mark  *bag[x]=true* and when it will not have any neighbour in last then mark *bag[x]=false*

### Approach :

![[Detect_Cycle_Directed_DFS_app.png]]


```C++
bool dfsCyclic(int node, vector<bool> &bag, vector<bool> &visited, unordered_map<int, list<int>> &adj)
{
    visited[node] = true;
    bag[node] = true;

    for (auto it : adj[node])
    {
        if (!visited[it])
        {
            bool ans = dfsCyclic(it, bag, visited, adj);
            if (ans == true)
                return true;
        }
        else if (bag[it] == true)
            return true; // means it is already visited and also there in the bag. means cycle is present
    }
    bag[node] = false; // removing the node from the bag
    return false;
}

int detectCycleInDirectedGraph(int n, vector<pair<int, int>> &edges)
{
    unordered_map<int, list<int>> adj;
    vector<bool> visited(n + 1, false);
    vector<bool> bag(n + 1, false);

    for (int i = 0; i < edges.size(); i++)
    {
        int u = edges[i].first;
        int v = edges[i].second;

        adj[u].push_back(v);
    }

    for (int i = 1; i <= n; i++)
    {
        if (!visited[i])
        {
            bool ans = dfsCyclic(i, bag, visited, adj);
            if (ans == true)
                return true;
        }
    }
    return false;
}
```

> **Time complexity :** O(N+E)
> **Space Complexity :** O(2N) + O(N)
> O(2N) -  because we have used 2 vectors
> O(N) - Auxillary space i.e stack(recursion)

### Question :

https://leetcode.com/problems/course-schedule/

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you **must** take course `bi` first if you want to take course `ai`.

-   For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return `true` if you can finish all courses. Otherwise, return `false`.

**Example 1:**
**Input:** numCourses = 2, prerequisites = [ [1,0] ]
**Output:** true
**Explanation:** There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.

**Example 2:**
**Input:** numCourses = 2, prerequisites = [ [1,0],[0,1] ]
**Output:** false
**Explanation:** There are a total of 2 courses to take. 
To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.

![[Directed_Cycle_COurse_schedule_DFS.png]]


```C++
bool dfsCyclic(int node, vector<bool> &visited, vector<bool> &bag, unordered_map<int, list<int>> &adj)
{
    visited[node] = true;
    bag[node] = true;

    for (auto it : adj[node])
    {
        if (!visited[it])
        {
            bool ans = dfsCyclic(it, visited, bag, adj);
            if (ans == true)
                return true;
        }
        else if (bag[it])
            return true;
    }
    bag[node] = false;
    return false;
}
bool canFinish(int numCourses, vector<vector<int>> &prerequisites)
{
    if (prerequisites.size() == 1 || numCourses == 0)
        return true;
    unordered_map<int, list<int>> adj;
    vector<bool> visited(numCourses, false);
    vector<bool> bag(numCourses, false);

    for (int i = 0; i < prerequisites.size(); i++)
    {
        int u = prerequisites[i][0];
        int v = prerequisites[i][1];
        adj[v].push_back(u);
    }

    for (int i = 0; i < numCourses; i++)
    {
        if (!visited[i])
        {
            bool ans = dfsCyclic(i, visited, bag, adj);
            if (ans == true)
                return false;
        }
    }
    return true;
}
```

### Reference :

https://youtu.be/Tl5qbEmEQyY?list=PLDzeHZWIZsTobi35C3I-tKB3tRDX6YxuA
https://youtu.be/uzVUw90ZFIg?list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw