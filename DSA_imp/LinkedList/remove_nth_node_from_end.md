# Remove Nth Node From End of List

Given the `head` of a linked list, remove the `nth` node from the end of the list and return its head.
**Example 1:**
![[remove_n_node_ex.png]]

**Input:** head = [1,2,3,4,5], n = 2
**Output:** [1,2,3,5]

**Example 2:**

**Input:** head = [1], n = 1
**Output:** []

**Example 3:**

**Input:** head = [1,2], n = 1
**Output:** [1]

### Approach (Using Two Pointer Approach) :

![[remove_nth_node_end_approach.png]]

> ** Why we used dummmy node ?**
> There is an edge case if n=length_of_linkedlist i.e you have to delete the head. So if you use dummy node then fast will be at the last node and while loop condidtion will be false bcz fast->next == NULL and slow will be pointing to the dummy node and if you update the slow->next=slow->next->next then dummy will be pointing to the head->next.

![[remove_nth_node_dummy.png]]

```cpp
ListNode* removeNthFromEnd(ListNode* head,int n)
{
    ListNode* dummy=new ListNode();
    dummy->next=head;
    // dummy= head;
    ListNode* slow=dummy;
    ListNode* fast=dummy;
    for(int i=0;i<n;i++)
    {
       fast=fast->next;
    }
    while (fast->next!=NULL)
    {
        fast=fast->next;
        slow=slow->next;
    }
    slow->next=slow->next->next;
    return dummy->next;
}
```

### Question :

https://leetcode.com/problems/remove-nth-node-from-end-of-list/

### Reference:

https://takeuforward.org/data-structure/remove-n-th-node-from-the-end-of-a-linked-list/
