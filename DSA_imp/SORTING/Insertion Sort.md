# Insertion Sort

>**In insertion Sort we shift the element to right. And insert element to right place**

Insertion Sort explanation by taking card example

![[insertion_cards.png]]

### Approach :

![[insertion_sort_app1.png]]


![[insertion_sort_app2.png]]


### Why Insertion Sort ?
1. We don't traverse the whole for checking the element. Because left arrays is sorted as **i increases** . Like in Selection Sort we check ith element with whole array.
2. Suppose arrays is partially sorted then insertion sort gives more performance.

### Code :
```cpp
void insertionSort(int n, vector<int> &arr){
    // Write your code h/ere.
    for(int i=1;i<n;i++)
    {
        int temp=arr[i];
        int j;
        for(j=i-1;j>=0;j--)
        {
            if(arr[j]>temp)
            {
                arr[j+1]=arr[j];
            }
            else
                break;
        }
        arr[j+1]=temp;
    }
}
```

>**Time Complexity :**  O(n^2)
>**Space Complexity :** O(1)

**Best Case Complexity** When arrays is already sorted *O(n)*


### Question :
https://www.codingninjas.com/codestudio/problems/insertion-sort_3155179

### Reference :
https://youtu.be/7kIVfVY6Axk?list=PLDzeHZWIZsTp4pb_WBRahP1tnipLuX9qM