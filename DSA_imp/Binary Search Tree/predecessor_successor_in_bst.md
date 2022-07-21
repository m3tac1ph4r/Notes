# PREDECESSOR AND SUCCESSOR IN BST

There is BST given with root node with key part as an integer only. You need to find the in-order successor and predecessor of a given key. If either predecessor or successor is not found, then set it to _NULL_.

**EXAMPLE 1:**

![[predecessor_ex1.png]]

**Predecessor :** 7
**Successor :** 9

**EXAMPLE 2:**
![[predecessor_ex2.png]]

**Predecessor :** 2
**Successor :** 4

### Approach (Iterative) :

```cpp
void findPreSuc(Node *root, Node *&pre, Node *&suc, int key)
{
    pre = NULL;
    suc = NULL;

    Node *temp = root;
    // successor
    while (temp != NULL)
    {
        if (temp->key > key)
        {
            suc = temp;
            temp = temp->left;
        }
        else
            temp = temp->right;
    }
    // predecessor
    temp = root;
    while (temp != NULL)
    {
        if (temp->key < key)
        {
            pre = temp;
            temp = temp->right;
        }
        else
            temp = temp->left;
    }
```

> **Time Complexity : O(height of tree)** > **Space Complexity: O(1)**

### Question :

https://practice.geeksforgeeks.org/problems/predecessor-and-successor/1#

### Reference:

https://www.youtube.com/watch?v=SXKAD2svfmI&ab_channel=takeUforward
