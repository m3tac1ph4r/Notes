# Increasing order BST

Given the `root` of a binary search tree, rearrange the tree in **in-order** so that the leftmost node in the tree is now the root of the tree, and every node has no left child and only one right child.

![[increasing_order_bst_ex1.png]]

![[increasing order bst ex2.png]]

# Increasing order BST

Given the `root` of a binary search tree, rearrange the tree in **in-order** so that the leftmost node in the tree is now the root of the tree, and every node has no left child and only one right child

![[increasing_order_bst_ex1.png]]

![[increasing order bst ex2.png]]

### Approach 1

1. Firstly we will insert all node values in vector of integer.
2. Then sort the vector. As you can see we have to ararnge node in ascending order in right boundary
3. Now insert all values of vector in new tree.

**Code :**

```cpp
class Solution {
public:
    void solve(TreeNode* root,vector<int> &ans)
    {
        if(root==NULL)
            return;
        ans.push_back(root->val);
        solve(root->left,ans);
        solve(root->right,ans);
}
    TreeNode* buildTree(TreeNode* node,vector<int> ans,int count)
    {
        if(count==ans.size())
            return node;
        node=new TreeNode(ans[count]);
        node->left=NULL;
        node->right=buildTree(node->right,ans,count+1);
        return node;
}
    TreeNode* increasingBST(TreeNode* root) {
        vector<int> ans;
        solve(root,ans);
        sort(ans.begin(),ans.end());
        TreeNode* node;
        node=buildTree(node,ans,0);
        return node;
    }
};
```
