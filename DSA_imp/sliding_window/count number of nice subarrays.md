# Count Number of Nice Subarrays


Given an array of integers `nums` and an integer `k`. A continuous subarray is called **nice** if there are `k` odd numbers on it.

Return _the number of **nice** sub-arrays_.

**Example 1:**

**Input:** nums = [1,1,2,1,1], k = 3
**Output:** 2
**Explanation:** The only sub-arrays with 3 odd numbers are [1,1,2,1] and [1,2,1,1].

**Example 2:**

**Input:** nums = [2,4,6], k = 1
**Output:** 0
**Explanation:** There is no odd numbers in the array.

**Example 3:**

**Input:** nums = [2,2,2,1,2,2,1,2,2,2], k = 2
**Output:** 16


### Approach (Using Hashmap) :

We will convert all the even number to 0 and odd numbers to 1. 
Then problem will be like [[count binary subarrays with sum]]

```cpp
class Solution {
public:
    int numberOfSubarrays(vector<int>& nums, int k) {
        int n=nums.size();
        for(int i=0;i<n;i++)
        {
            if(nums[i]%2==0)
                nums[i]=0;
            else
                nums[i]=1;
        }
        // Now array would be [1,1,0,1,1] And now we will find the number of subrray
        // equal to sum k
        
        unordered_map<int,int> mp;
        mp[0]=1;
        int ans=0,sum=0;
        
        for(int i=0;i<n;i++)
        {
            sum+=nums[i];
            if(mp.find(sum-k)!=mp.end())
            {
                ans+=mp[sum-k];
            }
            mp[sum]++;   
        }
        return ans;
    }
};
```


### Question :
https://leetcode.com/problems/count-number-of-nice-subarrays/

### Reference :
https://youtu.be/atUJS7ArOY0