# check BT is valid BST or not :

Given the `root` of a binary tree, *determine if it is a valid binary search tree (BST)*.

A **valid BST** is defined as follows:

- The left subtree of a node contains only nodes with keys **less than** the node's key.
- The right subtree of a node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees must also be binary search trees.

**EXAMPLE :**

![[check_valid_BST_ex1.png]]

![[check_valid_BST_ex2.png]]

### Appoach (Using RANGE) :

We will use range to check whether the node values lie between range or not.

![[check_valid_BST_appraoch.png]]

So this is the valid BST. All the elements lies between the range.

> 1. **If we move LEFT :** then high value will be updated to node value
> 2. **If we move RIGHT :** then low value will be updated to node value

```cpp
#include<bits/stdc++.h>
using namespace std;
#define ll long long
const int M=1e9+7;


// Definition for a binary tree node.
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode() : val(0), left(nullptr), right(nullptr) {}
    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
    TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
};

class Solution
{
public:
    bool solve(TreeNode *root, long low, long high)
    {
        if (root == NULL)
            return true;
        if (root->val <= low || root->val >= high)
            return false;

        return (solve(root->left, low, root->val) and solve(root->right, root->val, high));
    }
    bool isValidBST(TreeNode *root)
    {
        long low = LONG_MIN;
        long high = LONG_MAX;
        return solve(root, low, high);
    }
};
```

### Question:

https://leetcode.com/problems/validate-binary-search-tree/

### Reference:

https://www.youtube.com/watch?v=f-sj7I5oXEI&ab_channel=takeUforward
