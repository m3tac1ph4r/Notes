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

![[remove_nth_node_1.png]]

**If N is equal to the size of linkedlist i.e remove the head node :**

![[remove_nth_node_2.png]]


### C++ Code using dummy node method :

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

```java
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode slow=head;
       ListNode fast=head;

       for(int i=0;i<n;i++){
        fast=fast.next;
       }

       if(fast==null)
        return slow.next;

        while(fast.next!= null){
            slow=slow.next;
            fast=fast.next;
        }

        slow.next=slow.next.next;
        return head;
    }
}
```
### Question :

https://leetcode.com/problems/remove-nth-node-from-end-of-list/

### Reference:

https://takeuforward.org/data-structure/remove-n-th-node-from-the-end-of-a-linked-list/
