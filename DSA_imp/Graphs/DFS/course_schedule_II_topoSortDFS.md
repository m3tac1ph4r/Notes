#  Course Schedule II
There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you **must** take course `bi` first if you want to take course `ai`.

-   For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return _the ordering of courses you should take to finish all courses_. If there are many valid answers, return **any** of them. If it is impossible to finish all courses, return **an empty array**.

**Example 1:**

**Input:** numCourses = 2, prerequisites = [[1,0]]
**Output:** [0,1]
**Explanation:** There are a total of 2 courses to take. To take course 1 you should have finished course 0. So the correct course order is [0,1].

**Example 2:**

**Input:** numCourses = 4, prerequisites = [ [1,0],[2,0],[3,1],[3,2]]
**Output:** [0,2,1,3]
**Explanation:** There are a total of 4 courses to take. To take course 3 you should have finished both courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0.
So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3].

**Example 3:**

**Input:** numCourses = 1, prerequisites = []
**Output:** [0]


### Approach (TopoSort DFS + Cycle Detection) :
We will use topoSort using DFS and cycle detection in DFS(we will use an extra array name bag to check whether that node is in the recursion call or not).

```cpp
bool topoSort(int node, stack<int> &st, vector<bool> &visited, unordered_map<int, list<int>> &adj, vector<bool> &bag)
{
    visited[node] = true;
    bag[node] = true;
    for (auto it : adj[node])
    {
        if (!visited[it])
        {
            bool ans = topoSort(it, st, visited, adj, bag);
            if (ans)
                return true;
        }
        else if (bag[it] == true)
            return true;
    }
    bag[node] = false;
    st.push(node);
    return false;
}
vector<int> findOrder(int numCourses, vector<vector<int>> &prerequisites)
{
    stack<int> st;
    unordered_map<int, list<int>> adj;
    vector<int> outDegree(numCourses, 0);
    for (int i = 0; i < prerequisites.size(); i++)
    {
        int u = prerequisites[i][0];
        int v = prerequisites[i][1];
        adj[v].push_back(u);
    }
    vector<bool> visited(numCourses, false);
    vector<bool> parent(numCourses, false);
    vector<int> ans;
    for (int i = 0; i < numCourses; i++)
    {
        if (!visited[i])
        {
            if (topoSort(i, st, visited, adj, parent))
                return ans;
        }
    }

    while (!st.empty())
    {
        int t = st.top();
        ans.push_back(t);
        st.pop();
    }
    return ans;
}
```


### Question :
https://leetcode.com/problems/course-schedule-ii/