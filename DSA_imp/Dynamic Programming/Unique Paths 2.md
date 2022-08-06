# Unique Paths 2
#dp_on_grids

Same as Unique paths [[Unique Paths]]  with small change.

You are given an `m x n` integer array `grid`. There is a robot initially located at the **top-left corner** (i.e., `grid[0][0]`). The robot tries to move to the **bottom-right corner** (i.e., `grid[m-1][n-1]`). The robot can only move either down or right at any point in time.

An obstacle and space are marked as `1` or `0` respectively in `grid`. A path that the robot takes cannot include **any** square that is an obstacle.

Return _the number of possible unique paths that the robot can take to reach the bottom-right corner_.

The testcases are generated so that the answer will be less than or equal to `2 * 109`.

**Example 1:**

![[unique_path_2_ex.png]]

**Input:** obstacleGrid = [ [0,0,0],[0,1,0],[0,0,0]]
**Output:** 2
**Explanation:** There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right

**Example 2:**

![[unique_path_2_ex2.png]]

**Input:** obstacleGrid = [ [0,1],[0,0]]
**Output:** 1


### Approach 1 (Memoization) :

```cpp
    int solve(int i,int j,int m,int n,vector<vector<int>> &dp,vector<vector<int>>& obstacleGrid)
	{
	    if(i<0 or j<0)
	        return 0;
	    if(i>=0 and j>=0 and obstacleGrid[i][j]==1)
            return 0;
        if(i==0 and j==0)
	        return 1;
	    if(dp[i][j]!=-1)
	        return dp[i][j];
	    
	    int up=solve(i-1,j,m,n,dp,obstacleGrid);
	    int left=solve(i,j-1,m,n,dp,obstacleGrid);
	    return dp[i][j]=up+left;
	}
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m=obstacleGrid.size();
        int n=obstacleGrid[0].size();
        vector<vector<int>> dp(m,vector<int>(n,-1));
        int ans=solve(m-1,n-1,m,n,dp,obstacleGrid);
        return ans;
    }
```


### Approach 2 (Tabulation) :

```cpp
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m=obstacleGrid.size();
        int n=obstacleGrid[0].size();
        vector<vector<int>> dp(m,vector<int>(n,0));
        
        for(int i=0;i<m;i++)
        {
            for(int j=0;j<n;j++)
            {
                if(i>=0 and j>=0 and obstacleGrid[i][j]==1)
                    dp[i][j]=0;
                else if(i==0 and j==0)
                    dp[i][j]=1;
                else
                {
                    int up=0,left=0;
                    if(i>0)
                        up=dp[i-1][j];
                    if(j>0)
                        left=dp[i][j-1];
                    dp[i][j]=up+left;
                }
            }
        }
        return dp[m-1][n-1];
    }
```

### Question :
https://leetcode.com/problems/unique-paths-ii/

### Reference :
https://youtu.be/TmhpgXScLyY?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY