# Reverse Linkedlist 2

Given the `head` of a singly linked list and two integers `left` and `right` where `left <= right`, reverse the nodes of the list from position `left` to position `right`, and return _the reversed list_.


**Example 1:**

![[reverse_linkedlist2_ex1.png]]

**Input:** head = [1,2,3,4,5], left = 2, right = 4
**Output:** [1,4,3,2,5]

**Example 2:**

**Input:** head = [5], left = 1, right = 1
**Output:** [5]


### Approach :

1. Firstly find the left_node i.e start node for reverse. We will use prev pointer to store the previous node of start node to store the reverse node to it's previous.
2. Then we will find the next to right node.
3. Then reverse the `right-left+1` node 
4. Then rejoin reversed linkedlist in the orginal linkedlist
5. Then check if `left==1` return new_head means the previous head will be reversed. Else return head

```C++
ListNode *reverse(ListNode *head, int len)
{
    ListNode *prev = NULL;
    ListNode *curr = head;
    ListNode *nexxt;
    int c = 1;
    while (curr != NULL and c <= len)
    {
        nexxt = curr->next;
        curr->next = prev;
        prev = curr;
        curr = nexxt;
        c++;
    }
    return prev;
}
ListNode *reverseBetween(ListNode *head, int left, int right)
{
    if (left == right || head == NULL)
        return head;
    ListNode *curr = head;
    ListNode *prev = NULL;
    int k = 1;
    while (curr != NULL and k < left)
    {
        prev = curr;
        curr = curr->next;
        k++;
    }

    ListNode *start = curr;
    while (curr != NULL and k < right)
    {
        curr = curr->next;
        k++;
    }
    ListNode *last = curr->next;
    ListNode *new_head = reverse(start, right - left + 1);

    if (prev != NULL)
    {
        prev->next = new_head;
    }
    curr = new_head;

    while (curr->next != NULL)
    {
        curr = curr->next;
    }

    curr->next = last;

    if (left == 1)
        return new_head;
    else
        return head;
}
```

### Question :

https://leetcode.com/problems/reverse-linked-list-ii/

### Reference :

https://youtu.be/tHKp8UuOkm4