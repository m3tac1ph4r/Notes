# Find all Pertmutations of String/Array

Given an array `nums` of distinct integers, return _all the possible permutations_. You can return the answer in **any order**.

**Example 1:**

**Input:** nums = [1,2,3]
**Output:** [ [1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]

**Example 2:**

**Input:** nums = [0,1]
**Output:** [ [0,1],[1,0]]

**Example 3:**

**Input:** nums = [1]
**Output:** [ [1]]


### Approach (Backtracking) :

![[permutation_app.png]]

![[permutation_ex2.png]]

We have given the nums array, so we will declare an ans vector of vector that will store all the permutations.

Call a recursive function that starts with zero, nums array, and ans vector.

Declare a map and initialize it to zero and call the recursive function

**Base condition:**

Whenever the index reaches the end take the nums array and put it in ans vector and return.

**Recursion:**

Go from index to n – 1 and swap. Once the swap has been done call recursion for the next state.After coming back from the recursion make sure you re-swap it because for the next element the swap will not take place.

```cpp
void solve(int ind,vector<int> &nums,vector<vector<int>> &ans)
{
    if(ind==nums.size())    // base function
    {
        ans.push_back(nums);
        return;
    }
    for(int i=ind;i<nums.size();i++)
    {
        swap(nums[i],nums[ind]);   
        solve(ind+1,nums,ans);      // recursive call
        swap(nums[i],nums[ind]);    // backtracking step
    }
}
vector<vector<int>> permute(vector<int> &nums)
{
    vector<vector<int>> ans;
    solve(0,nums,ans);
    return ans;
}
```

> **Time Complexity :** O(N! * N)
> **Space Complexity :** O(1)


### Question :

https://leetcode.com/problems/permutations/

### Reference :
https://youtu.be/f2ic2Rsc9pU