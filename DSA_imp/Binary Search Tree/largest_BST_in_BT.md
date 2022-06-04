# Largest BST in BT


You are given a binary tree with 'N' nodes. Your task is to return the size of the largest subtree of the binary tree which is also a BST.

A binary search tree (BST) is a binary tree data structure which has the following properties.

```
• The left subtree of a node contains only nodes with data less than the node’s data.
• The right subtree of a node contains only nodes with data greater than the node’s data.
• Both the left and right subtrees must also be binary search trees.
```

**Example 1:**
![[largest_bst_bt_ex1.png]]

**OUTPUT :** 3
 2 1 3 -1 -1 -1 -1 is largest bst in that binary tree
 
 
 ### Approach (Using range) :
 
 ![[largest_BST_in_BT_app.png]]
 
 ```C++
struct Node
{
    int data;
    Node *left;
    Node *right;

    Node(int val)
    {
        data = val;
        left = right = NULL;
    }
};

class info
{
public:
    int maxi;
    int mini;
    bool isvalidBST;
    int size;
};

info solve(Node *root, int &ans)
{
    if (root == NULL)
        return {INT_MIN, INT_MAX, true, 0};

    info left = solve(root->left, ans);
    info right = solve(root->right, ans);

    info curr;
    curr.maxi = max(root->data, right.maxi);
    curr.mini = min(root->data, left.mini);

    curr.size = left.size + right.size + 1;

    if (left.isvalidBST and right.isvalidBST and (left.maxi < root->data and root->data < right.mini))
    {
        ans = max(curr.size, ans); // answer update
        curr.isvalidBST = true;
    }
    else
        curr.isvalidBST = false;
    return curr;
}
int largestBST(Node *root)
{
    int ans = 0;
    solve(root, ans);
    return ans;
}

int main()
{
    
    return 0;
}
```


### Question :
https://www.codingninjas.com/codestudio/problems/largest-bst-subtree_893103

### Reference :

https://youtu.be/fqx8z3VepMA?list=PLDzeHZWIZsTpTAcxT0N5dhzMauZ0A1ZL8

