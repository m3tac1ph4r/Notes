# Triangle Minimum Path Sum || Fixed Starting  Point and Variable Ending Point


Given a `triangle` array, return _the minimum path sum from top to bottom_.

For each step, you may move to an adjacent number of the row below. More formally, if you are on index `i` on the current row, you may move to either index `i` or index `i + 1` on the next row.

**Example 1:**

**Input:** triangle = [ [2],[3,4],[6,5,7],[4,1,8,3]]
**Output:** 11
**Explanation:** The triangle looks like:
   <u>2</u>
  <u>3</u> 4
 6<u> 5</u> 7
4 <u>1</u> 8 3
The minimum path sum from top to bottom is 2 + 3 + 5 + 1 = 11 (underlined above).

**Example 2:**

**Input:** triangle = [ [-10]]
**Output:** -10


### Approach 1 (Recursion) :
```cpp
int solve(int i,int j,int n,vector<vector<int>> &triangle)
{
    if(i==n-1)
    {
        return triangle[i][j];
    }
    int down=triangle[i][j]+solve(i+1,j,n,triangle);
    int diagonal_down=triangle[i][j]+solve(i+1,j+1,n,triangle);
    return min(down,diagonal_down);
}
int minimumPathSum(vector<vector<int>>& triangle, int n){
	// Write your code here.
    int ans=solve(0,0,n,triangle);
    return ans;
}
```


### Approach 2 (Memoization) :

```cpp
int solve(int i,int j,int n,vector<vector<int>> &triangle,vector<vector<int>> &dp)
{
    if(i==n-1)
    {
        return triangle[i][j];
    }
    if(dp[i][j]!=-1)
        return dp[i][j];
    int down=triangle[i][j]+solve(i+1,j,n,triangle,dp);
    int diagonal_down=triangle[i][j]+solve(i+1,j+1,n,triangle,dp);
    return dp[i][j]=min(down,diagonal_down);
}
int minimumPathSum(vector<vector<int>>& triangle, int n){
	// Write your code here.
    vector<vector<int>> dp(n,vector<int>(n,-1));
    int ans=solve(0,0,n,triangle,dp);
    return ans;
}
```


### Approach 3 (Tabulation) :
```cpp
int minimumPathSum(vector<vector<int>>& triangle, int n){
	// Write your code here.
    vector<vector<int>> dp(n,vector<int>(n,0));
    for(int j=0;j<n;j++)
    {
        dp[n-1][j]=triangle[n-1][j];
    }
    for(int i=n-2;i>=0;i--)
    {
        for(int j=i;j>=0;j--)
        {
            int down,diagonal_down;
            down=triangle[i][j]+dp[i+1][j];
            diagonal_down=triangle[i][j]+dp[i+1][j+1];
            dp[i][j]=min(down,diagonal_down);
        }
    }
    return dp[0][0];
}
```


### Approach 4 (Space Optimization) :

![[triangle minimum path_space_app.png]]

```cpp
int minimumTotal(vector<vector<int>>& triangle) {
	int n=triangle.size();
	vector<int> dp(n,0);
	for(int j=0;j<n;j++)
	{
		dp[j]=triangle[n-1][j];
	}
	int k=n-1;
	for(int i=n-2;i>=0;i--)
	{
		vector<int> temp(k--,0);
		for(int j=i;j>=0;j--)
		{
			int down,diagonal_down;
			down=triangle[i][j]+dp[j];
			diagonal_down=triangle[i][j]+dp[j+1];
			temp[j]=min(down,diagonal_down);
		}
		dp=temp;
	}
	return dp[0];
}
```



### Question :
https://www.codingninjas.com/codestudio/problems/triangle_1229398
https://leetcode.com/problems/triangle/

### Reference :
https://youtu.be/SrP-PiLSYC0?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY