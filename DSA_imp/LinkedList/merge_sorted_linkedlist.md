# Merge Sorted LinkedList

For a given Singly Linked List of integers, sort the list using the 'Merge Sort' algorithm.

##### Sample Input 1 :

```
1 4 5 2 -1
```

##### Sample Output 1 :

```
1 2 4 5
```

##### Sample Input 2 :

```
10 9 8 7 6 5 4 -1
```

##### Sample Output 2 :

```
4 5 6 7 8 9 10
```

### Approach(Using Merged Sort) :

1. Find mid of linkedlist using fast-slow approach
2. Then break the linkedlist in two halves i.e
   1. First linkedlist will be head to mid
   2. Second linkedlist will be mid->next to NULL
3. Then merge the first and second linkedlist using **merge()** function.
   1. Create the dummy linkedlist to store the answer. Then create a pointer node which will point to the ans
   2. Check if data_of_left_linkedlist is smaller than data_of_rightlinkedlist. Store the data_of_leftlinkedlist to ans and move the pointer to left\
   3. Else do same thing with the right_linkedlist

![[merged_sortedz_linkelist_app.png]]

```cpp
Node *findMiddle(Node *head)
{
    Node *slow = head;
    Node *fast = head->next;
    while (fast != NULL and fast->next != NULL)
    {
        slow = slow->next;
        fast = fast->next->next;
    }
    return slow;
}

Node *merge(Node *left, Node *right)
{
    Node *res = new Node(-1);

    Node *temp = res;

    while (left != NULL and right != NULL)
    {
        if (left->data < right->data)
        {
            temp->next = left;
            temp = left;
            left = left->next;
        }
        else
        {
            temp->next = right;
            temp = right;
            right = right->next;
        }
    }

    while (left != NULL)
    {
        temp->next = left;
        temp = left;
        left = left->next;
    }

    while (right != NULL)
    {
        temp->next = right;
        temp = right;
        right = right->next;
    }

    res = res->next;
    return res;
}
Node *mergeSort(Node *head)
{
    // Write your code here.
    if (head == NULL || head->next == NULL)
    {
        return head;
    }
    Node *mid = findMiddle(head);

    Node *left = head;
    Node *right = mid->next;
    mid->next = NULL;

    left = mergeSort(left);
    right = mergeSort(right);

    Node *res = merge(left, right);

    return res;
}
```

### Question :

https://www.codingninjas.com/codestudio/problems/mergesort-linked-list_630514

### Reference :

https://youtu.be/rM5EEA_rbNY
