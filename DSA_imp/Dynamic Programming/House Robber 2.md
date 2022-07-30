# House Robber 2

>**Similar as maximum sum of non adjacent elements**
>[[maximum sum of non adjacent elements]]

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are **arranged in a circle.** That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have a security system connected, and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given an integer array `nums` representing the amount of money of each house, return _the maximum amount of money you can rob tonight **without alerting the police**_.

**Example 1:**

**Input:** nums = [2,3,2]
**Output:** 3
**Explanation:** You cannot rob house 1 (money = 2) and then rob house 3 (money = 2), because they are adjacent houses.

**Example 2:**

**Input:** nums = [1,2,3,1]
**Output:** 4
**Explanation:** Rob house 1 (money = 1) and then rob house 3 (money = 3).
Total amount you can rob = 1 + 3 = 4.

**Example 3:**

**Input:** nums = [1,2,3]
**Output:** 3

### Approach (Tabualtion) :

As I previously said it is same as the [[maximum sum of non adjacent elements]] but in this question
**index 0 and index (n-1)** is also a adjacent neighbour. So we cannot take index 0 and index n-1 together.

**How we will know that have to take index 0 or not. OR how we will know that we have to take index n-1 in sum or not.**

So we will create two arrays :
1. 1 to n-1 (Taking whole array excluding 0 index element)
2. 0 to n-2 (Taking whole array excluding n-1 index element)

```cpp
int solve(vector<int> &nums){
    int sum=0;
    int n=nums.size();
    vector<int> dp(n+1,0);
    dp[0]=nums[0];
    for(int i=1;i<n;i++)
    {
        int pick=nums[i];
        if(i>1)
            pick+=dp[i-2];
        int non_pick=dp[i-1];
        dp[i]=max(pick,non_pick);
    }
    return dp[n-1];
}
    int rob(vector<int>& nums) {
        vector<int> temp1,temp2;
        int n=nums.size();
        if(n==1)
            return nums[0];
        for(int i=0;i<n;i++)
        {
            if(i!=0)
                temp1.push_back(nums[i]);
            if(i!=n-1)
                temp2.push_back(nums[i]);
        }
        int ans1=solve(temp1);
        int ans2=solve(temp2);
        
        return max(ans1,ans2);
    }
```


### Question :
https://leetcode.com/problems/house-robber-ii/

### Reference :
https://youtu.be/3WaxQMELSkw?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY