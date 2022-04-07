# Leetcode container with most water

You are given an integer array `height` of length `n`. There are `n` vertical lines drawn such that the two endpoints of the `ith` line are `(i, 0)` and `(i, height[i])`.

Find two lines that together with the x-axis form a container, such that the container contains the most water.

Return _the maximum amount of water a container can store_.

**Notice** that you may not slant the container.

**Example 1:**
![[container_with_most_water_ex1.png]]

**Example 2:**
**Input:** height = [1,1]
**Output:** 1


### Approach(two pointer approach) :-

1.  We will intialise two pointer left and right. left=0 and right=size()-1. And an integer variable which will store the maximum answer.
2.  Now we will store the water maximum water . Like we will **min(arr[left],arr[right]) * (left-right).** We have done min(arr[left],arr[right])  because water will stored only till minimum of both.
	For ex :
	![[excellidraw.png]]

3. Now if **arr[left]<arr[right]** means there will be chance I can get more height than arr[left] as it can store more water than the current one. So I will increase left by 1
4. Else right++ . Means arr[left]>arr[right]

![[excalidraw2.png]]

As you can see water will be stored more when left will be at 8 and right will be at 6.

```C++
int maxArea(vector<int> &height)
{
    int ans=0;
    int left=0,right=height.size()-1;
    while(left<=right)
    {
        ans=max(ans,(min(height[left],height[right])*(right-left)));
        if(height[left]<height[right])
            left++;
        else
            right--;
    }
    return ans;
}
```

### Question
https://leetcode.com/problems/container-with-most-water/

### References 
https://www.youtube.com/watch?v=e0kiAdtRGk8&ab_channel=AyushiSharma

