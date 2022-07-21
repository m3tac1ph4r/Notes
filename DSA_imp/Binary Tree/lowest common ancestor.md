# Lowest Common Ancestor

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where we allow **a node to be a descendant of itself**).”

**Ex 1 :-**

![[lca_ex1.png]]

**Ex 2 :-**
![[lca_ex2.png]]

### Approach :-

![[lowest_ancestor_approach.png]]

```cpp
Node* lowestCommonAncestor(Node* root,Node* p,Node* q)
{
    if (root == NULL || root == p || root == q)
        return root;
    Node *temp_left = lowestCommonAncestor(root->left, p, q);
    Node *temp_right = lowestCommonAncestor(root->right, p, q);
    if (temp_left == NULL)
        return temp_right;
    else if (temp_right == NULL)
        return temp_left;
    else
        return root;
}
```

### Question

https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/
