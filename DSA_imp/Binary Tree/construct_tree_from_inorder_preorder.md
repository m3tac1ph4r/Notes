# Construct a binary tree from inorder and preorder :-
#important_for_interview 

Given two integer arrays `preorder` and `inorder` where `preorder` is the preorder traversal of a binary tree and `inorder` is the inorder traversal of the same tree, construct and return _the binary tree_.

![[inorder_preorder_ex1.png]]

**Example 2:**

**Input:**
N = 6
inorder[] = {3 1 4 0 5 2}
preorder[] = {0 1 3 4 2 5}
**Output:** [0,1,2,3,4,5,null]
**Explanation:** The tree will look like
```
       0
    /     \
   1       2
 /   \    /
3    4   5
```


### Approach (recursion) :-

1. Preorder is **{node,left,right}** it means preorder[index] will be root.
2. So firstly we will find root i.e preorder[index]. 
3. Then find the position of element in inorder because inorder is having **{left,node,right}** i.e from 0 to position-1 we will have left of root and
	position+1 to n we will have right of root.
	To find position we will map the element of inorder with index so that we can find the index in O(1) time.
4. Like this we will build our binary tree. We will use inorderStart and inorderEnd for finding left and right of root from inorder.
5. In base case we will check if index is greater than n **OR** inorderStart>inorderEnd

![[inorder preorder appraoch.png]]


```C++
void createMapping(vector<int> inorder,map<int,int> &nodeToIndex,int n)
{
    for(int i=0;i<n;i++)
        nodeToIndex[inorder[i]]=i;
}

Node* solve(vector<int> inorder,vector<int> preorder,int n,int &index,map<int,int> &nodeToIndex,int inorderStart,int inorderEnd)
{
    // base case
    if(index>=n || inorderStart>inorderEnd)
        return NULL;
    
    int element=preorder[index++];
    Node* root=new Node(element);
    int position=nodeToIndex[element];
    
    //recursive call
    root->left=solve(inorder,preorder,n,index,nodeToIndex,inorderStart,position-1);
    root->right=solve(inorder,preorder,n,index,nodeToIndex,position+1,inorderEnd);

    return root;
}

Node* buildTree(vector<int> inorder,vector<int> preorder)
{
    int n=inorder.size();
    map<int,int> nodeToIndex; 	// for mapping element with index
    createMapping(inorder,nodeToIndex,n);
    int index=0,inorderStart=0,inorderEnd=n-1;
    Node* ans=solve(inorder,preorder,n,index,nodeToIndex,inorderStart,inorderEnd);
    return ans;
}
```

### Time complexity :
Recursive call will take : **O(n)**
Createmapping will take :**O(nlogn)**

O(n) + O(nlogn) => O(nlogn)


### Question:
https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/
https://practice.geeksforgeeks.org/problems/construct-tree-1/1/#

### Reference:
https://www.youtube.com/watch?v=ffE1xj51EBQ&list=PLDzeHZWIZsTo87y1ytEAqp7wYlEP3nner&index=5&ab_channel=CodeHelp-byBabbar