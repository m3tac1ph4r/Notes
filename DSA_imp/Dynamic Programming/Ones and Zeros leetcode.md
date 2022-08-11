# Ones and Zeroes (Logic is same as 0 1 Knapsack) 3D DP
#dp_on_sequences 


You are given an array of binary strings `strs` and two integers `m` and `n`.

Return _the size of the largest subset of `strs` such that there are **at most**_ `m` `0`_'s and_ `n` `1`_'s in the subset_.

A set `x` is a **subset** of a set `y` if all elements of `x` are also elements of `y`.

**Example 1:**

**Input:** strs = ["10","0001","111001","1","0"], m = 5, n = 3
**Output:** 4
**Explanation:** The largest subset with at most 5 0's and 3 1's is {"10", "0001", "1", "0"}, so the answer is 4.
Other valid but smaller subsets include {"0001", "1"} and {"10", "1", "0"}.
{"111001"} is an invalid subset because it contains 4 1's, greater than the maximum of 3.

**Example 2:**

**Input:** strs = ["10","0","1"], m = 1, n = 1
**Output:** 2
**Explanation:** The largest subset is {"0", "1"}, so the answer is 2.



![[ones_zeros_leetcode_app.png]]


### Approach 1 (Recursion) :

```cpp
class Solution {
public:
    int solve(int i,vector<string> &strs,int m,int n,vector<pair<int,int>> &adj)
    {
        auto out=adj[i];
        int c0=out.first;
        int c1=out.second;
        if(i==0)
        {
            if(m>=c0 and n>=c1)
                return 1;
            else
                return 0;
        }
        int pick=0;
        if(m>=c0 and n>=c1)
            pick=1+solve(i-1,strs,m-c0,n-c1,adj);
        int nonpick=solve(i-1,strs,m,n,adj);
        return max(pick,nonpick);
        
    }
    int findMaxForm(vector<string>& strs, int m, int n) {
        int l=strs.size();
        vector<pair<int,int>> adj;
        for(int i=0;i<l;i++)
        {
            int c0=0,c1=0;
            for(char ch:strs[i])
            {
                if(ch=='0')
                    c0++;
                else
                    c1++;
            }
            adj.push_back({c0,c1});
        }
        return solve(l-1,strs,m,n,adj);
    }
};
```


### Approach 2 (Memoization) :

```cpp
class Solution {
public:
    int solve(int i,vector<string> &strs,int m,int n,vector<pair<int,int>> &adj,vector<vector<vector<int>>> &dp)
    {
        auto out=adj[i];
        int c0=out.first;
        int c1=out.second;
        if(i==0)
        {   
            if(m>=c0 and n>=c1)
                return 1;
            else
                return 0;
        }
        else if(dp[i][m][n]!=-1)
            return dp[i][m][n];
        int pick=0;
        if(m>=c0 and n>=c1)
            pick=1+solve(i-1,strs,m-c0,n-c1,adj,dp);
        int nonpick=solve(i-1,strs,m,n,adj,dp);
        return dp[i][m][n]=max(pick,nonpick);
        
    }
    int findMaxForm(vector<string>& strs, int m, int n) {
        int l=strs.size();
        vector<pair<int,int>> adj;
        for(int i=0;i<l;i++)
        {
            int c0=0,c1=0;
            for(char ch:strs[i])
            {
                if(ch=='0')
                    c0++;
                else
                    c1++;
            }
            adj.push_back({c0,c1});
        }
        
        vector<vector<vector<int>>> dp(l,vector<vector<int>>(m+1,vector<int>(n+1,-1)));
        return solve(l-1,strs,m,n,adj,dp);
    }
};
```





### Question :
https://leetcode.com/problems/ones-and-zeroes/

### Reference :
https://youtu.be/GqOmJHQZivw

https://leetcode.com/problems/ones-and-zeroes/discuss/2407670/Simple-C%2B%2B-DP-solution-oror-Memoization

https://youtu.be/qkUZ87NCYSw