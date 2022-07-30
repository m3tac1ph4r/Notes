# Dynamic Programming Introduction

Dynamic Programming can be described as storing answers to various sub-problems to be used later whenever required to solve the main problem.

The two common dynamic programming approaches are:

-   Memoization: Known as the **“top-down”** dynamic programming, usually the problem is solved in the direction of the main problem to the base cases.
-   Tabulation: Known as the **“bottom-up ”** dynamic programming, usually the problem is solved in the direction of solving the base cases to the main problem

**Note:** The base case does not always mean smaller input. It depends upon the implementation of the algorithm.


We will be using the example of Fibonacci numbers here. The following series is called the Fibonacci series:

**0,1,1,2,3,5,8,13,21,…**

We need to find the nth Fibonacci number, where n is based on a 0-based index.

Every ith number of the series is equal to the sum of (i-1)th and (i-2)th number where the first and second number is given as 0 and 1 respectively.


### Approach 1 (Memoization) :

![[fibonacci_intro1.png]]

![[fibonacci_intro2.png]]

We want to compute f(2) as the second call from f(4), but in the recursive tree we had already computed f(2) once (in the first recursive call of f(3) ) Similar is the case with f(3), therefore if we somehow store these values, the first time we calculated it then we can simply find its value in constant time whenever we need it. This technique is called **Memoization**. Here the cases marked in yellow are called overlapping sub-problems and we need to solve them only once during the code execution.

![[fibo_memo3.png]]

```cpp
#include <bits/stdc++.h>

using namespace std;

int f(int n, vector<int>& dp){
    if(n<=1) return n;
    
    if(dp[n]!= -1) return dp[n];
    return dp[n]= f(n-1,dp) + f(n-2,dp);
}


int main() {

  int n=5;
  vector<int> dp(n+1,-1);
  cout<<f(n,dp);
  return 0;
}
```

>**Time Complexity: O(N)**
>**Space Complexity: O(N)**


### Approach 2 (Tabulation) :

Tabulation is a ‘bottom-up’ approach where we start from the base case and reach the final answer that we want.

**Steps to convert Recursive Solution to Tabulation one.**

-   Declare a dp[] array of size n+1.
-   First initialize the base condition values, i.e i=0 and i=1 of the dp array as 0 and 1 respectively.
-   Set an iterative loop which traverses the array( from index 2 to n) and for every index set its value as dp[i-1] + dp[i-2].

```cpp
#include <bits/stdc++.h>

using namespace std;


int main() {

  int n=5;
  vector<int> dp(n+1,-1);
  
  dp[0]= 0;
  dp[1]= 1;
  
  for(int i=2; i<=n; i++){
      dp[i] = dp[i-1]+ dp[i-2];
  }
  cout<<dp[n];
  return 0;
}
```


>**Time Complexity: O(N)**
>**Space Complexity: O(N)**


### Approach 3(Space optimization) :

![[fibo_space_optimize.png]]


```cpp
#include <bits/stdc++.h>

using namespace std;


int main() {

  int n=5;
  
  int prev2 = 0;
  int prev = 1;
  
  for(int i=2; i<=n; i++){
      int cur_i = prev2+ prev;
      prev2 = prev;
      prev= cur_i;
  }
  cout<<prev;
  return 0;
}
```


### Resource :
https://youtu.be/tyB0ztf0DNY?list=PLgUwDviBIf0qUlt5H_kiKYaNSqJ81PMMY
https://takeuforward.org/data-structure/dynamic-programming-introduction/