# Quick Sort 

>**In Quick Sort we find the pivot element for partition the array and then recursively call for left {start to partitionIndex-1} and for right {partitionIndex+1 to end}**
>Quick Sort is also a divide and conquer approach


### Approach :
![[quick_sort_app1.png]]

![[quick_sort_app2.png]]

![[quick_sort_app3.png]]


### Dry Run

![[quick_sort_dry_run1.png]]

![[quick_sort_dry_run2.png]]

![[quick_sort_dry_run3.png]]




### Code :

```cpp
//{ Driver Code Starts
#include <stdio.h>
#include <bits/stdc++.h>
using namespace std;

class Solution
{
    public:
    //Function to sort an array using quick sort algorithm.
    void quickSort(int arr[], int low, int high)
    {
        // code here
        if(low>=high)
            return;
        int partitionIndex=partition(arr,low,high);
        
        // recursive calls
        quickSort(arr,low,partitionIndex-1);
        quickSort(arr,partitionIndex+1,high);
    }
    
    public:
    int partition (int arr[], int low, int high)
    {
       // Your code here
        int pivotElement=arr[low];
        int count=0;
       
        for(int i=low+1;i<=high;i++)
            if(arr[i]<=pivotElement)
                count++;
        
        int pivotIndex=low+count; 
        swap(arr[low],arr[pivotIndex]);
        
        int i=0,j=high;
        
        // for check left part of arr is less than pivotElement
        // and right part of arr is greater than pivotElement
        while(i<pivotIndex and j>pivotIndex)
        {
            while(i<pivotIndex and arr[i]<=pivotElement)
                i++;
            while(j>pivotIndex and arr[j]>pivotElement)
                j--;
                
            if(i<pivotIndex and j>pivotIndex)
                swap(arr[i++],arr[j--]);
        }
        
        return pivotIndex;
        
    }
};
```

>**Time Complexity :** Best -> O(nlogn)  Worst -> O(n^2)
>**Space Complexity :** O(n) {recursion} and O(1) {as it doesnot take more space}

### Question :
https://practice.geeksforgeeks.org/problems/quick-sort/1


### Reference :
https://youtu.be/sNaHN4tZmRk?list=PLDzeHZWIZsTp4pb_WBRahP1tnipLuX9qM
https://www.geeksforgeeks.org/quick-sort/