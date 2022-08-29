# Merge Sort

We will implement merge sort using **recursion and divide and conquer approach** 


> **Merge Sort is best for sorting linkedlist**
> https://youtu.be/rM5EEA_rbNY
> https://leetcode.com/problems/sort-list/




### Code :

```cpp
void merge(vector<int> &arr,int start,int end)
{
    int mid=start+(end-start)/2;
    int len1=mid-start+1;
    int len2=end-mid;
    
    vector<int> a1(len1);
    vector<int> a2(len2);

    int mainArrayIndex=start;
    
    // copy values from [start-mid] from mainArray to a1
    // And [mid+1-end] from mainArray to a2
    for(int i=0;i<len1;i++)
        a1[i]=arr[mainArrayIndex++];
    
    for(int j=0;j<len2;j++)
        a2[j]=arr[mainArrayIndex++];
    
    // again intialize mainArrayIndex to start
    mainArrayIndex=start;
    int i=0,j=0;

	// merge two sorted arrays
    while(i<len1 and j<len2)
    {
        if(a1[i]<a2[j])
            arr[mainArrayIndex++]=a1[i++];
        else
            arr[mainArrayIndex++]=a2[j++];
    }
    
    while(i<len1)
        arr[mainArrayIndex++]=a1[i++];
    
    while(j<len2)
        arr[mainArrayIndex++]=a2[j++];

	// IMPROVEMENT :to delete the arrays created
	a1.clear();
    a2.clear();
}
void sorted(vector<int> &arr,int start,int end)
{
    int mid=start+(end-start)/2;
    if(start>=end)
        return;
    
    sorted(arr,start,mid);
    sorted(arr,mid+1,end);
    merge(arr,start,end);
}
void mergeSort(vector < int > & arr, int n) {
    sorted(arr,0,n-1);
}
```

>**Time Complexity :** O(nlogn)
>**Space Complexity :** O(n) {creating two arrays} + O(n) {for recursion}


### Question :
https://www.codingninjas.com/codestudio/problems/merge-sort_920442

### Resource :
https://youtu.be/cdHEpbBVjRM?list=PLDzeHZWIZsTp4pb_WBRahP1tnipLuX9qM