# Topological Sort (Kahn's Algorithm) :
#algorithm #graphAlgo 

>**A directed acyclic graph (DAG) G has at least one vertex with the indegree zero and one vertex with the out-degree zero.**

Given a Directed Acyclic Graph (DAG) with V vertices and E edges, Find any Topological Sorting of that Graph.

![[topo_BFS_ex.png]]

**OUTPUT :** 4 5 0 2 3 1



### Approach :

Essentially, Kahn’s algorithm works by keeping track of the number of incoming edges into each node (indegree)

1. FInd the indegrees for all vertex. 
2. Then insert all the node which are having indegree 0. 
3. Store the front node of queue in the variable name front and insert into the ans array.
4. Then find neighbour of queue[front] and decrease the indegree of neighbours. If indegree of neighour is 0 then insert into the queue else move on
5. In the last you will have topological sort in the array stored

![[toposort_bfs_approach.png]]

```C++
vector<int> topoSort(int V, vector<int> adj[])
{
    // code here
    vector<int> ans;
    vector<int> indegree(V, 0);
    for (int i = 0; i < V; i++)
    {
        for (auto it : adj[i])
            indegree[it]++;
    }

    queue<int> q;
    for (int i = 0; i < V; i++)
    {
        if (indegree[i] == 0)
            q.push(i);
    }

    while (!q.empty())
    {
        int front = q.front();
        q.pop();
        ans.push_back(front);
        for (auto it : adj[front])
        {
            indegree[it]--;
            if (indegree[it] == 0)
                q.push(it);
        }
    }
    return ans;
}
```

 > **How we will check whether there is a cycle or not ?**
 > In the last we will get the array. *If number of elements in the array are equal to the number of vertex* then **no cycle** present. If it is less than or greater than the vertex then it means cycle is present.

> **Time Complexity :** O(N+E)
> **Space Complexity :** O(v)

**Question 1: What are the applications of Kahn’s Algorithm?**

Answer: Kahn’s algorithm for topological sorting is used mainly when tasks or items have to be ordered, where some tasks or items have to occur before others can. For example:  

1.  Scheduling jobs, given dependencies some jobs have on some other jobs.
2.  Course arrangement in educational institutions. Finding prerequisites of any job or task.
3.  Detecting deadlocks in operating systems. Finding out if cycles exist in a graph.
4.  Resolving symbol dependencies in linkers. Compile-time build dependencies. Deciding the appropriate order of performing compilation tasks in makefiles.
 
### Question :

https://practice.geeksforgeeks.org/problems/topological-sort/1#

### Reference :
https://youtu.be/rZv_jHZva34?list=PLgUwDviBIf0rGEWe64KWas0Nryn7SCRWw

https://youtu.be/6XmzL04mlgQ?list=PLDzeHZWIZsTobi35C3I-tKB3tRDX6YxuA