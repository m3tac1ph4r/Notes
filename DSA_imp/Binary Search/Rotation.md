# Number of times sorted array rotated :

Given an ascending sorted rotated array **Arr** of distinct integers of size **N**. The array is right rotated **K** times. Find the value of **K**.

**Example 1:**

**Input:**
N = 5
Arr[] = {5, 1, 2, 3, 4}
**Output:** 1
**Explanation:** The given array is 5 1 2 3 4. 
The original sorted array is 1 2 3 4 5. 
We can see that the array was rotated 
1 times to the right.

**Example 2:**

**Input:**
N = 5
Arr[] = {1, 2, 3, 4, 5}
**Output:** 0
**Explanation:** The given array is not rotated.

### Approach :

1. As we know our array is divided in two parts 
	1. Sorted
	2. Unsorted
2. Our answer lies in unsorted part. So we will use two pointers next, prev.
	1. Prev - will have the previous element of mid
	2. Next - will have the next element of mid\
3. So we will find that element whose next and prev both are greater.

```C++
int findKRotation(int arr[], int n)
{
    int low = 0, high = n - 1, res = 0;
    while (low <= high)
    {
        int mid = low + (high - low) / 2;
        int prev = mid-1;
        int next = (mid + 1);
		if(mid==0)
		{
			prev=n-1;
			next=1;
		}
		else if(mid==n-1)
		{
			prev=n-2;
			next=0;
		}
        if (arr[mid] <= arr[prev] and arr[mid] <= arr[next])
        {
            return mid;
        }
        else if (arr[low] <= arr[mid] and arr[mid] >= arr[high])
            low = mid + 1;
        else if (arr[mid] <= arr[high])
            high = mid - 1;
    }
    return res;
}
```

### Question :
https://practice.geeksforgeeks.org/problems/rotation4723/1/#
