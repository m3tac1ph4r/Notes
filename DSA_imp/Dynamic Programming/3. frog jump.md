# Frog Jump


##### Sample Input 1:

<pre>
2
4

10 20 30 10
3
10 50 10
</pre>

##### Sample Output 1:

<pre>
20
0
</pre>

##### Explanation Of Sample Input 1:

<pre>
For the first test case,
The frog can jump from 1st stair to 2nd stair (|20-10| = 10 energy lost).
Then a jump from the 2nd stair to the last stair (|10-20| = 10 energy lost).
So, the total energy lost is 20 which is the minimum. 
Hence, the answer is 20.

For the second test case:
The frog can jump from 1st stair to 3rd stair (|10-10| = 0 energy lost).
So, the total energy lost is 0 which is the minimum. 
Hence, the answer is 0.
</pre>

##### Sample Input 2:

<pre>
2
8
7 4 4
2 6 6 3 4 
6
4 8 3 10 4 4 
</pre>

##### Sample Output 2:

<pre>
7
2
</pre>


### Approach 1 (Memoization) :

```cpp
int solve(int index,vector<int> heights,vector<int> &dp)
{
    if(index==0)
        return 0;
    if(dp[index]!=-1)
        return dp[index];
    int left=solve(index-1,heights,dp)+abs(heights[index]-heights[index-1]);
    int right=INT_MAX;
    if(index>1)
        right=solve(index-2,heights,dp)+abs(heights[index]-heights[index-2]);
    return dp[index]=min(left,right);
}
int frogJump(int n, vector<int> &heights)
{
    // Write your code here.
    vector<int> dp(n+1,-1);
    int ans=solve(n-1,heights,dp);
    return ans;
}
```

>**Time Complexity :** O(N)
>**Space Complexity :** O(N) + O(N) {Recursion + DP ARRAY}

### Approach 2 (Tabulation) :

```cpp
int frogJump(int n, vector<int> &heights)
{
    // Write your code here.
    vector<int> dp(n+1,-1);
    dp[0]=0;
    dp[1]=abs(heights[0]-heights[1]);
    for(int i=2;i<n;i++)
    {
        int left=dp[i-1]+abs(heights[i]-heights[i-1]);
        int right=dp[i-2]+abs(heights[i]-heights[i-2]);
        dp[i]=min(left,right);
    }
    return dp[n-1];
}
```

>**Time Complexity :** O(N)
>**Space Complexity :** O(N) {DP ARRAY}


### Space Optimization :
```cpp
int frogJump(int n, vector<int> &heights)
{
    // Write your code here.
    int prev1=0;
    int prev2=abs(heights[0]-heights[1]);
    for(int i=2;i<n;i++)
    {
        int left=prev2+abs(heights[i]-heights[i-1]);
        int right=prev1+abs(heights[i]-heights[i-2]);
        int curr=min(left,right);
        prev1=prev2;
        prev2=curr;
    }
    return prev2;
}
```

>**Time Complexity :** O(N)
>**Space Complexity :** O(1)

### Question :
https://www.codingninjas.com/codestudio/problems/frog-jump_3621012

### Reference :
https://youtu.be/EgG3jsGoPvQ?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY