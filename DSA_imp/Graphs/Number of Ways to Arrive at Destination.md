# Number of Ways to Arrive at Destination

>**Example of count number of shortest path in graph**
>Using Dijkastra Algorithm


You are in a city that consists of `n` intersections numbered from `0` to `n - 1` with **bi-directional** roads between some intersections. The inputs are generated such that you can reach any intersection from any other intersection and that there is at most one road between any two intersections.

You are given an integer `n` and a 2D integer array `roads` where `roads[i] = [ui, vi, timei]` means that there is a road between intersections `ui` and `vi` that takes `timei` minutes to travel. You want to know in how many ways you can travel from intersection `0` to intersection `n - 1` in the **shortest amount of time**.

Return _the **number of ways** you can arrive at your destination in the **shortest amount of time**_. Since the answer may be large, return it **modulo** `109 + 7`.


**Example 1 :**

![[Arrive at Destination example.png]]

**Input:** n = 7, roads = 
```
[[0,6,7],[0,1,2],[1,2,3],[1,3,3],[6,3,3],[3,5,1],[6,5,1],[2,5,1],[0,4,5],[4,6,2]]
```
**Output:** 4
**Explanation:** The shortest amount of time it takes to go from intersection 0 to intersection 6 is 7 minutes.
The four ways to get there in 7 minutes are:
- 0 ➝ 6
- 0 ➝ 4 ➝ 6
- 0 ➝ 1 ➝ 2 ➝ 5 ➝ 6
- 0 ➝ 1 ➝ 3 ➝ 5 ➝ 6


**Example 2:**

**Input:** n = 2, roads =
```
[[1,0,10]]
```
**Output:** 1
**Explanation:** There is only one way to go from intersection 0 to intersection 1, and it takes 10 minutes.


### Approach (Using Dijkastra Algo) :

```C++

int countPaths(int n, vector<vector<int>> &roads)
{
    int M = 1e9 + 7;
    if (n == 2)
        return 1;
    if (n == 1)
        return 1;
    unordered_map<long long, list<pair<long long, long long>>> adj;
    for (int i = 0; i < roads.size(); i++)
    {
        long long u = roads[i][0];
        long long v = roads[i][1];
        long long w = roads[i][2];

        adj[u].push_back({v, w});
        adj[v].push_back({u, w});
    }

    set<pair<long long, long long>> st;
    vector<long long> distance(n, LONG_MAX);
    vector<long long> path(n, 0);
    distance[0] = 0;
    path[0] = 1;

    st.insert({0, 0});

    while (!st.empty())
    {
        auto top = *(st.begin());
        st.erase(st.begin());
        long u = top.second;

        for (auto it : adj[u])
        {
            long long v = it.first;
            long long wt = it.second;

            if (distance[v] > (distance[u]) + wt)
            {
                auto findNode = st.find({distance[v], v});
                if (findNode != st.end())
                    st.erase(findNode);

                distance[v] = (distance[u] + wt);
                path[v] = path[u];
                st.insert({distance[v], v});
            }
            else if (distance[v] == distance[u] + wt)
            {
                path[v] = (path[v] + path[u]) % M;
            }
        }
    }
    return path[n - 1] % M;
}
```

### Question :
https://leetcode.com/problems/number-of-ways-to-arrive-at-destination/