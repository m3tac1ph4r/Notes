# Reverse a LinkedList

Given the `head` of a singly linked list, reverse the list, and return _the reversed list_.

**Example 1:**
![[reverse_linkedlist_ex1.png]]
**Input:** head = [1,2,3,4,5]
**Output:** [5,4,3,2,1]

**Example 2:**
**Input:** head = [1,2]
**Output:** [2,1]

**Example 3:**
**Input:** head = []
**Output:** []

### Approach (three pointer approach) :




```C++
ListNode *reverseList(ListNode *head) 
{
    ListNode* prev=NULL;
    ListNode* curr=head;
    ListNode* next_p;
    while(curr!=NULL)
    {
        next_p=curr->next;
        curr->next=prev;
        prev=curr;
        curr=next_p;
    }
    head=prev;
    return head;
}
```