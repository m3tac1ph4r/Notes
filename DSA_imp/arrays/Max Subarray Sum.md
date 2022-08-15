# Maximum Subarray Sum(Using Kaden's Algo)

### Approach 1 (Using Kaden's Algorithm) :

```cpp
#include <bits/stdc++.h> 
long long maxSubarraySum(int arr[], int n)
{
    long long maxSum=0,currSum=0;
    for(int i=0;i<n;i++)
    {
        currSum+=arr[i];
        if(currSum>maxSum)
            maxSum=currSum;
        if(currSum<0)
            currSum=0;
    }
    return maxSum;
}
```


>**Why traverse loop from n-1 to 0 ?**
>Suppose test case is [-2,1]
>Then the Desired output will be : **1**
>But  **ACUTUAL OUTPUT :** -1
>To fix this we will traverse from n-1 to 0 to overcome this

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


### Question :
https://www.codingninjas.com/codestudio/problems/maximum-subarray-sum_630526?leftPanelTab=0

https://leetcode.com/problems/maximum-subarray/