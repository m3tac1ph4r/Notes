# Bubble Sort

> In bubble sort we swap the adjacent element.

![[bubble_sort_r1.png]]


![[bubble_sort_r2.png]]

![[bubble_sort_r3.png]]

![[bubble_sort_r4.png]]


### Use Case of Bubble  Sort ?
In each ith round we find the ith largest element. And place that in its sorted place.
Suppose for i=1 then it will find the 1st largest element element. And place that in it's original position.

### Code :
```cpp
void bubbleSort(vector<int>& arr, int n)
{
    for(int i=1;i<n;i++)
    {
        for(int j=0;j<n-i-1;j++)
        {
            if(arr[j]>arr[j+1])
                swap(arr[j],arr[j+1]);
        }
    }
}
```

>**Time Complexity :** Worst and Best both are : O(n^2)

### Optimize Code :

Suppose your array is already sorted. Then also the above code will take O(n^2) time. To overcome this we will check if any element is sorted or not in that round.

```cpp
void bubbleSort(vector<int>& arr, int n)
{
    for(int i=0;i<n-1;i++)
    {
        bool checkSwapped=false;
        for(int j=0;j<n-i-1;j++)
        {
            if(arr[j]>arr[j+1])
            {
                swap(arr[j],arr[j+1]);
                checkSwapped=true;
            }
        }
        if(checkSwapped==false)
            break;
    }
}
```

>**Time Complexity :** Worst is : O(n^2) Best is : O(n)


### Question :
https://www.codingninjas.com/codestudio/problems/bubble-sort_980524

### Reference :
https://youtu.be/zOhUavxlzw4?list=PLDzeHZWIZsTp4pb_WBRahP1tnipLuX9qM
