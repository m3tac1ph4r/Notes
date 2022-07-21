# Kaden's Algorithm

Given an integer array `nums`, find the contiguous subarray (containing at least one number) which has the largest sum and return *its sum*.

A **subarray** is a **contiguous** part of an array.

**Example 1:**

**Input:** nums = [-2,1,-3,4,-1,2,1,-5,4]
**Output:** 6
**Explanation:** [4,-1,2,1] has the largest sum = 6.

**Example 2:**

**Input:** nums = [1]
**Output:** 1

**Example 3:**

**Input:** nums = [5,4,-1,7,8]
**Output:** 23

### Approach (Using Kaden's Algorithm) :

```
Initialize:
    max_so_far = INT_MIN
    max_ending_here = 0

Loop for each element of the array
  (a) max_ending_here = max_ending_here + a[i]
  (b) if(max_so_far < max_ending_here)
            max_so_far = max_ending_here
  (c) if(max_ending_here < 0)
            max_ending_here = 0
return max_so_far
```

**Code : **

```cpp
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
            int sum=0,max_sum=INT_MIN;
    for(int i=0;i<nums.size();i++)
    {
        sum+=nums[i];
        if(sum>max_sum)
            max_sum=sum;
        else if(sum<0)
            sum=0;
    }
    sum=0;
    for (int i = nums.size()-1; i >=0; i--)
    {
        sum += nums[i];
        if (sum > max_sum)
            max_sum = sum;
        else if (sum < 0)
            sum = 0;
    }
    return max_sum;
    }
};
```

### Question:

https://leetcode.com/problems/maximum-subarray/
