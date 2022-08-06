# Check Subset Sum Equal to target
#dp_on_sequences


### Approach 1 (Recursion) :
```cpp
bool solve(int index,int target,vector<int> &arr)
{
    if(target==0)
        return true;
    else if(index==0)
        return (target==arr[0]);
    
    bool pick=false,non_pick;
    if(target>=arr[index])
        pick=solve(index-1,target-arr[index],arr);
    non_pick=solve(index-1,target,arr);
    return (pick || non_pick);
}
bool subsetSumToK(int n, int k, vector<int> &arr) {
    // Write your code here.
    bool ans=solve(n-1,k,arr);
    return ans;
}
```

>**Time Complexity :** O(2^n)
>**Space Complexity :** O(n)

### Approach 2 (Memoization) :
```cpp
bool solve(int index,int target,vector<int> &arr,vector<vector<int>> &dp)
{
    if(target==0)
        return true;
    else if(index==0)
        return (target==arr[0]);
    if(dp[index][target]!=-1)
        return dp[index][target];
    bool pick=false,non_pick;
    if(target>=arr[index])
        pick=solve(index-1,target-arr[index],arr,dp);
    non_pick=solve(index-1,target,arr,dp);
    dp[index][target]=int(pick || non_pick);
    return (pick||non_pick);
}
bool subsetSumToK(int n, int k, vector<int> &arr) {
    // Write your code here.
    vector<vector<int>> dp(n+1,vector<int>(k+1,-1));
    bool ans=solve(n-1,k,arr,dp);
    return ans;
}
```

>**Time Complexity :** ```O(n * target )```
>**Space Complexity :** ```O(n* target) + O(n)```


