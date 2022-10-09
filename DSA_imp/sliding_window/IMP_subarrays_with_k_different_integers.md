# Subarrays with K Different Integers

Given an integer array `nums` and an integer `k`, return _the number of **good subarrays** of_ `nums`.

A **good array** is an array where the number of different integers in that array is exactly `k`.

-   For example, `[1,2,3,1,2]` has `3` different integers: `1`, `2`, and `3`.

A **subarray** is a **contiguous** part of an array.

**Example 1:**

**Input:** nums = [1,2,1,2,3], k = 2
**Output:** 7
**Explanation:** Subarrays formed with exactly 2 different integers: [1,2], [2,1], [1,2], [2,3], [1,2,1], [2,1,2], [1,2,1,2]

**Example 2:**

**Input:** nums = [1,2,1,3,4], k = 3
**Output:** 3
**Explanation:** Subarrays formed with exactly 3 different integers: [1,2,1,3], [2,1,3], [1,3,4].


### Approach (Using Sliding Window and Hashmap) :

1. **Find number of subarrays with at most k different integers**
2. **Find number of subarrays with at most k-1 different integers**
3. **Now subtract (atmost k integer) - (atmost k-1 integer)**

![[subarrays_with_k_different_integer_app.png]]

```cpp
class Solution {
public:
    int atMost(vector<int> &nums,int k,int n)
    {
        int left=0,right=0,max_len=0;
        unordered_map<int,int> mp;
        while(right<n)
        {
            mp[nums[right]]++;
            if(mp.size()>k)
            {
                while(mp.size()>k and left<right)
                {
                    mp[nums[left]]--;
                    if(mp[nums[left]]==0)
                    {
                        mp.erase(mp[nums[left]]);
                        left++;
                        break; // this break is only for if condition
                    }
                    left++;
                }
            }
            max_len+=right-left+1;
            right++;
        }
        return max_len;
    }
    int subarraysWithKDistinct(vector<int>& nums, int k) {
        int n=nums.size();
        int ans1=atMost(nums,k,n);
        int ans2=atMost(nums,k-1,n);
        return ans1-ans2;
    }
};
```


### Question :
https://leetcode.com/problems/subarrays-with-k-different-integers/