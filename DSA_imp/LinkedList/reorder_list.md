# Reorder List

You are given the head of a singly linked-list. The list can be represented as:

L0 → L1 → … → Ln - 1 → Ln

_Reorder the list to be on the following form:_

L0 → Ln → L1 → Ln - 1 → L2 → Ln - 2 → …

You may not modify the values in the list's nodes. Only nodes themselves may be changed.

**Example 1:**

![[reorder_list_ex1.png]]

**Input:** head = [1,2,3,4]
**Output:** [1,4,2,3]

**Example 2:**

![[reorder_list_ex2.png]]

**Input:** head = [1,2,3,4,5]
**Output:** [1,5,2,4,3]

### Approach :

1. Find the middle of linked list. Then divide linkedlist in two halves first part will be left of middle and second will be right of middle.
2. Reverse the second part of linkedlist
3. Now add node from first part of linkedlist and then add node from second part of linkedlist

![[reorderlist_approach.png]]

```cpp
ListNode *reverseList(ListNode *head)
{
    ListNode *prev = NULL;
    ListNode *curr = head;
    ListNode *next_p;
    while (curr != NULL)
    {
        next_p = curr->next;
        curr->next = prev;
        prev = curr;
        curr = next_p;
    }
    head = prev;
    return head;
}
void reorderList(ListNode*  head)
{
	// finding middle
    ListNode* slow=head;
    ListNode* fast=head->next;
    while (fast!=NULL and fast->next!=NULL)
    {
        slow=slow->next;
        fast=fast->next->next;
    }
    ListNode* second=reverseList(slow->next);
    slow->next=NULL;
    ListNode* first=head;
    while(second!=NULL)
    {
        ListNode* temp1=first->next;
        ListNode* temp2=second->next;
        first->next=second;
        second->next=temp1;
        first=temp1;
        second=temp2;
    }
}
```
