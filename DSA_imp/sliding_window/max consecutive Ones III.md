# Max Consecutive Ones III

Given a binary array `nums` and an integer `k`, return _the maximum number of consecutive_ `1`_'s in the array if you can flip at most_ `k` `0`'s.

**Example 1:**

**Input:** nums = [1,1,1,0,0,0,1,1,1,1,0], k = 2
**Output:** 6
**Explanation:** [1,1,1,0,0,**1**,1,1,1,1,**1**]
Bolded numbers were flipped from 0 to 1. The longest subarray is underlined.

**Example 2:**

**Input:** nums = [0,0,1,1,0,0,1,1,1,0,1,1,0,0,0,1,1,1,1], k = 3
**Output:** 10
**Explanation:** [0,0,1,1,**1**,**1**,1,1,1,**1**,1,1,0,0,0,1,1,1,1]
Bolded numbers were flipped from 0 to 1. The longest subarray is underlined.


### Approach 1 (Using Sliding)

```cpp
class Solution {
public:
    int longestOnes(vector<int>& nums, int k) {
        int left=0,right=0;
        int ans=0,zeroCount=0;
        while(left<=right and right<nums.size())
        {
            if(nums[right]==0)
                zeroCount++;
            while(zeroCount>k)
            {
                if(nums[left]==0)
                    zeroCount--;
                left++;
            }
            ans=max(ans,right-left+1);
            right++;
        }
        return ans;
    }
};
```


### Question :
https://leetcode.com/problems/max-consecutive-ones-iii/