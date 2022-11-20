
# Cheapest Flights within K Stops


There are `n` cities connected by some number of flights. You are given an array `flights` where `flights[i] = [fromi, toi, pricei]` indicates that there is a flight from city `fromi` to city `toi` with cost `pricei`.

You are also given three integers `src`, `dst`, and `k`, return _**the cheapest price** from_ `src` _to_ `dst` _with at most_ `k` _stops._ If there is no such route, return `-1`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2022/03/18/cheapest-flights-within-k-stops-3drawio.png)

**Input:** n = 4, flights = [[0,1,100],[1,2,100],[2,0,100],[1,3,600],[2,3,200]], src = 0, dst = 3, k = 1
**Output:** 700
**Explanation:**
The graph is shown above.
The optimal path with at most 1 stop from city 0 to 3 is marked in red and has cost 100 + 600 = 700.
Note that the path through cities [0,1,2,3] is cheaper but is invalid because it uses 2 stops.

**Example 2:**

![](https://assets.leetcode.com/uploads/2022/03/18/cheapest-flights-within-k-stops-1drawio.png)

**Input:** n = 3, flights = [[0,1,100],[1,2,100],[0,2,500]], src = 0, dst = 2, k = 1
**Output:** 200
**Explanation:**
The graph is shown above.
The optimal path with at most 1 stop from city 0 to 2 is marked in red and has cost 100 + 100 = 200.

**Example 3:**

![](https://assets.leetcode.com/uploads/2022/03/18/cheapest-flights-within-k-stops-2drawio.png)

**Input:** n = 3, flights = [[0,1,100],[1,2,100],[0,2,500]], src = 0, dst = 2, k = 0
**Output:** 500
**Explanation:**
The graph is shown above.
The optimal path with no stops from city 0 to 2 is marked in red and has cost 500.


### Approach :

We will not use priority_queue taking distance as a key because our main focus is to reach target by atmost k stops. And suppose we reached the destination with minimum weight but stops are greater than k then the answer will wrong. So this time we will not take distance as key. We will not use priority_queue because we will take steps as a key and steps can only be increase by 1. So they will automatically be sorted.

![[cheapest_flights_within_k_stops_queue.png]]


```cpp
class Solution {
public:
    int findCheapestPrice(int n, vector<vector<int>>& flights, int src, int dst, int k) 
    {
        unordered_map<int,list<pair<int,int>>> adj;
        for(int i=0;i<flights.size();i++)
        {
            int u=flights[i][0];
            int v=flights[i][1];
            int wt=flights[i][2];

            adj[u].push_back({v,wt});
        }
        queue<pair<int,pair<int,int>>> q;  // {stops,{node,distance}}
        vector<int> distance(n,INT_MAX);
        distance[src]=0;
        q.push({0,{src,0}});

        while(!q.empty())
        {
            int stops=q.front().first;
            int node=q.front().second.first;
            int dist=q.front().second.second;
            q.pop();

            if(stops>k)
                continue;
            if(node==dst)
                continue;
            for(auto it:adj[node])
            {
                int nbrNode=it.first;
                int wt=it.second;

                if(dist+wt<distance[nbrNode] and stops<=k)
                {
                    distance[nbrNode]=dist+wt;
                    q.push({stops+1,{nbrNode,dist+wt}});
                }
            }
        }

        // for(auto it:distance)
        //     cout<<it<<" ";
        cout<<endl;
        if(distance[dst]==INT_MAX)
            return -1;
        else
            return distance[dst];    
    }
};
```


### Link :
https://youtu.be/9XybHVqTHcQ?list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn

### Question :
https://leetcode.com/problems/cheapest-flights-within-k-stops/description/