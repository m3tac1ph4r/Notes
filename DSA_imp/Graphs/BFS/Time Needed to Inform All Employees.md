# Time Needed to Inform All Employees

A company has `n` employees with a unique ID for each employee from `0` to `n - 1`. The head of the company is the one with `headID`.

Each employee has one direct manager given in the `manager` array where `manager[i]` is the direct manager of the `i-th` employee, `manager[headID] = -1`. Also, it is guaranteed that the subordination relationships have a tree structure.

The head of the company wants to inform all the company employees of an urgent piece of news. He will inform his direct subordinates, and they will inform their subordinates, and so on until all employees know about the urgent news.

The `i-th` employee needs `informTime[i]` minutes to inform all of his direct subordinates (i.e., After informTime[i] minutes, all his direct subordinates can start spreading the news).

Return _the number of minutes_ needed to inform all the employees about the urgent news.

**Example 1:**

**Input:** n = 1, headID = 0, manager = [-1], informTime = [0]
**Output:** 0
**Explanation:** The head of the company is the only employee in the company.

**Example 2:**

![[time_needed_to_inform_all_employees_ex1.png]]

**Input:** n = 6, headID = 2, manager = [2,2,-1,2,2,2], informTime = [0,0,1,0,0,0]
**Output:** 1
**Explanation:** The head of the company with id = 2 is the direct manager of all the employees in the company and needs 1 minute to inform them all.
The tree structure of the employees in the company is shown.


### Approach(Using BFS) :

![[time_needed_to_inform_all_employees_app.png]]

```cpp
int numOfMinutes(int n, int headID, vector<int> &manager, vector<int> &informTime)
{
    unordered_map<int, list<pair<int, int>>> adj;
    if (n == 1)
        return informTime[0];
    for (int i = 0; i < n; i++)
    {
        if (manager[i] == -1)
            continue;
        else
        {
            adj[manager[i]].push_back({i, informTime[i]});
        }
    }

    vector<int> distance(n, INT_MAX);
    queue<pair<int, int>> q;
    q.push({headID, informTime[headID]});
    distance[headID] = informTime[headID];
    while (!q.empty())
    {
        int id = q.front().first;
        q.pop();

        for (auto it : adj[id])
        {
            int v = it.first;
            int time = it.second;
            if (distance[id] + time < distance[v])
            {
                distance[v] = distance[id] + time;
                q.push({v, distance[v]});
            }
        }
    }
    int ans = 0;
    for (int i = 0; i < n; i++)
    {
        if (distance[i] != INT_MAX)
            ans = max(ans, distance[i]);
    }
    return ans;
}
```


### Question :

https://leetcode.com/problems/time-needed-to-inform-all-employees/