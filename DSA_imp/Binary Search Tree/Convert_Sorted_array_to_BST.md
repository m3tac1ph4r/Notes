# Convert sorted array to BST

Given an integer array `nums` where the elements are sorted in **ascending order**, convert *it to a **height-balanced** binary search tree*.

A **height-balanced** binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.

**Example**

![[convert_BST_ex1.png]]

![[convert_BST_ex2.png]]

### Approach (Recursion) :

We will find the mid of the array.

- Mid element will be the **root**
- left part array will be the **left subtree of root**
- right part array will be the **right subtree of root**

![[approach_converted_BST.png]]

```cpp
class Solution {
public:
    TreeNode* solve(vector<int>& nums,int start,int end)
    {
        if(start>end)
            return NULL;

        int mid=(start+end)/2;
        TreeNode* root=new TreeNode(nums[mid]);
        root->left=solve(nums,start,mid-1);
        root->right=solve(nums,mid+1,end);
        return root;
}
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        int start=0,end=nums.size()-1;
        return solve(nums,start,end);
    }
};
```

### Question:

https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/

### Reference:

https://youtu.be/C59kWTK4_Zs
