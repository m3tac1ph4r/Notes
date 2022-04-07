# Sum of binary tree :-

Given a Binary Tree. Return **true** if, for every node **X** in the tree other than the leaves, its value is equal to the sum of its left subtree's value and its right subtree's value. Else return **false**.
An empty tree is also a Sum Tree as the sum of an empty tree can be considered to be 0. A leaf node is also considered a Sum Tree.

**Ex 1 :-**
**Input:**
```
    3
  /   \    
 1     2
```
**Output:** 1
**Explanation:** The sum of left subtree and right subtree is
1 + 2 = 3, which is the value of the root node.
Therefore,the given binary tree is a **sum tree**.

**Ex 2 :-**
**Input:**
```
		  10
        /    \
      20      30
    /   \ 
   10    10
```

**Output:** 0
**Explanation:** The given tree is not a sum tree.
For the root node, sum of elements
in left subtree is 40 and sum of elements
in right subtree is 30. Root element = 10
which is not equal to 30+40.

### Approach (Recursion):-
Data structure for storing ans : **pair<int,bool>**
1.  In this question we need to check two things.
	1.  return the sum of left subtree and rightsub tree. Then we will check the sum with root node.
	2.  And return true and false for leaf node and if sum is greater than root node
2. Firstly we will check if the root is **NULL**. Then it means the sum will be **0** and bool will be true.
3. Else we will check if node is leaf node or not, means **root->left == NULL and root->right == NULL** then sum will be root->data and bool will be true.
4. Then call for sum for leftsubtree and rightsubtree. And check if leftsubtree+rightsubtree== root->data. Then store leftsubtree+rightsubtree+root->data to sum and true in bool.
5. else return false in bool.

```C++
pair<int,bool> checkSum(Node* root)
{
    if(root==NULL)
    {
        pair<int,bool> p={0,true};
        return p;
    }
    else if (root->left ==NULL and root->right==NULL)
    {
        pair<int,bool> p={root->data,true};
        return p;
    }
    pair<int,bool> leftSubTree=checkSum(root->left);
    pair<int,bool> rightSubTree=checkSum(root->right);
    if(leftSubTree.second and rightSubTree.second and (leftSubTree.first+rightSubTree.first==root->data))
    {
        pair<int,bool> p={root->data+leftSubTree.first+rightSubTree.first,true};
        return p;
    }
    pair<int,bool> p;
    p.second=false;
    return p;
    }
bool isSumTree(Node* root)
{
    pair<int,bool> p;
    p=checkSum(root);
    return p.second;
}
```

### Question Link
https://practice.geeksforgeeks.org/problems/sum-tree/1#