# Check whether number is Prime in Efficient Approach


```cpp
bool isPrime(int n)
{
	if(n==1||n==0)
		return false;
	for(int i=2;i*i<=n;i++)
	{
		if(n%i==0)
			return false;
	}
	return true;
}
```



### Question
https://practice.geeksforgeeks.org/problems/help-ishaan5837/1