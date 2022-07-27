# Minimum Time to make rope colorful

Alice has `n` balloons arranged on a rope. You are given a **0-indexed** string `colors` where `colors[i]` is the color of the `ith` balloon.

Alice wants the rope to be **colorful**. She does not want **two consecutive balloons** to be of the same color, so she asks Bob for help. Bob can remove some balloons from the rope to make it **colorful**. You are given a **0-indexed** integer array `neededTime` where `neededTime[i]` is the time (in seconds) that Bob needs to remove the `ith` balloon from the rope.

Return _the **minimum time** Bob needs to make the rope **colorful**_.


**Example 1:**

![[rope_colourful_ex1.png]]

**Input:** colors = "abaac", neededTime = [1,2,3,4,5]
**Output:** 3
**Explanation:** In the above image, 'a' is blue, 'b' is red, and 'c' is green.
Bob can remove the blue balloon at index 2. This takes 3 seconds.
There are no longer two consecutive balloons of the same color. Total time = 3.


**Example 2:**
![[rope_colourful_ex2.png]]

**Input:** colors = "abc", neededTime = [1,2,3]
**Output:** 0
**Explanation:** The rope is already colorful. Bob does not need to remove any balloons from the rope


### Approach :

![[rope_colourful_app.png]]

```cpp
int minCost(string colors, vector<int> &neededTime)
{
    char curr_ch = '*';
    int currTime = 0;
    int ans = 0;

    for (int i = 0; i < colors.length(); i++)
    {
        if (curr_ch == colors[i])
        {
            if (currTime < neededTime[i])
            {
                ans += currTime;
                currTime = neededTime[i];
            }
            else
            {
                ans += neededTime[i];
            }
        }
        else
        {
            curr_ch = colors[i];
            currTime = neededTime[i];
        }
    }
    return ans;
}
```


### Question :
https://leetcode.com/problems/minimum-time-to-make-rope-colorful/

### Reference :

https://youtu.be/ULodF78XRBk