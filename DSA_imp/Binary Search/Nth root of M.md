# Nth root of M

Problem Statement

Suggest Edit

#### You are given two positive integers N and M. You have to find the Nth root of M i.e. M^(1/N).

##### Note:

```
N'th root of an integer M is a real number, which when raised to the power N gives M as a result.

N'th root of the M should be correct up to 6 decimal places.
```

##### Sample Input 1:

```
1
3 27
```

##### Sample Output 1:

```
3.000000
```

##### Explanation For Sample Input 1:

```
3rd Root of 27 is 3.000000, as (3.000000)^3 is equal to 27.
```

##### Sample Input 2:

```
1
4 69
```

##### Sample Output 2:

```
2.882121
```


### Approach (Binary Search) :

**How we thought to use Binary Search ?**
<pre>
Binary search can be implemented in any search space which is monotonic(strictly increasing or decreasing) in nature.

Suppose N=3 and M=27

1*1*1 = 1
2*2*2 = 8
3*3*3 = 9
4*4*4 = 64

As you can see it is monotonic in nature
</pre>

> 1. Range will be [low,high]
> 2. Then we will find the mid
> 3. If mid^n > M then we will update the high=mid [low,mid]
> 4. else low=mid [mid,high]
> 5. We will check that (high-low > 1e-7) to find upto answer upto 7 decimal places


![[nth_root_m_appraoch.png]]

```C++
double multiply(double number, int n)
{
    double ans = 1.0;
    for (int i = 1; i <= n; i++)
    {
        ans = ans * number;
    }
    return ans;
}
double findNthRootOfM(int n,long long m)
{
    double low=1,high=m+1;
    double eps = 1e-8;
    while ((high - low) > eps)
    {
        double mid = (low + high) / 2.00;
        if (multiply(mid, n) < m)
        {
            low = mid;
        }
        else
        {
            high = mid;
        }
    }
    return low;
}
```

### Resources :

https://youtu.be/WjpswYrS2nY

### Question :

https://www.codingninjas.com/codestudio/problems/nth-root-of-m_1062679