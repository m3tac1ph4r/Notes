# Selection Sort

> In Selection Sort we take ith element and check for all (i+1)th element. And  place that in it's sorted position.

![[selection_Sort_app.png]]


### Code :
```cpp
void selectionSort(vector<int>& arr, int n)
{   
    for(int i=0;i<n-1;i++)
    {
        int minIndex=i;
        for(int j=i+1;j<n;j++)
        {
            if(arr[j]<arr[minIndex])
                minIndex=j;
        }
        int temp=arr[i];
        arr[i]=arr[minIndex];
        arr[minIndex]=temp;
    }
}
```

>**Time Complexity :** O(n^2)
>**Space Complexity :** O(1)



### Question :
https://www.codingninjas.com/codestudio/problems/selection-sort_981162


### Reference :
https://youtu.be/UdO2NeHB46c?list=PLDzeHZWIZsTp4pb_WBRahP1tnipLuX9qM