
# Minimum Number of Coins

##### Sample Input 1 :

<pre>
2
3 7
1 2 3
1 0
1
</pre>

##### Sample Output 1 :

<pre>
 3
 0
</pre>

##### Explanation For Sample Output 1:

<pre>
For the first test case,
Way 1 - You can take 4 elements  [2, 2, 2, 1] as 2 + 2 + 2 + 1 = 7.
Way 2 - You can take 3 elements  [3, 3, 1] as 3 + 3 + 1 = 7.
Here, you can see in Way 2 we have used 3 coins to reach the target sum of 7.
Hence the output is 3.

For the second test case,
Way 1 - You can take 3 elements  [1, 1, 1] as 1 + 1 + 1  = 3.
Way 2 - You can take 2 elements  [2, 1] as 2 + 1 = 3.
Here, you can see in Way 2 we have used 2 coins to reach the target sum of 7.
Hence the output is 2.
</pre>

##### Sample Input 2 :

<pre>
2
3 4
12 1 3
2 11
2 1
</pre>

##### Sample Output 2 :

<pre>
2
6 
</pre>

### Approach 1 (Recursion) :


```cpp
int solve(int k,vector<int> &num,int target)
{
    if(target==0)
        return 0;
    if(target<0)
        return INT_MAX;
    int mini=INT_MAX;
    for(int i=0;i<k;i++)
    {
        int ans=solve(k,num,target-num[i]);
        if(ans!=INT_MAX)
            mini=min(mini,1+ans);
    }
    return mini;
}
int minimumElements(vector<int> &num, int x)
{
    int k=num.size();
    int ans=solve(k,num,x);
    if(ans==INT_MAX)
        return -1;
    return ans;
}
```


### Approach 2 (Memoization) :

```cpp
int solve(int k,vector<int> &num,int target,vector<int> &dp)
{
    if(target==0)
        return 0;
    if(target<0)
        return INT_MAX;
    if(dp[target]!=-1)
        return dp[target];
    int mini=INT_MAX;
    for(int i=0;i<k;i++)
    {
        int ans=solve(k,num,target-num[i],dp);
        if(ans!=INT_MAX)
            mini=min(mini,1+ans);
    }
    dp[target]=mini;
    return mini;
}
int minimumElements(vector<int> &num, int x)
{
    
    int k=num.size();
    vector<int> dp(x+1,-1);
    int ans=solve(k,num,x,dp);
    if(ans==INT_MAX)
        return -1;
    return ans;
}
```


### Approach 3 (Tabulation) :

![[minimum_number_of_coins_tabulation.png]]

```cpp
int minimumElements(vector<int> &num, int x)
{
    
    int k=num.size();
    vector<int> dp(x+1,INT_MAX);
    dp[0]=0;
    for(int i=1;i<=x;i++)
    {
        for(int j=0;j<k;j++)
        {
            if(i-num[j]>=0 and dp[i-num[j]]!=INT_MAX)
            {
                dp[i]=min(dp[i],1+dp[i-num[j]]);
            }
        }
    }
    if(dp[x]!=INT_MAX)
        return dp[x];
    else
        return -1;
}
```



### Question :
https://www.codingninjas.com/codestudio/problems/minimum-elements_3843091

### Reference :
https://youtu.be/A3FHNCAkhxE?list=PLDzeHZWIZsTomOPnCiU3J95WufjE36wsb