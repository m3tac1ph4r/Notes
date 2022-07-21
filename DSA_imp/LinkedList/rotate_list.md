# Rotate List by K places to right

Given the `head` of a linked list, rotate the list to the right by `k` places.

**Example 1:**

![[rotate_list_ex1.png]]

**Input:** head = [1,2,3,4,5], k = 2
**Output:** [4,5,1,2,3]

**Example 2:**
![[rotate_list_ex2.png]]

**Input:** head = [0,1,2], k = 4
**Output:** [2,0,1]

### Approach :

1. Count the length of linkedlist.
2. Then check if the k is having the multiple of len then remove the multiple because they will give the same linkedlist. Suppose len=5 and k=12 then 10 rotations will give the same linkedlist as given but only 2 nodes will be shifted right.`k = k % count`
3. Then traverse {len-k} nodes and now our new_head will be next of {len-k} node. And then update the next of {len-k} node to NULL

```cpp
ListNode *rotateRight(ListNode *head, int k)
{
    ListNode *curr = head;
    int count = 1;
    while (curr->next != NULL)
    {
        count++;
        curr = curr->next;
    }
    curr->next = head;
    k = k % count; // To remove the multiple of k suppose len=5 and k=12
                   // then 10 rotation will give the same linkedlist.So we have to check for only 2 rotations
    k = count - k;
    while (k > 0)
    {
        curr = curr->next;
        k--;
    }
    head = curr->next;
    curr->next = NULL;
    return head;
}
```

### Question :

https://leetcode.com/problems/rotate-list/

### Reference :

https://youtu.be/9VPm6nEbVPA
