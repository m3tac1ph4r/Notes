
# Pattern of Binary Search Questions :

- If in question it is asked to **Find the maximum of {minimum}** then increase the space search by end=mid-1 . Now the range will be [start,mid-1]

![[book_allocation_ex1.png]]

- If in question it is asked to **Find the minimu of {maximum}** then decrease the space search by start=mid+1

![[aggresive_cow_ex.png]]


### Complexity :

1. **Time Complexity :** O(logn)
2. **Space Complexity :** O(n)