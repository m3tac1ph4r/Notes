# Morris Traversal (Inorder and Preorder) :-

As we have done other traversal like levelorder, inorder, preorder, postorder traversal. In all these traversal **Time complexity was : O(n) and Space complexity was : O(n)** but in
Morris Traversal **Time complexity is : O(n) and Space complexity is : O(1)**
So space complexity is the plus point in Morris Traversal.

> In Morris Traversal we use **Threaded Binary Tree**.
> And every node traverse **at most 3 times** .
>
> 1. Link Creation
> 2. Printing value
> 3. Removing Link

### 1. Morris Inorder Traversal {LEFT,NODE,RIGHT}

Firstly we will discuss inorder Traversal.

###### Algorithm for Morris Inorder Traversal :

<pre>
1. current=root
2. while(current!=NULL)
	 if(current->left == NULL) **{if left not exist}**
			print(current)
			current=current->right
	else
			predecessor=find(current)
			// this is for creating the temporary link
			if(pred->right==NULL)
					pred->right=current
					current=current->left
			// this is for removing the temporary link
			else
					pred->right=NULL
					print(current)
					current=current->right
</pre>

![[img1.png]]

![[img2.png]]

This is the threaded binary tree.

###### Code :

```cpp
vector<int> morrisInorderTraversal(Node *root)
{
    vector<int> inorder;
    Node *current = root;
    while (current != NULL)
    {
        // checking whether current left is not present
        if (current->left == NULL)
        {
            inorder.push_back(current->data);
            current = current->right;
        }
        // current left part is present
        else
        {
            // finding the predecessor of current
            Node *prev = current->left;
            while (prev->right != NULL and prev->right != current)
            {
                prev = prev->right;
            }
            // creating temporary link with predecessor of current
            if (prev->right == NULL)
            {
                prev->right = current;
                current = current->left;
            }
            // removing the temporary link with predecessor of current
            else
            {
                prev->right = NULL;
                inorder.push_back(current->data);
                current = current->right;
            }
        }
    }
    return inorder;
}
```

### 2. Morris Preorder Traversal {NODE,LEFT,RIGHT}

###### Algorithm for Morris Preorder Traversal :

<pre>
1. current=root
2. while(current!=NULL)
	 if(current->left == NULL) **{if left not exist}**
			print(current)
			current=current->right
	else
			predecessor=find(current)
			// this is for creating the temporary link
			if(pred->right==NULL)
					pred->right=current
					print(current)
					current=current->left
			// this is for removing the temporary link
			else
					pred->right=NULL
					current=current->right
</pre>

###### Code :

```cpp
vector<int> morrisPreorderTraversal(Node *root)
{
    vector<int> preorder;
    Node *current = root;
    while (current != NULL)
    {
        // checking whether current left is not present
        if (current->left == NULL)
        {
            preorder.push_back(current->data);
            current = current->right;
        }
        // current left part is present
        else
        {
            // finding the predecessor of current
            Node *prev = current->left;
            while (prev->right != NULL and prev->right != current)
            {
                prev = prev->right;
            }
            // creating temporary link with predecessor of current
            if (prev->right == NULL)
            {
                prev->right = current;
                preorder.push_back(current->data);
                current = current->left;
            }
            // removing the temporary link with predecessor of current
            else
            {
                prev->right = NULL;
                current = current->right;
            }
        }
    }
    return preorder;
}
```

## Questions

1. **Flatten Binary tree into linkedlist :-**
   https://leetcode.com/problems/flatten-binary-tree-to-linked-list/
   https://practice.geeksforgeeks.org/problems/flatten-binary-tree-to-linked-list/1/#
