

## We can use window sliding technique instead of nested loop

We can use  sliding window technique to convert nested for loop into one and decrease the complexity of the problem.

**How to identify when to use sliding window technique ?**
 -    The problem will involve a data structure that is ordered and iterable like an array or a string
 -    You are looking for some subrange in that array/string, like a longest, shortest or target value.
 -    There is an apparent native or brute force solution that runs in O(N²), O(2^N) or some other large time complexity.


```
[a b c d e f g h]
```

a sliding window of size 3 would run over it like

```
[a b c]
  [b c d]
    [c d e]
      [d e f]
        [e f g]
          [f g h]
```



There are two type of sliding window :
1. Fixed window length k: the length of the window is fixed and it asks you to find something in the window such as the maximum sum of all windows, the maximum or median number of each window
2.  Two pointers + criteria: the window size is not fixed, usually it asks you to find the subarray that meets the criteria, for example, given an array of integers, find the number of subarrays whose sum is equal to a target value.


**Ques 1: We have an array of n elements and an integer k . We have to find the minimum sum of subarray of k elements**
**Input :**  
A[]= {-2,10,1,3,2,-1,4,5}
k=3
**OUTPUT : **  4
**Explanation: ** Elements of subarray will be {3,2,-1} which give sum as 4

**Ans 1: ** As this question is having a fixed value k so it comes in 1st category of sliding window. 

```C++
#include <iostream>
using namespace std;
int main() {
    int A[]= {-2,10,1,3,2,-1,4,5};
    int n=8;
    int k=3;
    int sum=0,ans=100;
    for(int i=0;i<k;i++)
        sum+=A[i];
    ans=min(ans,sum);
    for(int i=1;i<n-k+1;i++)
    {
        sum=sum-A[i-1];
        sum=sum+A[i+k-1];
        ans=min(ans,sum);
    }
    cout<<ans<<endl;
    return 0;
}
```


**Ques 2:   We have given an array of n elements and also a integer X. So we have to find a triplet in that array which is equal to X. If there is any triplet then print 1.
It is not mandatory that triplet should be subarray .**

**INPUT : ** 
A[]={1,4,45,6,10,8}
X= 13
**OUTPUT :** 
1
**Explanation :**
Triplet = {1,4,8} = 13

**Ans 2 : **  So this questions comes under 2nd sliding window technique. It means we will use two pointer technique in this question.

```C++
#include<bits/stdc++.h>
using namespace std;
#define ll long long
int main()
{
int A[]={1,4,45,6,10,8};
int n=sizeof(A)/sizeof(A[0]);
int i=0;
int X=13;
int sum=0;
int ans=0;
sort(A,A+n);
for(i=0;i<n;i++)
{
	int j=n-1;
	int l=i+1;
	while (l<j)
	{
		sum=A[i]+A[j]+A[l];
		if(sum==X)
		{
			ans=1;
			break;
		}
		else if(sum<X)
			l++;
		else
			j--;
	}
}
cout<<ans<<endl;
return 0;
}
```


