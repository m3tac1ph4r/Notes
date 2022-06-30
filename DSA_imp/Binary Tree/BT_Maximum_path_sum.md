# Binary Tree Maximum Path Sum
#important_for_interview 

A **path** in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence **at most once**. Note that the path does not need to pass through the root.

The **path sum** of a path is the sum of the node's values in the path.

Given the `root` of a binary tree, return _the maximum **path sum** of any **non-empty** path_.

**Example 1:**

![[max_path_sum_ex1.png]]

**Input:** root = [1,2,3]
**Output:** 6
**Explanation:** The optimal path is 2 -> 1 -> 3 with a path sum of 2 + 1 + 3 = 6.


**Example 2:**
![[max_path_sum_ex2.png]]

**Input:** root = [-10,9,20,null,null,15,7]
**Output:** 42
**Explanation:** The optimal path is 15 -> 20 -> 7 with a path sum of 15 + 20 + 7 = 42.


### Approach (Recursion) :

Prerequisites of this question are **Diameter of Binary Tree** and **Check Binary Tree Balanced**

![[BT_max_path_sum_approach.png]]

Now we can apply this formula at every node by doing a simple tree traversal and storing the maximum value (our answer) in a reference variable.

To summarize:

-   Initialize a maxi variable to store our final answer.
-   Do a simple tree traversal. At each node, find  recursively its leftMaxPath and its rightMaxPath.
-   Calculate the maxPath through the node as val + (leftMaxPath + rightMaxPath) and update maxi accordingly.
-   Return the maxPath when node is not the curving point as val + max(leftMaxPath, rightMaxPath).

![[BT_max_path_sum_app_ex.png]]


>**How to handle the negative values ?**
>We will take ans=INT_MIN so that if root is having -ve value then it ans will be updated.
>And we will ignore the negative values from lh and rh as we will ignore the -ve path sum. So we will take **max(0,lh) and max(0,rh)**

```C++
int solve(TreeNode *root, int &sum)
{
    if (root == NULL)
        return 0;

    int lh = max(0, solve(root->left, sum));
    int rh = max(0, solve(root->right, sum));

    sum = max(sum, root->val + lh + rh);

    return root->val + max(lh, rh);
}
int maxPathSum(TreeNode *root)
{
    int sum = INT_MIN;
    solve(root, sum);
    return sum;
}
```

### Question :

https://leetcode.com/problems/binary-tree-maximum-path-sum/


### Reference :

https://youtu.be/WszrfSwMz58