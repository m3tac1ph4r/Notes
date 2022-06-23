# Flatten Linkedlist

Given a Linked List of size N, where every node represents a sub-linked-list and contains two pointers:  
(i) a **next** pointer to the next node,  
(ii) a **bottom** pointer to a linked list where this node is head.  
Each of the sub-linked-list is in sorted order.  
Flatten the Link List such that all the nodes appear in a single level while maintaining the sorted order.

**Input:**
<pre>
5 -> 10 -> 19 -> 28
|     |     |     | 
7     20    22   35
|           |     | 
8          50    40
|                 | 
30               45
</pre>
**Output:**  5-> 7-> 8- > 10 -> 19-> 20->22-> 28-> 30-> 35-> 40-> 45-> 50.
**Explanation**:
The resultant linked lists has every 
node in a single level.
(**Note:** | represents the bottom pointer.)

**Example 2:**
**Input:**
<pre>
5 -> 10 -> 19 -> 28
|          |                
7          22   
|          |                 
8          50 
|                           
30 
</pre>

**Output:** 5->7->8->10->19->22->28->30->50
**Explanation:**
The resultant linked lists has every node in a single level.
(**Note:** | represents the bottom pointer.)

### Approach :

```C++
ListNode *mergeList(ListNode *a, ListNode *b)
{
    if (a == NULL)
        return b;
    if (b == NULL)
        return a;
    ListNode *temp = new ListNode(0);
    ListNode *res = temp;
    while (a != NULL and b != NULL)
    {
        if (a->val < b->val)
        {
            temp->bottom = a;
            temp = temp->bottom;
            a = a->bottom;
        }
        else
        {
            temp->bottom = b;
            temp = temp->bottom;
            b = b->bottom;
        }
    }
    if (a != NULL)
    {
        temp->bottom = a;
    }
    else
        temp->bottom = b;
    return res->bottom;
}
ListNode *flatten(ListNode *root)
{
    // Your code here
    if (root == NULL or root->next == NULL)
        return root;

    root->next = flatten(root->next);
    root = mergeList(root, root->next);
    return root;
}
```

### Question :
https://practice.geeksforgeeks.org/problems/flattening-a-linked-list/1

### Reference :

https://youtu.be/ysytSSXpAI0