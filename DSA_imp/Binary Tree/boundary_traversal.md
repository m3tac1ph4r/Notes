# Boundary traversal in Binary Tree

Given a Binary Tree, find its Boundary Traversal. The traversal should be in the following order: 

1.  **Left boundary nodes:** defined as the path from the root to the left-most node ie- the leaf node you could reach when you always travel preferring the left subtree over the right subtree. 
2.  **Leaf nodes:** All the leaf nodes except for the ones that are part of left or right boundary.
3.  **Reverse right boundary nodes:** defined as the path from the right-most node to the root. The right-most node is the leaf node you could reach when you always travel preferring the right subtree over the left subtree. Exclude the root from this as it was already included in the traversal of left boundary nodes.

**Note:** If the root doesn't have a left subtree or right subtree, then the root itself is the left or right boundary.


**Example 1:**

**Input:** 
```
	   1 
	 /   \
     2     3 
	/ \   / \ 
   4   5 6   7
      / \
     8   9 
 ```
 
 **Output:** 1 2 4 8 9 6 7 3
 
 **Example 2:**

**Input:**
 ```
 		   1
           / 
          2
        /  \
       4    9
     /  \    \
    6    5    3
             /  \
            7     8  
```

**Output:** 1 2 4 6 5 7 8

### Approach

We will divide this question in three parts:
1. We will find left boundary of a tree.
2. Leaf nodes of left subtree. Then leaf nodes of right subtree.
	> Why we didn't find the leaf nodes of whole tree directly ?
	> Because we have to find the path of leaf node which will connect to the root.
	
For example in the below tree. If we find leaf of root it will be **1** . So it will give the output [1,1,] which is incorrect acc to question. Because we have to find those leaf node which joins **root to root**.  Because of that we will find leaf nodes of left and right subtree seperately.

![[draw_boundary.png]]
 3. Now we will find boundary of right subtree.

**Code**

```C++
void travelLeft(Node* root,vector<int> &ans)
{
    if(root==NULL || (root->left==NULL and root->right==NULL))
        return;
    ans.push_back(root->data);
    if(root->left)
        travelLeft(root->left,ans);
    else
        travelLeft(root->right,ans);
}

void leafNode(Node* root,vector<int> &ans)
{
    if(root==NULL)
        return;
    if(root->left==NULL and root->right==NULL)
    {
        ans.push_back(root->data);
        return;
    }
    leafNode(root->left,ans);
    leafNode(root->right,ans);
}

void travelRight(Node* root,vector<int> &ans)
{
    if(root==NULL || (root->left==NULL and root->right==NULL))
        return;
    if(root->right)
        travelRight(root->right,ans);
    else
        travelRight(root->left,ans);
    ans.push_back(root->data);
}
vector<int> boundary(Node* root)
{
    vector<int> ans;
    ans.push_back(root->data);
    
    // left part boundary
    travelLeft(root->left,ans);

    // left subtree leaf node
    leafNode(root->left,ans);

    //right subtree leaf node
    leafNode(root->right,ans);

    //right part boundary
    travelRight(root->right,ans);
    return ans; 
}
```

### Question

https://practice.geeksforgeeks.org/problems/boundary-traversal-of-binary-tree/1/#


### Reference
https://www.youtube.com/watch?v=s1d8UGDCCN8&list=PLDzeHZWIZsTo87y1ytEAqp7wYlEP3nner&index=7