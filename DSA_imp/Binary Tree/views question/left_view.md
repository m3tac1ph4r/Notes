# Left view of binary Tree
#binary_tree_view_question 

Given a binary tree of size **N.** Your task is to complete the function **sumOfLongRootToLeafPath(),** that find the sum of all nodes on the longest path from root to leaf node.  
If two or more paths compete for the longest path, then the path having maximum sum of nodes is being considered.

**Example 1:**

**Input:** 
```
        4        
       / \       
      2   5      
     / \ / \     
    7  1 2  3    
      /
     6
```
**Output:** 13
**Explanation:**

**(4, 2, 1, 6)** above are 
part of the longest root to leaf path having
sum = (4 + 2 + 1 + 6) = 13

**Example 2:**

**Input:** 
```
          1
        /   \
       2     3
      / \   / \
     4   5 6   7
````
**Output:** 11

### Approach(level order traversal)

The approach is same as top view and bottom view. 
We will store the first node from left in every level.

We will use **map<int,int>** key will be level of the node and value will be the data of node. As we have to maintain 1:1 relation that is 1 node for 1 level.
And **queue<pair<Node*,int>>** for storing the node and level. Because we are going to do level order traversal.

1. We will push root and level 0 in queue.
2. And then check if level is not present in the map then store data of node in map , level as key.
3. push the node in the map at that level because we want FIRST node.
4. then check if root->left is not NULL then push {node,level+1} in queue.
5. Same with right if root->right is not NULL then push {node,level+1} in queue.
6.  Now we have all level and data in map. The only thing we have to do is to node data from map and copy to the array.

![[left_view_approach.png]]

```C++
vector<int> leftView(Node* root)
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
        int level=tempNode.second;
        if(hash_map.find(level)==hash_map.end())
        {
            hash_map[level]=tempNode.first->data;   
        }
        if(tempNode.first->left)
            q.push({tempNode.first->left,level+1});
        if(tempNode.first->right)
            q.push({tempNode.first->right,level+1});
    }
    for(auto i:hash_map)
    {
        ans.push_back(i.second);
    }
    return ans;
}
```

### Question
https://practice.geeksforgeeks.org/problems/left-view-of-binary-tree/1#

### Reference
https://youtu.be/s1d8UGDCCN8?list=PLDzeHZWIZsTo87y1ytEAqp7wYlEP3nner&t=3688