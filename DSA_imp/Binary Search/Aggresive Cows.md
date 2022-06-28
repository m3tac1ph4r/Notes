# Agressive Cows

Given an array of length ‘N’, where each element denotes the position of a stall. Now you have ‘N’ stalls and an integer ‘K’ which denotes the number of cows that are aggressive. **To prevent the cows from hurting each other, you need to assign the cows to the stalls, such that the minimum distance between any two of them is as large as possible. Return the largest minimum distance.**


![[aggresive_cow_ex.png]]

##### Sample Input 2 :

```
2
6 4
0 3 4 7 10 9
6 3
0 4 3 7 10 9
```

##### Sample Output 2 :

```
3
4
```

##### Explanation To Sample Input 2 :

```
In the first test case, the largest minimum distance will be 3 when 4 cows are placed at positions {0, 3, 7, 10} min=>3

In the second test case, the largest minimum distance will be 4 when 3 cows are placed at positions {0, 4, 10}.
```


### Approach :

![[aggresive_cow_approach.png]]

1. Our search space will be from 0 to maximum element
2. Now we will find mid and check if  all cows are placed at a distance greater than mid
3. Now we have to find the minimum of largest distance. So if got our anwer we will increase mid by increasing the start to mid+1
4. And suppose the all cows are not placed at a distance of mid then it means if cows are not placed at minimum distance of x then it can't be placed at x+1,x+2...
	So we will decrease the mid by end=mid-1

```C++
bool isPossible(vector<int> stalls,int mid,int k)
{
    int cowCount=1,lastPos=stalls[0];
    for(int i=1;i<stalls.size();i++)
    {
        if(stalls[i]-lastPos>=mid)
        {
            cowCount++;
            if(cowCount==k)
                return true;
            lastPos=stalls[i];
        }
    }
    return false;
}
int agressiveCows(vector<int> &stalls,int k)
{
    sort(stalls.begin(),stalls.end());
    int start=0,end=stalls[stalls.size()-1],ans;
    while (start<=end)
    {
        int mid=start+(end-start)/2;
        if(isPossible(stalls,mid,k))
        {
            ans=mid;
            start=mid+1;
        }
        else
            end=mid-1;
    }
    return ans;
}
```

### Question :
https://www.codingninjas.com/codestudio/problems/aggressive-cows_1082559

### Resource :
https://youtu.be/YTTdLgyqOLY
https://drive.google.com/file/d/1d2eNEMdw5iuX7PflLfGykLgKF-SloUyr/view
	