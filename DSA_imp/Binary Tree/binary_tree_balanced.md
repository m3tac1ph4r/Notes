# Check Binary Tree is balanced

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:

> a binary tree in which the left and right subtrees of _every_ node differ in height by not more than 1.

**Ex 1 :-**
![[balanced_ex1.png]]

**Ex 2 :-**
![[binary_balanced_ex2.png]]

### Approach (Using Postorder) :-

1. find left height of binary tree and right height of binary tree. And check if abs(lh-rh)>1
   then return -1
2. And if abs(lh-rh) <= 1 then return height of tree.

![[balanced tree approach.png]]

```cpp
int check_balanced(Node* root)
{
    if(root==NULL)
        return 0;
    int lh=check_balanced(root->left);
    if(lh==-1)
        return -1;
    int rh=check_balanced(root->right);
    if(rh==-1)
        return -1;
    if(abs(lh-rh)>1)
        return -1;
    return (1+max(lh,rh));
}
bool isBalanced(Node* root)
{
    if(check_balanced(root)!=-1)
        return true;
    else
        return false;
}
```
