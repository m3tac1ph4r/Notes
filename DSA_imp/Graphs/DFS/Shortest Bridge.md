# Shortest Bridge using FloodFill and DFS

You are given an `n x n` binary matrix `grid` where `1` represents land and `0` represents water.

An **island** is a 4-directionally connected group of `1`'s not connected to any other `1`'s. There are **exactly two islands** in `grid`.

You may change `0`'s to `1`'s to connect the two islands to form **one island**.

Return _the smallest number of_ `0`_'s you must flip to connect the two islands_.


**Example 1:**

**Input:** grid = [ [0,1],[1,0] ]
**Output:** 1

**Example 2:**

**Input:** grid = [ [0,1,0],[0,0,0],[0,0,1] ]
**Output:** 2

**Example 3:**

**Input:** grid = [ [1,1,1,1,1],[1,0,0,0,1],[1,0,1,0,1],[1,0,0,0,1],[1,1,1,1,1] ]
**Output:** 1

![[shortest_bridge_app.png]]


### Approach :

1. In the question it clearly given that we have exactly two islands.
2. We will store the coordinate of first island in **vector x** and coordinate of second island in **vector y**
3. Now find the minimum distance from x[i] to y[i]
```
int dist=abs(x[i].first - y[j].first) + abs(x[i].second - y[j].second) - 1;;
```

```C++

void floodFill(int i,int j,vector<pair<int,int>> &r,vector<vector<int>> &grid)
{
    if(i<0 || j<0 || i>=grid.size() || j>=grid[i].size() || grid[i][j]==0)
        return;
    
    grid[i][j]=0;
    r.push_back({i,j});
    
    // 4-directional
    floodFill(i-1,j,r,grid);
    floodFill(i,j-1,r,grid);
    floodFill(i+1,j,r,grid);
    floodFill(i,j+1,r,grid);
    
    return;
}
int shortestBridge(vector<vector<int>>& grid) {
    int islandCount=0;
    vector<pair<int,int>> x;  // for fist island
    vector<pair<int,int>> y;  // for second island
    
    for(int i=0;i<grid.size();i++)
    {
        for(int j=0;j<grid[i].size();j++)
        {
            if(grid[i][j]==1)
            {
                islandCount++;
                if(islandCount==1)
                    floodFill(i,j,x,grid);
                else if(islandCount==2)
                    floodFill(i,j,y,grid);
            }
        }
    }
    int ans=INT_MAX;
    for(int i=0;i<x.size();i++)
    {
        for(int j=0;j<y.size();j++)
        {
            int dist=abs(x[i].first - y[j].first) + abs(x[i].second - y[j].second) - 1;;
            ans=min(ans,dist);
        }
    }
    return ans;
}
```


### Question :

https://leetcode.com/problems/shortest-bridge/


### Reference :

https://youtu.be/3Yz-IDSpm-E