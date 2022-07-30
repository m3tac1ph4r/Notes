# Maximum sum of non adjacent elements

![[DSA_imp/Dynamic Programming/img/max_sum_non_adjacent_1.png]]

![[max_sum_non_adjacent_1 1.png]]

##### Sample Input 1:

<pre>
2
3
1 2 4
4
2 1 4 9
</pre>

##### Sample Output 1:

<pre>
5
11
</pre>

##### Explanation To Sample Output 1:

<pre>
In test case 1, the sum of 'ARR[0]' & 'ARR[2]' is 5 which is greater than 'ARR[1]' which is 2 so the answer is 5.

In test case 2, the sum of 'ARR[0]' and 'ARR[2]' is 6, the sum of 'ARR[1]' and 'ARR[3]' is 10, and the sum of 'ARR[0]' and 'ARR[3]' is 11. So if we take the sum of 'ARR[0]' and 'ARR[3]', it will give the maximum sum of sequence in which no elements are adjacent in the given array/list.
</pre>

##### Sample Input 2:

<pre>
2
5
1 2 3 5 4
9
1 2 3 1 3 5 8 1 9
</pre>

##### Sample Output 2:

<pre>
8
24
</pre>

##### Explanation To Sample Output 2:

<pre>
In test case 1, out of all the possibilities, if we take the sum of 'ARR[0]', 'ARR[2]' and 'ARR[4]', i.e. 8, it will give the maximum sum of sequence in which no elements are adjacent in the given array/list.

In test case 2, out of all the possibilities, if we take the sum of 'ARR[0]', 'ARR[2]', 'ARR[4]', 'ARR[6]' and 'ARR[8]', i.e. 24 so, it will give the maximum sum of sequence in which no elements are adjacent in the given array/list.
</pre>


### Approach (Recursion & Pick/Non Pick) :

![[sum_of_adjacent_element_recursion.png]]

```cpp
int solve(int index,vector<int> nums,int n)
{
    if(index==0)
    {
        return nums[0];
    }
    else if(index<0)
        return 0;
    int pick=nums[index]+solve(index-2,nums,n);
    int non_pick=0+solve(index-1,nums,n);
    
    return max(pick,non_pick);
}
int maximumNonAdjacentSum(vector<int> &nums){
    // Write your code here.
    int sum=0;
    int n=nums.size();
    int ans=solve(n-1,nums,n);
    return ans;
}
```


### Approach 2 (Recursion + Memoization) :
```cpp
    int solve(int index,vector<int> &nums,vector<int> &dp)
    {
        if(index==0)
            return nums[0];
        if(index<0)
            return 0;
        else if(dp[index]!=-1)
            return dp[index];
        
        int pick=nums[index]+solve(index-2,nums,dp);
        int non_pick=0+solve(index-1,nums,dp);
        return dp[index]=max(pick,non_pick);
    }
    int rob(vector<int>& nums) {
        int n=nums.size();
        vector<int> dp(n+1,-1);
        int ans=solve(n-1,nums,dp);
        return ans;
    }
```

>**Time Complexity :** O(N)
>**Space Complexity :** O(N) + O(N)

### Approach 3 (Tabulation) :

![[max_sum_adjacent_tabulation.png]]

```cpp
int maximumNonAdjacentSum(vector<int> &nums){
    // Write your code here.
    
    int sum=0;
    int n=nums.size();
    vector<int> dp(n+1,0);
    dp[0]=nums[0];
    for(int i=1;i<n;i++)
    {
        int pick=nums[i];
        if(i>1)
            pick+=dp[i-2];
        int non_pick=dp[i-1];
        dp[i]=max(pick,non_pick);
    }
    return dp[n-1];
}
```

>**Time Complexity :** O(N)
>**Space Complexity :** O(N)



### Approach 3(Space Optimization) :

![[non_adjacent_element_space_optimize.png]]

```cpp
int maximumNonAdjacentSum(vector<int> &nums){

    int n=nums.size();
    int prev1=nums[0];
    int prev2=0;
    for(int i=1;i<n;i++)
    {
        int pick=nums[i];
        if(i>1)
            pick+=prev2;
        int non_pick=prev1;
        int curr=max(pick,non_pick);
        prev2=prev1;
        prev1=curr;
    }
    return prev1;
}
```

>**Time Complexity :** O(N)
>**Space Complexity :** O(1)


### Question :
https://www.codingninjas.com/codestudio/problems/maximum-sum-of-non-adjacent-elements_843261
https://leetcode.com/problems/house-robber/


### References :
https://youtu.be/m9-H6AUBLgY?list=PLDzeHZWIZsTomOPnCiU3J95WufjE36wsb
https://youtu.be/GrMBfJNk_NY?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY