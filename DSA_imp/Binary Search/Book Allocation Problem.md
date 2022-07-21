# Book Allocation Problem

Given an array of integers **A** of size **N** and an integer **B**.

College library has **N** bags,the **ith** book has **A[i]** number of pages.

You have to allocate books to **B** number of students so that maximum number of pages alloted to a student is minimum.

```
A book will be allocated to exactly one student.
Each student has to be allocated at least one book.
Allotment should be in contiguous order, for example: A student cannot be allocated book 1 and book 3, skipping book 2.
```

Calculate and return that minimum possible number.

**NOTE:** Return -1 if a valid assignment is not possible.

![[book_allocation_ex1.png]]

**For Example**

```
Input 1:
    A = [12, 34, 67, 90]
    B = 2
Output 1:
    113
Explanation 1:
    There are 2 number of students. Books can be distributed in following fashion :
        1) [12] and [34, 67, 90]
        Max number of pages is allocated to student 2 with 34 + 67 + 90 = 191 pages
        2) [12, 34] and [67, 90]
        Max number of pages is allocated to student 2 with 67 + 90 = 157 pages
        3) [12, 34, 67] and [90]
        Max number of pages is allocated to student 1 with 12 + 34 + 67 = 113 pages

        Of the 3 cases, Option 3 has the minimum pages = 113.

Input 2:
    A = [5, 17, 100, 11]
    B = 4
Output 2:
    100
```

![[book_allocation_ex2.png]]

**Conditions :**

1. A book will be allocated to one student i.e you cannot split the book
2. Each student must get a minium of 1 book
3. Allotment should be contigous order

### Approach

<pre>
 1. We will take two variable start=0 and end=sum_of_elements.
 while(start is less than  end)
		mid=(start+end)/2
		if we can distribute the sum of pages to B students which should be less than mid 
			then store answer and end=mid-1
		else
			start=mid+1
</pre>

```cpp
bool isPossible(vector<int> &A,int mid,int B)
{
    int student=1;
    int pageSum=0;
    for(int i=0;i<A.size();i++)
    {
        if(pageSum+A[i]<=mid)
        {
            pageSum+=A[i];
        }
        else
        {
            student++;
            if(student>B || A[i]>mid)
                return false;
            pageSum=A[i];
        }
        if(student>B)
            return false;
    }
    return true;
}
int books(vector<int> &A,int B)
{
    if(B>A.size())
        return -1;
    int start=0,sum=0,end=0,ans=-1;
    for(int i=0;i<A.size();i++)
        sum+=A[i];
    end=sum;
    while(start<=end)
    {
        int mid=start+(end-start)/2;
        if(isPossible(A,mid,B))
        {
            ans=mid;
            end=mid-1;
        }
        else
            start=mid+1;
    }
    return ans;
}
```

### Reference :

https://drive.google.com/file/d/1d2eNEMdw5iuX7PflLfGykLgKF-SloUyr/view

### Question :

https://www.interviewbit.com/problems/allocate-books/
