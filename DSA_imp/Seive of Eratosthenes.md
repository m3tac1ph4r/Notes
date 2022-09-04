# Sieve of Eratosthenes

https://www.geeksforgeeks.org/sieve-of-eratosthenes/



## Find Prime Number in a range :
Given two integers M and N, generate all primes between M and N including M and N.

**Example 1:**

**Input:**
M=1,N=10
**Output:**
2 3 5 7
**Explanation:**
The prime numbers between 1 and 10
are 2,3,5 and 7.

**Example 2:**

**Input:**
M=2, N=5
**Output:**
2,3,5
**Explanation:**
The prime numbers between 2 and 5 are 
2,3 and 5.

### Code :

```cpp
class Solution {
  public:
    vector<int> primeRange(int M, int N) {
        // code here
        vector<bool> isPrime(N+1,true);
        vector<int> ans;
        for(int i=2;i<=N;i++)
        {
            if(isPrime[i])
            {
                if(i>=M)
                    ans.push_back(i);
                for(int j=2*i;j<=N;j=j+i)
                    isPrime[j]=false;
            }
        }
        return ans;
    }
};
```


### Question :
https://practice.geeksforgeeks.org/problems/find-prime-numbers-in-a-range4718/1