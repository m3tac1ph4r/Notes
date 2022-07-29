# Subset II

Given an integer array `nums` that may contain duplicates, return _all possible subsets (the power set)_.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

**Example 1:**

**Input:** nums = [1,2,2]
**Output:** [ [],[1],[1,2],[1,2,2],[2],[2,2]]

**Example 2:**

**Input:** nums = [0]
**Output:** [ [],[0]]


### Approach :

![[subset_2_app.png]]


1. We will start with an empty array.
2. Add the array in the answer. Then start a for loop from index i to n
3. Then insert ith element in array and do a recursion call by taking ith element.
4. **To not insert duplicate elements** you will skip all the same adjacent elements

```cpp
void solve(int indx, vector<int> &nums, vector<int> &temp, vector<vector<int>> &ans)
{
    ans.push_back(temp);
    for (int i = indx; i < nums.size(); i++)
    {
        if (i != indx and nums[i] == nums[i - 1])
            continue;
        temp.push_back(nums[i]);
        solve(i + 1, nums, temp, ans);
        temp.pop_back();
    }
}
vector<vector<int>> subsetsWithDup(vector<int> &nums)
{
    vector<vector<int>> ans;
    vector<int> temp;
    int i = 0;
    sort(nums.begin(), nums.end());
    solve(i, nums, temp, ans);
    return ans;
}
```


### Question :
https://leetcode.com/problems/subsets-ii/

### Reference :
https://youtu.be/RIn3gOkbhQE