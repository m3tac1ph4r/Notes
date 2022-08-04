# Unique Paths

There is a robot on an `m x n` grid. The robot is initially located at the **top-left corner** (i.e., `grid[0][0]`). The robot tries to move to the **bottom-right corner** (i.e., `grid[m - 1][n - 1]`). The robot can only move either down or right at any point in time.

Given the two integers `m` and `n`, return _the number of possible unique paths that the robot can take to reach the bottom-right corner_.

The test cases are generated so that the answer will be less than or equal to `2 * 109`.

**Example 1:**

![[unique paths ex1.png]]

**Input:** m = 3, n = 7
**Output:** 28

**Example 2:**

**Input:** m = 3, n = 2
**Output:** 3
**Explanation:** From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Down -> Down
2. Down -> Down -> Right
3. Down -> Right -> Down

### Approach 1(Recursion) :

```cpp
#include <bits/stdc++.h> 
int solve(int i,int j,int m,int n)
{
    if(i==0 and j==0)
        return 1;
    else if(i<0 or j<0)
        return 0;
    
    int up=solve(i-1,j,m,n);
    int left=solve(i,j-1,m,n);
    return up+left;
}
int uniquePaths(int m, int n) {
	// Write your code here.
    int ans=solve(m-1,n-1,m,n);
    return ans;
}
```



### Approach 2 (Memoization) :

```cpp
#include <bits/stdc++.h> 
int solve(int i,int j,int m,int n,vector<vector<int>> &dp)
{
    if(i==0 and j==0)
        return 1;
    else if(i<0 or j<0)
        return 0;
    
    if(dp[i][j]!=-1)
        return dp[i][j];
    
    int up=solve(i-1,j,m,n,dp);
    int left=solve(i,j-1,m,n,dp);
    return dp[i][j]=up+left;
}
int uniquePaths(int m, int n) {
	// Write your code here.
    vector<vector<int>> dp(m,vector<int>(n,-1));
    int ans=solve(m-1,n-1,m,n,dp);
    return ans;
}
```


### Approach 3 (Tabulation) :

```cpp
#include <bits/stdc++.h> 
int uniquePaths(int m, int n) {
	// Write your code here.
    vector<vector<int>> dp(m,vector<int>(n,0));
    dp[0][0]=1;
    for(int i=0;i<m;i++)
    {
        for(int j=0;j<n;j++)
        {
            if(i==0 and j==0)
                continue;
            int up=0,left=0;
            if(i>0)
                up=dp[i-1][j];
            if(j>0)
                left=dp[i][j-1];
            dp[i][j]=up+left;
        }
    }
    return dp[m-1][n-1];
}
```



### Question :
https://leetcode.com/problems/unique-paths/

### Resources :
https://youtu.be/sdE0A2Oxofw?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY