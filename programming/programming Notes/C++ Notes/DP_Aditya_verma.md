
# Dynamic Programming

Dynamic programming is used to optimize by using more storage.
Mostly Dynamic programming is used where recursion is used.

**When we can use dynamic programming ?**
1. When we have choice
2. When we have to optimize like largest,smallest,minimum,maximum etc.

We can achieve DP by two ways:
1. Memoization (Bottom-UP ) approach using recursion
2. Top Down approach
 

Before DP we have to understand recursion

### Recursion
How to write recursion base case ?

We have to find the smallest valid value which can be for our question. That would be our base case.

Firstly we will write **Recursive code -> Memoization -> Top Down (optional)**

**How to make matrix for DP ?**
We have to find which constraint is changing its value in recursive code. It can be two different values also.
Ex : In fibonacci n is decreased in recursive call. So we will make 2D matrix size.


--------------------------------------------------------------------


# Most Popular Problems of DP

**1. 01 Knapsack Problem : **

**Problem statement : **
Given weights and values of n items, put these items in a knapsack of capacity W to get the maximum total value in the knapsack. In other words, given two integer arrays val[0..n-1] and wt[0..n-1] which represent values and weights associated with n items respectively. Also given an integer W which represents knapsack capacity, find out the maximum value subset of val[] such that sum of the weights of this subset is smaller than or equal to W. You cannot break an item, either pick the complete item or don’t pick it (0-1 property).

**Recursive Approach :**

**Function Definition :**
```C++
int knapsack(int wt[],int val[],int W,int n)
{
}
```

**Structure of recursion code : **
int knapsack(int wt[],int val[],int W,int n)
{
	Base Case
	Choice Diagram
}

Choice Diagram :

![[01 Knapsack_1.png]]


Base Condition :
**Base Condition -> Think of the smallest valid Input**
So smallest valid input will be n=0 and W=0 and it will return 0 because profit will be 0.

**Code:**
```C++
int knapsack(int wt[],int val[],int W,int n)
{
 if(n==0 || W==0)
 	return 0;
 if(wt[n-1]<=W)
 	return max(val[n-1]+knapsack(wt,val,W-wt[n-1],n-1),knapsack(wt,val,W,n-1));
 else if(wt[n-1]>W)
 	return knapsack(wt,val,W,n-1);
}
```



**Memoization Approach : **
This is one of the DP approach. In this we will make 2D matrix. 
Memoization -> Recursive approach + 3 lines

**What will be the	 size of matrix ?**
Basically how many input we have ? 
wt[],val[],W,n
And all of these how many are changing its value in recursive function. Only two W and n. So this will be the size of our matrix
```C++
int dp[n+1][w+1]
```

We will intialize the array with -1.
We can use **memset(dp,-1,sizeof(dp))** or for loop

**Code : **
```C++
int dp[102][1002]		// 102 and 1002 are maximum values of n and W
memset(dp,-1,sizeof(dp));
int knapsack(int wt[],int val[],int W,int n)
{
 if(n==0 || W==0)
 	return 0;
 if(dp[n][W]!=-1)
 	return dp[n][W];
 if(wt[n-1]<=W)
 	return dp[n][W] = max(val[n - 1] + knapsack(wt, val, W - wt[n - 1], n - 1), knapsack(wt, val, W, n - 1));
 else if(wt[n-1]>W)
 	return dp[n][W]=knapsack(wt,val,W,n-1);
}
```


**Converting memoization to top down approach : - **

In top down approach we will convert recursion to iterative.

**STEPS TO CHANGE MEMOIZATION TO TOP DOWN APPROACH : **
1. Intialization
2. Change recursive_function(recursive calls) to iterative.

**What value we will intialize and where ?**
We will see the recursive function base condition.
```C++
	if(n==0 || W==0)
		return 0;
```

As we can see when there will be n equal to 0 then we will mark zero . And when W equal to 0 then we will mark 0.
So in the matrix we will intialize first row and coloumn with 0 respectively. 

Equations of top down approch:
```C++
if(wt[n-1]<=W)
	t[n][w]=max(val[n-1]+t[n-1][W-wt[n-1]],t[n-1][w]);
else
	t[n][w]=t[n-1][w]
```

Now we will convert n,w into i,j

**Code : **
```C++
int dp[1000][1000];
int knapsack(int wt[],int val[],int W,int n)
{
	for(int i=0;i<n+1;i++)
	{
		dp[i][0]=0;
	}
	for(int i=0;i<W+1;i++)
	{
		dp[0][i]=0;
	}
	for(int i=1;i<n+1;i++)
	{
		for(int j=1;j<W+1;j++)
		{
			if(wt[n-1]<=j)
				dp[i][j]=max(val[i-1]+dp[i-1][W-wt[i-1]],dp[i-1][j]);
			else
				dp[i][j]=dp[i-1][j];
		}
	}
}
```


