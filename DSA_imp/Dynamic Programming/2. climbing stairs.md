# Climbing Stairs


You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb `1` or `2` steps. In how many distinct ways can you climb to the top?

**Example 1:**

**Input:** n = 2
**Output:** 2
**Explanation:** There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps

**Example 2:**

**Input:** n = 3
**Output:** 3
**Explanation:** There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step

### Approach 1 (Using Recursion) :

```cpp
    int solve(int i,int n)
    {
        if(i==n)
            return 1;
        if(i>n)
            return 0;
        return solve(i+1,n) + solve(i+2,n);
    }
    int climbStairs(int n) {
        int ans;
        ans=solve(0,n);
        return ans;
    }
```


### Approach 2 (Using Tabulation) :
```cpp
    int climbStairs(int n) {
        vector<int> dp(n+1,-1);
        dp[0]=1;
        dp[1]=1;
        for(int i=2;i<=n;i++)
        {
            dp[i]=dp[i-1]+dp[i-2];
        }
        return dp[n];
    }
```

### Approach 3 (Space optimization) :
```cpp
int climbStairs(int n) {
        int prev1=1,prev2=1,curr=1;
        for(int i=2;i<=n;i++)
        {
            curr=prev1+prev2;
            prev2=prev1;
            prev1=curr;
        }
        return curr;
    }
```


### Question :
https://leetcode.com/problems/climbing-stairs/

### Reference :
https://takeuforward.org/data-structure/dynamic-programming-climbing-stairs/