# Ninjas Training 2D DP

##### Sample Input 1:

<pre>
2
3
1 2 5 
3 1 1
3 3 3
3
10 40 70
20 50 80
30 60 90
</pre>

##### Sample Output 1:

<pre>
11
210
</pre>

##### Explanation Of Sample Input 1:

<pre>
For the first test case,
One of the answers can be:
On the first day, Ninja will learn new moves and earn 5 merit points. 
On the second day, Ninja will do running and earn 3 merit points. 
On the third day, Ninja will do fighting and earn 3 merit points. 
The total merit point is 11 which is the maximum. 
Hence, the answer is 11.

For the second test case:
One of the answers can be:
On the first day, Ninja will learn new moves and earn 70 merit points. 
On the second day, Ninja will do fighting and earn 50 merit points. 
On the third day, Ninja will learn new moves and earn 90 merit points. 
The total merit point is 210 which is the maximum. 
Hence, the answer is 210.
</pre>

##### Sample Input 2:

<pre>
2
3
18 11 19
4 13 7
1 8 13
2
10 50 1
5 100 11
</pre>

##### Sample Output 2:

<pre>
45
110
</pre>


### Approach 1 (Recursion) :

```cpp
int solve(int lastTask,int day,vector<vector<int>> &points)
{
    if(day==0)
    {
        int maxi=0;
        for(int i=0;i<3;i++)
        {
            if(i!=lastTask)
            {
                maxi=max(maxi,points[0][i]);
            }
        }
        return maxi;
    }
    int maxi=0;
    for(int i=0;i<3;i++)
    {
        if(i!=lastTask)
        {
            int p=points[day][i]+solve(i,day-1,points);
            maxi=max(maxi,p);
        }
    }
    return maxi;
}
int ninjaTraining(int n, vector<vector<int>> &points)
{
    // Write your code here.
    int ans=solve(3,n-1,points);
    return ans;
}
```


### Approach 2 (Memoization) :

```cpp
int solve(int lastTask,int day,vector<vector<int>> &points,vector<vector<int>> &dp)
{
    if(day==0)
    {
        int maxi=0;
        for(int i=0;i<3;i++)
        {
            if(i!=lastTask)
            {
                maxi=max(maxi,points[0][i]);
            }
        }
        return maxi;
    }
    
    if(dp[day][lastTask]!=-1)
        return dp[day][lastTask];
    int maxi=0;
    for(int i=0;i<3;i++)
    {
        if(i!=lastTask)
        {
            int p=points[day][i]+solve(i,day-1,points,dp);
            maxi=max(maxi,p);
        }
    }
    return dp[day][lastTask]=maxi;
}
int ninjaTraining(int n, vector<vector<int>> &points)
{
    // Write your code here.
    vector<vector<int>> dp(n,vector<int>(4,-1));
    
    int ans=solve(3,n-1,points,dp);
    return ans;
}
```


### Approach 3 (Tabulation) :

```cpp
int ninjaTraining(int n, vector<vector<int>> &points)
{
    vector<vector<int>> dp(n,vector<int>(4,0));
    dp[0][0]=max(points[0][1],points[0][2]);
    dp[0][1]=max(points[0][0],points[0][2]);
    dp[0][2]=max(points[0][0],points[0][1]);
    dp[0][3]=max(points[0][0],max(points[0][1],points[0][2]));
    for(int day=1;day<n;day++)
    {
        for(int lastTask=0;lastTask<4;lastTask++)
        {
            for(int currTask=0;currTask<3;currTask++)
            {
                if(currTask!=lastTask)
                {
                    int p=points[day][currTask]+dp[day-1][currTask];
                    dp[day][lastTask]=max(dp[day][lastTask],p);
                }
            }
        }
    }
    return dp[n-1][3];
}
```


### Question :
https://www.codingninjas.com/codestudio/problems/ninja-s-training_3621003


### Reference :
https://youtu.be/AE39gJYuRog?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY

