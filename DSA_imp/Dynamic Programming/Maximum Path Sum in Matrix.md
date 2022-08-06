# Maximum Path Sum || Variable Starting Point || Variable Ending Point
#dp_on_grids












### Approach 1 (Recursion) :
```cpp
#include<bits/stdc++.h>
int solve(int i,int j,int n,int m,vector<vector<int>> &matrix)
{
    if(j<0 || j>=m || i<0 || i>=n)
        return -1e7;
    else if(i==0)
        return matrix[0][j];
    int up=matrix[i][j]+solve(i-1,j,n,m,matrix);
    int leftDiagonal=matrix[i][j]+solve(i-1,j-1,n,m,matrix);
    int rightDiagonal=matrix[i][j]+solve(i-1,j+1,n,m,matrix);
    return max(up,max(leftDiagonal,rightDiagonal));
}
int getMaxPathSum(vector<vector<int>> &matrix)
{
    //  Write your code here.
    int n=matrix.size();
    int m=matrix[0].size();
    int ans=INT_MIN;
    for(int j=0;j<m;j++)
    {
        ans=max(ans,solve(n-1,j,n,m,matrix));
    }
    return ans;
}
```

>**Time Complexity :** O(3^n) nearly exponential (Because for every index we are going up,leftDIagonal,rightDiagonal)
>**Space Complexity :** O(n) (Recurion stack space is storing path)


### Approach 2 (Memoization) :

```cpp
#include<bits/stdc++.h>
int solve(int i,int j,int n,int m,vector<vector<int>> &matrix,vector<vector<int>> &dp)
{
    if(j<0 || j>=m || i<0 || i>=n)
        return -1e7;
    else if(i==0)
        return matrix[0][j];
    else if(dp[i][j]!=-1)
        return dp[i][j];
    int up=matrix[i][j]+solve(i-1,j,n,m,matrix,dp);
    int leftDiagonal=matrix[i][j]+solve(i-1,j-1,n,m,matrix,dp);
    int rightDiagonal=matrix[i][j]+solve(i-1,j+1,n,m,matrix,dp);
    return dp[i][j]=max(up,max(leftDiagonal,rightDiagonal));
}
int getMaxPathSum(vector<vector<int>> &matrix)
{
    //  Write your code here.
    int n=matrix.size();
    int m=matrix[0].size();
    vector<vector<int>> dp(n,vector<int>(m,-1));
    int ans=INT_MIN;
    for(int j=0;j<m;j++)
    {
        ans=max(ans,solve(n-1,j,n,m,matrix,dp));
    }
    return ans;
}
```


>**Time Complexity :** ```O(n * m)```
>**Space Complexity :** ```O(n * m) + O(n) (Recurion stack space is storing path)```


### Approach 3 (Tabulation) :

```cpp
int getMaxPathSum(vector<vector<int>> &matrix)
{
    //  Write your code here.
    int n=matrix.size();
    int m=matrix[0].size();
    vector<vector<int>> dp(n,vector<int>(m,0));
    for(int j=0;j<m;j++)
    {
        dp[n-1][j]=matrix[n-1][j];
    }
    for(int i=n-2;i>=0;i--)
    {
        for(int j=0;j<m;j++)
        {
            int down,leftDiagonal,rightDiagonal;
            down=matrix[i][j]+dp[i+1][j];
            if(j-1<0)
                leftDiagonal=-1e7;
            else
                leftDiagonal=matrix[i][j]+dp[i+1][j-1];
            if(j+1>=m)
                rightDiagonal=-1e7;
            else
                rightDiagonal=matrix[i][j]+dp[i+1][j+1];
            dp[i][j]=max(down,max(leftDiagonal,rightDiagonal));
        }
    }
    int ans=INT_MIN;
    for(int j=0;j<m;j++)
    {
        ans=max(ans,dp[0][j]);
    }
    return ans;
}
```

>**Time Complexity :** ```O(n *  m) + O(m) (single for loop)```
>**Space Complexity :** ```O(n * m) (dp array)```


### Approach 3 (Space Optimization) :

```cpp
#include<bits/stdc++.h>
int getMaxPathSum(vector<vector<int>> &matrix)
{
    //  Write your code here.
    int n=matrix.size();
    int m=matrix[0].size();
    vector<int> prev(m,0);
    vector<int> curr(m,0);
    
    for(int j=0;j<m;j++)
    {
        prev[j]=matrix[0][j];
    }
    for(int i=1;i<n;i++)
    {
        for(int j=0;j<m;j++)
        {
            int up,leftDiagonal,rightDiagonal;
            up=matrix[i][j]+prev[j];
            if(j-1<0)
                leftDiagonal=-1e7;
            else
                leftDiagonal=matrix[i][j]+prev[j-1];
            if(j+1>=m)
                rightDiagonal=-1e7;
            else
                rightDiagonal=matrix[i][j]+prev[j+1];
            
            curr[j]=max(up,max(leftDiagonal,rightDiagonal));
        }
        prev=curr;
    }
    int ans=INT_MIN;
    for(int j=0;j<m;j++)
    {
        ans=max(ans,prev[j]);
    }
    return ans;
}
```

>**Time Complexity :** ```O(n * m) + O(m) (single for loop)```
>**Space Complexity :** ```O(m) (dp array)```


### Question :
https://www.codingninjas.com/codestudio/problems/maximum-path-sum-in-the-matrix_797998

### Reference :
https://youtu.be/N_aJ5qQbYA0?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY