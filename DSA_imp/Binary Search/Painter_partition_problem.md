# Painter's Partition Problem


Given an array/list of length ‘N’, where the array/list represents the boards and each element of the given array/list represents the length of each board. Some ‘K’ numbers of painters are available to paint these boards. Consider that each unit of a board takes 1 unit of time to paint.

You are supposed to return the area of the minimum time to get this job done of painting all the ‘N’ boards under a constraint that any painter will only paint the continuous sections of boards.

##### For Example :

```
In the below figure where array/list elements are {2, 1, 5, 6, 2, 3}.
```

![[painter_partition_ex.png]]

```
A painter can paint blocks {5,6} or {1,5,6,2} together but not {2,5,6} or {5,6,3}.
```

##### Sample Input 1 :

```
2
4 2
5 5 5 5
4 2
10 20 30 40
```

![[book_allocation_ex1.png]]

##### Sample Output 1 :

```
10
60
```

##### Explanation For Sample Input 1 :

```
In the first test case, we can divide the boards into 2 equal-sized partitions, so each painter gets 10 units of the board and the total time taken is 10.


In the second test case, we can divide the first 3 boards for one painter and the last board for the second painter.
```

##### Sample Input 2 :

```
2
2 2
48 90
4 2
1 2 3 4
```

##### Sample Output 2 :

```
90
6
```



### Approach :

**Same as Book allocation Problem**

```C++
bool isPossible(vector<int> boards, int k, int mid)
{
    int paintersCount = 1, sum = 0;
    for (int i = 0; i < boards.size(); i++)
    {
        if (sum + boards[i] <= mid)
        {
            sum += boards[i];
        }
        else
        {
            paintersCount++;
            if (paintersCount > k || boards[i] > mid)
                return false;
            sum = boards[i];
        }
    }
    return true;
}
int findLargestMinDistance(vector<int> boards, int k)
{
    int start = 0, sum = 0, end, ans = -1;
    if (k > boards.size())
        return -1;
    for (int i = 0; i < boards.size(); i++)
        sum += boards[i];
    end = sum;
    while (start <= end)
    {
        int mid = start + (end - start) / 2;
        if (isPossible(boards, k, mid))
        {
            ans = mid;
            end = mid - 1;
        }
        else
            start = mid + 1;
    }
    return ans;
}
```

### Question :

https://www.codingninjas.com/codestudio/problems/painter-s-partition-problem_1089557