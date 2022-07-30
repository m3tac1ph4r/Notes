# Flatten Binary tree into linked list :-

Given the `root` of a binary tree, flatten the tree into a "linked list":

- The "linked list" should use the same `TreeNode` class where the `right` child pointer points to the next node in the list and the `left` child pointer is always `null`.
- The "linked list" should be in the same order as a **pre-order traversal** (https://en.wikipedia.org/wiki/Tree_traversal#Pre-order,_NLR) of the binary tree.

**Follow up:** Can you flatten the tree in-place (with `O(1)` extra space)?

![[flatten tree to linkedlist example.png]]

![[flatten tree to linkedlist appraoch.png]]

## Appproach Using morris traversal

As in question it is said that we don't have to use extra space. That's why we will use Morris traversal

<pre>
current=root
if (current->left!=NULL)
	 	 then find predecessor of  current and store it in the prev
 	then prev->right=current->right  and current->right=current->left 
	current->left=NULL then

then after update the current to current->right 
 </pre>

![[flatten binary tree approach.png]]

```cpp
void flatten(TreeNode* root) {
       TreeNode* current=root;
       while(current!=NULL)
       {
           if(current->left!=NULL)
           {
               TreeNode* prev=current->left;
               while(prev->right!=NULL)
                   prev=prev->right;
               prev->right=current->right;
               current->right=current->left;
               current->left=NULL;
           }
           current=current->right;
       }
   }
```

### Question :-

https://leetcode.com/problems/flatten-binary-tree-to-linked-list/

### Resource:-

https://takeuforward.org/data-structure/flatten-binary-tree-to-linked-list/
