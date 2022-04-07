
## Properties of dynamic Programming

1. **OPTIMAL SUBSTRUCTURE : ** If we can write a recurrence relation , then  a problem is said to have optimal substructure.
2. **OVERLAPPING SUBPROBLEM : **If our subproblem repeat , then a problem is said to have overlapping subproblem.

![[dp_1.png]]

As we can see we are computing Fib(1) twice. 
So we can store the value of Fib(1) and when ever it is required again we will use that value.


## Ways to handle Overlapping Subproblem

1. **MEMOIZATION (TOP-DOWN) : ** A lookup table is maintained and checked before computation of any state.  Recursion is involved.
2. **TABULATION (BOTTOM-UP) : ** Solution is built from base. It is an iterative process.



### Example of Dynamic Programming question

#### 1. Fibonacci Series

TIME COMPLEXITY WITHOUT DP :  O(2^n)
TIME COMPLEXITY WITH DP :  O(n)

**Without DP:**
```C++
#include<iostream>
using namespace std;
int fib(int n)
{
	if(n==0)
		return 0;
	else if(n==1)
		return 0;
	else if(n==2)
		return 1;
	return fib(n-1)+fib(n-2);
}
int main()
{
	int n;
	cin>>n;
	cout<<fib(n);
	return 0;
}
```


**With DP:**
1. MEMOIZATION APPROACH:

```C++
#include<iostream>
using namespace std;
int dp[1000];
int fib(int n)
{
	if(n==0)
		return 0;
	else if(n==1)
		return 0;
	else if(n==2)
		return 1;
	else if(dp[n]!=-1)
		return dp[n];
	dp[n]=fib(n-1)+fib(n-2);
	return dp[n];
}
int main()
{
	int n;
	cin>>n;
	for(int i=0;i<n;i++)
		dp[i]=-1;
	cout<<fib(n);
	return 0;
}
```

2. Tabulation

```C++
#include<iostream>
using namespace std;
int main()
{
	int n;
	cin>>n;
	vector<int> dp(n+1);
	dp[0]=0;
	dp[1]=0;
	dp[2]=1;
	for(int i=3;i<=n;i++)
	{
		dp[i]=dp[i-1]+dp[i-2];
	}
	cout<<dp[n];
	return 0;
}
```


--------------------------------------------------------------------

#### 2. Minimum square sum

**Problem:**
Given a number n, your task is to find the minimum number of numbers which sums to n.

**Example : **
n = 26 = 42 + 32 + 12 {3 numbers}
or 26 = 52 + 12 {2 numbers}
So the minimum number of numbers required are 2.


**RECURSION SOLUTION : **

```C++
#include<iostream>
using namespace std;
int minSquare(int n)
{
	if(n==1 || n==2||n==3 || n==0)
		return n;
	int ans=INT_MAX;
	for(int i=1;i*i<=n;i++)
	{
		ans=min(ans,1+minSquare(n-i*i));
	}
	return ans;
}
int main()
{
	int n;
	cin>>n;
	cout<<minSquare(n);
	return 0;
}
```

**WITH DP : **

1. MEMOIZATION APPROACH:
```C++
#include<iostream>
using namespace std;
int dp[1000];
int minSquare(int n)
{
	if(n==1 || n==2||n==3 || n==0)
		return n;
	if(dp[n]!=INT_MAX)
		return dp[n];
	for(int i=1;i*i<=n;i++)
	{
		dp[n]=min(dp[n],1+minSquare(n-i*i));
	}
	return dp[n];
}
int main()
{
	int n;
	cin>>n;
	for(int i=0;i<=n;i++)
	{
		dp[i]=INT_MAX;
	}
	cout<<minSquare(n);
	return 0;
}
```

2. TABULATION APPROACH :

```C++
#include<iostream>
using namespace std;

int main()
{
	int n;
	cin>>n;
	vector<int> dp((n+1),INT_MAX);
	dp[0]=0;
	dp[1]=1;
	dp[2]=2;
	dp[3]=3;
	for(int i;i*i<=n;i++)
	{
		for(int j=0;i*i+j<=n;j++)
		{
			dp[i*i+j]=min(dp[i*i+j],1+dp[j]);
		}
	}
	cout<<dp[n];
	return 0;
}
```


![[dp_2.png]]



