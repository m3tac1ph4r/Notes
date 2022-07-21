# POW(x,n)

Implement [pow(x, n)](http://www.cplusplus.com/reference/valarray/pow/), which calculates `x` raised to the power `n` (i.e., xⁿ).

**Example 1:**

**Input:** x = 2.00000, n = 10
**Output:** 1024.00000

**Example 2:**

**Input:** x = 2.10000, n = 3
**Output:** 9.26100

**Example 3:**

**Input:** x = 2.00000, n = -2
**Output:** 0.25000
**Explanation:** 2-2 = 1/22 = 1/4 = 0.25

**Constraints:**

- `-100.0 < x < 100.0`
- `-231 <= n <= 231-1`
- `-104 <= xn <= 104`

![[pow_x_n_appraoch.png]]

```cpp
double myPow(double x,int n)
{
    double ans = 1.0;
    long long i=abs(n);
    while(i>0)
    {
        if(i%2!=0)
        {
            ans=ans*x;
            i=i-1;
        }
        else
        {
            x=x*x;
            i=i/2;
        }
    }
    if(n<0)
        return (1/ans);
    else
        return ans;
}
```

### Question :

https://leetcode.com/problems/powx-n/
