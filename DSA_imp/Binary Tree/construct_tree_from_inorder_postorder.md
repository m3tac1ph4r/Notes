# Construct a binary tree from inorder and postorder :-

#important_for_interview

Given two integer arrays `inorder` and `postorder` where `inorder` is the inorder traversal of a binary tree and `postorder` is the postorder traversal of the same tree, construct and return *the binary tree*.

![[inorder_postorder_example.png]]

**Example 2:**

**Input:**
N = 8
in[] = 4 8 2 5 1 6 3 7
post[] =8 4 5 2 6 7 3 1
**Output:** 1 2 4 8 5 3 6 7
**Explanation:** For the given postorder and
inorder traversal of tree the  resultant
binary tree will be

```
          1
       /      \
     2         3
   /  \      /  \
  4    5    6    7
   \
     8
```

**Example 2:**

**Input:**
N = 5
in[] = 9 5 2 3 4
post[] = 5 9 3 4 2
**Output:** 2 9 5 4 3
**Explanation:**  
the  resultant binary tree will be

```
           2
        /     \
       9       4
        \     /
         5   3
```

### Approach

The approach is same as **construct binary tree from inorder preorder**

1. Postorder is **{left,right,node}** it means preorder[index] will be root.
2. So firstly we will find root i.e preorder[index].
3. Then find the position of element in inorder because inorder is having **{left,node,right}** i.e from 0 to position-1 we will have left of root and
   position+1 to n we will have right of right.
   To find position we will map the element of inorder with index so that we can do the operation in O(1) time.
4. Like this we will build our binary tree. We will use inorderStart and inorderEnd for finding left and right of root from inorder.
5. In base case we will check if index is less than 0 **OR** inorderStart>inorderEnd then it will return _NULL_

![[inorder_postorder_approach.png]]

```cpp
void createMapping(vector<int> inorder, map<int, int> &nodeToIndex, int n)
{
    for (int i = 0; i < n; i++)
        nodeToIndex[inorder[i]] = i;
}

Node *solve(vector<int> inorder, vector<int> postorder, int n, int &index, map<int, int> &nodeToIndex, int inorderStart, int inorderEnd)
{
    // base case
    if (index<0 || inorderStart > inorderEnd)
        return NULL;

    int element = postorder[index--];
    Node *root = new Node(element);
    int position = nodeToIndex[element];

    // recursive call
    // we have recursive call for right first because index started from end
    root->right = solve(inorder, postorder, n, index, nodeToIndex, position + 1, inorderEnd);
    root->left = solve(inorder, postorder, n, index, nodeToIndex, inorderStart, position - 1);

    return root;
}

Node *buildTree(vector<int> inorder, vector<int> postorder)
{
    int n = inorder.size();
    map<int, int> nodeToIndex;
    createMapping(inorder, nodeToIndex, n);
    int index = n-1, inorderStart = 0, inorderEnd = n - 1;
    Node *ans = solve(inorder, postorder, n, index, nodeToIndex, inorderStart, inorderEnd);
    return ans;
}
```

> In recursive call we have called right first because _in postorder root is in the last and we index is from n-1 . So right subtree will come first then left subtree will be called._
> That's why **root->right** is called first.

### Time complexity :

Recursive call will take : **O(n)**
Createmapping will take :**O(nlogn)**

O(n) + O(nlogn) => O(nlogn)

### Question:

https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/
https://practice.geeksforgeeks.org/problems/tree-from-postorder-and-inorder/1/#

### Reference:

https://www.youtube.com/watch?v=ffE1xj51EBQ&list=PLDzeHZWIZsTo87y1ytEAqp7wYlEP3nner&index=5&ab_channel=CodeHelp-byBabbar
