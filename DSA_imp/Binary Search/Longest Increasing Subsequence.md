# Longest Increasing Subsequence :

Given an integer array `nums`, return the length of the longest strictly increasing subsequence.

A **subsequence** is a sequence that can be derived from an array by deleting some or no elements without changing the order of the remaining elements. For example, `[3,6,2,7]` is a subsequence of the array `[0,3,1,6,2,2,7]`.

**Example 1:**

**Input:** nums = [10,9,2,5,3,7,101,18]
**Output:** 4
**Explanation:** The longest increasing subsequence is [2,3,7,101], therefore the length is 4.

**Example 2:**

**Input:** nums = [0,1,0,3,2,3]
**Output:** 4

**Example 3:**

**Input:** nums = [7,7,7,7,7,7,7]
**Output:** 1

### Approach 1 (Binary Search and lower bound) :

**Lower Bound means just bigger than that element.**
https://www.geeksforgeeks.org/lower_bound-in-cpp/

![[longest_increasing_subsequence.png]]

```cpp
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        vector<int> temp;
        temp.push_back(nums[0]);
        int len=1;
        for(int i=1;i<nums.size();i++)
        {
            if(nums[i]>temp.back())
            {
                temp.push_back(nums[i]);
                len++;
            }
            else
            {
                int index=lower_bound(temp.begin(),temp.end(),nums[i])-temp.begin();
                temp[index]=nums[i];
            }
        }
        return len;
    }
};
```

>**Time Complexity :** O(n* logn)
>**Space Complexity :** O(n)


### Question :
https://leetcode.com/problems/longest-increasing-subsequence/

### Reference :
https://takeuforward.org/data-structure/longest-increasing-subsequence-binary-search-dp-43/
https://youtu.be/on2hvxBXJH4