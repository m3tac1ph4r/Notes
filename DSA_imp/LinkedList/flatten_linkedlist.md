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
**Output:**  5-> 7-> 8- > 10 -> 19-> 20->
22-> 28-> 30-> 35-> 40-> 45-> 50.
**Explanation**:
The resultant linked lists has every 
node in a single level.
(**Note:** | represents the bottom pointer.)