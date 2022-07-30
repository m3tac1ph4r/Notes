# Minimum Cost of Climbing Stairs

You are given an integer array `cost` where `cost[i]` is the cost of `ith` step on a staircase. Once you pay the cost, you can either climb one or two steps.

You can either start from the step with index `0`, or the step with index `1`.

Return _the minimum cost to reach the top of the floor_.

**Example 1:**

**Input:** cost = [10,15,20]
**Output:** 15
**Explanation:** You will start at index 1.
- Pay 15 and climb two steps to reach the top.
The total cost is 15.

**Example 2:**

**Input:** cost = [1,100,1,1,1,100,1,1,100,1]
**Output:** 6
**Explanation:** You will start at index 0.
- Pay 1 and climb two steps to reach index 2.
- Pay 1 and climb two steps to reach index 4.
- Pay 1 and climb two steps to reach index 6.
- Pay 1 and climb one step to reach index 7.
- Pay 1 and climb two steps to reach index 9.
- Pay 1 and climb one step to reach the top.
The total cost is 6.

![[minimum_cost_climbing_recursion.png]]


### Approach 1 (Using Memoization) :

```cpp
    int solve(int n,vector<int> cost,vector<int> &dp)
    {
        if(n==0)
            return cost[0];
        if(n==1)
            return cost[1];
        else if(dp[n]!=-1)
            return dp[n];
        
        dp[n]=cost[n]+min(solve(n-1,cost,dp),solve(n-2,cost,dp));
        return dp[n];
    }
    int minCostClimbingStairs(vector<int>& cost) {
        vector<int> dp(cost.size()+1,-1);
        int n=cost.size();
        int ans=min(solve(n-1,cost,dp),solve(n-2,cost,dp));
        return ans;
    }
```

>**Time Complexity :** O(N)
>**Space Complexity :** O(N) + O(N) {Recursion + DP ARRAY}

### Approach 2 (Using Tabulation) :

```cpp
    int minCostClimbingStairs(vector<int>& cost) {
        int n=cost.size();
        vector<int> dp(n+1,-1);
        
        dp[0]=cost[0];
        dp[1]=cost[1];
        for(int i=2;i<n;i++)
        {
            dp[i]=cost[i]+min(dp[i-1],dp[i-2]);
        }
        return min(dp[n-1],dp[n-2]);
    }
```

>**Time Complexity :** O(N)
>**Space Complexity :** O(N)

### Question :
https://leetcode.com/problems/min-cost-climbing-stairs/

### Reference :
https://youtu.be/S31W3kohFDk?list=PLDzeHZWIZsTomOPnCiU3J95WufjE36wsb