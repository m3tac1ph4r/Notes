# Peak element in unsorted array

A peak element is an element that is strictly greater than its neighbors.

Given an integer array `nums`, find a peak element, and return its index. If the array contains multiple peaks, return the index to **any of the peaks**.

You may imagine that `nums[-1] = nums[n] = -∞`.

You must write an algorithm that runs in `O(log n)` time.

**Example 1:**

**Input:** nums = [1,2,3,1]
**Output:** 2
**Explanation:** 3 is a peak element and your function should return the index number 2.

**Example 2:**

**Input:** nums = [1,2,1,3,5,6,4]
**Output:** 5
**Explanation:** Your function can return either index number 1 where the peak element is 2, or index number 5 where the peak element is 6.

### Approach :

1. As we have to find the element whose both adjacent neighbours are smaller than the arr[mid]
2. Suppose you found an arr[mid] whose arr[mid-1] and arr[mid+1] are smaller than arr[mid] return mid
3. If you found arr[mid-1] is greater than arr[mid] means if we choose arr[mid-1] than arr[mid] will be smaller. Then there is a more chance of peak element and we have to find one more neighbour
4. Else if you found arr[mid+1] is greater than arr[mid] mean if we choose arr[mid+1] then arr[mid] will be smaller. Then there is a more chance of peak element and we have to find oen more neighbour

```cpp
int findPeakElement(vector<int> nums)
{
    int low=0,high=nums.size()-1;
    while (low<=high)
    {
        int mid=low+(high-low)/2;
        if(mid>0 and mid<nums.size()-1)
        {
            if(nums[mid]>nums[mid-1] and nums[mid]>nums[mid+1])
                return mid;
            else if(nums[mid-1]>nums[mid])
            {
                high=mid-1;
            }
            else if(nums[mid+1]>nums[mid])
                low=mid+1;
        }
        else if(mid==0)
        {
            if(nums[0]>nums[1])
                return 0;
            else
                return 1;
        }
        else if (mid == nums.size()-1)
        {
            if (nums[nums.size()-1]>nums[nums.size()-2])
                return nums.size()-1;
            else
                return nums.size()-2;
        }
    }
    return -1;
}
```

### Question :

https://leetcode.com/problems/find-peak-element/
https://leetcode.com/problems/peak-index-in-a-mountain-array/
