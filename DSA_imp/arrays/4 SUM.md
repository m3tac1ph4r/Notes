# 4 SUM

Given an array `nums` of `n` integers, return *an array of all the **unique** quadruplets* `[nums[a], nums[b], nums[c], nums[d]]` such that:

- `0 <= a, b, c, d < n`
- `a`, `b`, `c`, and `d` are **distinct**.
- `nums[a] + nums[b] + nums[c] + nums[d] == target`

You may return the answer in **any order**.

**Example 1:**

**Input:** nums = [1,0,-1,0,-2,2], target = 0
**Output:** [[-2,-1,1,2],[-2,0,0,2],[-1,0,0,1]]

**Example 2:**

**Input:** nums = [2,2,2,2,2], target = 8
**Output:** [[2,2,2,2]]

### Approach (Using 4 pointers)

1. We will use two for loops :

   - i=0 to n-3
   - j=i+1 to n-2

2. We will store _target2=target-nums[i]-nums[j]_ Then we will use **l** and **k**
   - l=j+1
   - k=n-1
3. Now we will check

   - _nums[l]+nums[k]< target2_ : l++
   - _nums[l]+nums[k] > target2_ : k--
   - _nums[l]+nums[k]== target2_ : store nums[i],nums[j],nums[l],nums[k] in an array

4. Then skip all the duplicates.

```cpp
vector<vector<int>> fourSum(vector<int> &nums,int target)
{
    vector<vector<int>> ans;
    sort(nums.begin(),nums.end());
    int n=nums.size();
    for(int i=0;i<n;i++)
    {
        for(int j=i+1;j<n;j++)
        {
            int target2=target-nums[i]-nums[j];
            int l=j+1,k=n-1;
            while (l<k)
            {
                int sum=nums[l]+nums[k];
                if(sum<target2)
                    l++;
                else if(sum>target2)
                    k--;
                else
                {
                    vector<int> tmp(4);
                    tmp[0]=nums[i];
                    tmp[1]=nums[j];
                    tmp[2]=nums[l];
                    tmp[3]=nums[k];
                    ans.push_back(tmp);
                    // remove the duplicates of num[l]
                    while(l<k and nums[l]==tmp[2])
                        l++;
                    // remove the duplicates of num[k]
                    while(l<k and nums[k]==tmp[3])
                        k--;
                }
            }
            // remove the duplicates of num[j]
            while (j + 1 < n and nums[j] == nums[j + 1])
                j++;
        }
        // remove the duplicates of num[i]
        while(i+1<n and nums[i]==nums[i+1])
            i++;
    }
    return ans;
}
```

### Question :

https://leetcode.com/problems/4sum/

### References :

https://youtu.be/OZdOHiodh_c
