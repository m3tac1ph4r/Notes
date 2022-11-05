# Shortest Path in a Grid with Obstacles Elimination
#interesting 

You are given an `m x n` integer matrix `grid` where each cell is either `0` (empty) or `1` (obstacle). You can move up, down, left, or right from and to an empty cell in **one step**.

Return _the minimum number of **steps** to walk from the upper left corner_ `(0, 0)` _to the lower right corner_ `(m - 1, n - 1)` _given that you can eliminate **at most**_ `k` _obstacles_. If it is not possible to find such walk return `-1`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/09/30/short1-grid.jpg)

**Input:** grid = [ [0,0,0],[1,1,0],[0,0,0],[0,1,1],[0,0,0]], k = 1
**Output:** 6
**Explanation:** 
The shortest path without eliminating any obstacle is 10.
The shortest path with one obstacle elimination at position (3,2) is 6. Such path is (0,0) -> (0,1) -> (0,2) -> (1,2) -> (2,2) -> **(3,2)** -> (4,2).

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/09/30/short2-grid.jpg)

**Input:** grid = [ [0,1,1],[1,1,1],[1,0,0]], k = 1
**Output:** -1
**Explanation:** We need to eliminate at least two obstacles to find such a walk.


### Approach Using BFS :

In every BFS call we will add their valid neighbours and we used 3D array because we can reach at grid[i][j]  by different number of obstacles. So for that I have created 3D array.

```cpp
class Solution {
public:
    vector<int> delRow={-1,0,1,0};
    vector<int> delCol={0,1,0,-1};
    int solve(int n,int m,int k,vector<vector<int>>& grid)
    {
        vector<vector<vector<bool>>> visited(n,vector<vector<bool>>(m,vector<bool>(k+1,false)));
        queue<vector<int>> q;
        q.push({0,0,k});
        visited[0][0][k]=true;
        int res=0;
        
        while(!q.empty())
        {
            int size=q.size();
            while(size--)
            {
                int row=q.front()[0];
                int col=q.front()[1];
                int kk=q.front()[2];
                
                q.pop();
                
                if(row==n-1 and col==m-1)
                    return res;
                
                for(int i=0;i<4;i++)
                {
                    int newRow=row+delRow[i];
                    int newCol=col+delCol[i];
                    
                    if(newRow>=0 and newRow<n and newCol>=0 and newCol<m)
                    {
                        if(grid[newRow][newCol]==1 and kk>0 
                           and visited[newRow][newCol][kk-1]==false)
                        {
                            q.push({newRow,newCol,kk-1});
                            visited[newRow][newCol][kk-1]=true;
                        }
                        if(grid[newRow][newCol]==0 
                                and visited[newRow][newCol][kk]==false)
                        {
                            q.push({newRow,newCol,kk});
                            visited[newRow][newCol][kk]=true;
                        }
                    }
                }
            }
            res++;
        }
        return -1;
    }
    int shortestPath(vector<vector<int>>& grid, int k) {
        
        int n=grid.size();
        int m=grid[0].size();
        
        return solve(n,m,k,grid);
        
    }
};
```


### Question :
https://leetcode.com/problems/shortest-path-in-a-grid-with-obstacles-elimination/