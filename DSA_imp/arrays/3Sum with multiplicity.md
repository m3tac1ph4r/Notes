# 3sum with multiplicity

Given an integer array `arr`, and an integer `target`, return the number of tuples `i, j, k` such that `i < j < k` and `arr[i] + arr[j] + arr[k] == target`.

As the answer can be very large, return it **modulo** `109 + 7`.


**Example 1:**

**Input:** arr = [1,1,2,2,3,3,4,4,5,5], target = 8
**Output:** 20
**Explanation:** 
Enumerating by the values (arr[i], arr[j], arr[k]):
(1, 2, 5) occurs 8 times;
(1, 3, 4) occurs 8 times;
(2, 2, 4) occurs 2 times;
(2, 3, 3) occurs 2 times.

**Example 2:**

**Input:** arr = [1,1,2,2,2,2], target = 5
**Output:** 12
**Explanation:** 
arr[i] = 1, arr[j] = arr[k] = 2 occurs 12 times:
We choose one 1 from [1,1] in 2 ways,
and two 2s from [2,2,2,2] in 6 ways.


### Approach (Two pointer +hashing)

1. We will use unordered_map to store the number of counts of elements.
2. Now we will store the count of number in map . So key will be number and count will be value.
3. Now we will use two for loop. First for arr[i] and second for arr[j].
4.  If all are different means `count+=map[i]*map[j]*map[k]`
5. We will find third element using **k=target-i-j** . Now we will check whether third element is present in the map or not.  `count+= (map[i]*map[i]-1*map[k])/2`
6. Then if two element are same like **i == j** . Suppose the target is 8 and i=2( count=2) and j=2(count=2) and k=4(count=2) . Now if we will add element then 2(count=2) + 2(count=1)+4(count=2) . Because first 2 is used in i then it means count will be decrease. This means `count+= (map[i]*map[i]-1*map[i]-2)/6`
![[3sum_multiplicity_ij_same.png]]<br>
6. Same when **i , j, k are same** means count will `count*(count-1)*(count-2)`

![[3sum_multiplicity_ijk_same.png]]
 

![[3_sum_multiplicity_approach.png]]


```C++
int threeSumWithMulti(vector<int> height,int target)
{
    unordered_map<int, long> hash_map;
    int mod = 1e9 + 7;
    long res=0;
    for(int i:A)
        hash_map[i]++;
    for(auto it1:hash_map)
    {
        for(auto it2:hash_map)
        {
            int i=it1.first,j=it2.first,k=target-i-j;
            if(!hash_map.count(k))
                continue;
            if(i==j and j==k)
                res+=hash_map[i]*(hash_map[i]-1)*(hash_map[i]-2)/6;
                // res += hash_map[i] * (hash_map[i] - 1) * (hash_map[i] - 2) / 6;
            else if(i==j and j!=k)
                res += (hash_map[i] * (hash_map[i] - 1) * hash_map[k])/2;
            else if(i<j and j<k)
                res+=hash_map[i]*hash_map[j]*hash_map[k];
        }
    }
    return res % mod;
}
```


### Questions:

https://leetcode.com/problems/3sum-with-multiplicity/

### Reference:
https://www.youtube.com/watch?v=DiWpfOorDaA&ab_channel=AyushiSharma