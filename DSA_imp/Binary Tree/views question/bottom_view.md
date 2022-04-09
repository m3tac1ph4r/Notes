# Bottom View of Binary tree
#binary_tree_view_question 


Given a binary tree, print the bottom view from left to right.  
A node is included in bottom view if it can be seen when we look at the tree from bottom.
```
 					  20  
                    /    \  
                  8       22  
                /   \        \  
              5      3       25  
                    /   \        
                  10    14
```

For the above tree, the bottom view is 5 10 3 14 25.  
If there are **multiple** bottom-most nodes for a horizontal distance from root, then print the later one in level traversal. For example, in the below diagram, 3 and 4 are both the bottommost nodes at horizontal distance 0, we need to print 4.

**Example 1:**

**Input:**      
```
	   1
     /   \
    3     2
```
**Output:** 3 1 2 **Explanation:**
First case represents a tree with 3 nodes
and 2 edges where root is 1, left child of
1 is 3 and right child of 1 is 2.

**Example 2:**

**Input:**         
```
		 10
       /    \
      20    30
     /  \
    40   60
```
**Output:** 40 20 60 30

### Approach

Approach is same as top view. The only diffence is in top view we take the first node which comes at that horizontal distance using if condition. But in bottom view we will take the last node at that particular horizontal distance.

1. We will push root and horizontal distance 0 in queue.
2. push the node in the map at that horizontal distance because we want last node.
3. then check if root->left is not NULL then push {node,hd-1} in queue.
4. Same with right if root->right is not NULL then push {node,hd+1} in queue.
5.  Now we have all horizontal distance and data in map. The only thing we have to do is to node data from map and copy to the array.

![[bottom_view_appraoch.png]]

As you can see in the bottom there is one eye. At horizontal distance *0* there are to nodes but eye can only see the LAST node at horizontal distance 0.

```C++
vector<int> bottomView(Node* root)
{
    vector<int> ans;
    if(root==NULL)
        return ans;
    map<int,int> hash_map;
    queue<pair<Node*,int>> q;
    q.push({root,0});
    while (!q.empty())
    {
        pair<Node*,int> tempNode=q.front();
        q.pop();
        int hd=tempNode.second;
        hash_map[hd]=tempNode.first->data;
        if(tempNode.first->left)
            q.push({tempNode.first->left,hd-1});
        if(tempNode.first->right)
            q.push({tempNode.first->right,hd+1});
    }
    for(auto i:hash_map)
    {
        ans.push_back(i.second);
    }
    return ans;
}
```


### Question
https://practice.geeksforgeeks.org/problems/bottom-view-of-binary-tree/1/#

### Reference
https://www.youtube.com/watch?v=s1d8UGDCCN8&list=PLDzeHZWIZsTo87y1ytEAqp7wYlEP3nner&index=14&ab_channel=CodeHelp-byBabbar