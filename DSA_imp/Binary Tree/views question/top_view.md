# Top View of Binary Tree
#binary_tree_view_question

Given below is a binary tree. The task is to print the top view of binary tree. Top view of a binary tree is the set of nodes visible when the tree is viewed from the top. For the given 
below tree

```
 	   1  
    /     \  
   2       3  
  /  \    /   \  
4    5   6     7
```


Top view will be: 4 2 1 3 7  
**Note:** Return nodes from **leftmost** node to **rightmost** node.

**Example 1:**

**Input:**      
```
	  1
   /    \
  2      3
```
**Output:** 2 1 3 

**Example 2:**

**Input:**        
```   
	   10
    /      \
  20        30
 /   \    /    \
40   60  90    100
```
**Output:** 40 20 10 30 100


### Approach

We will use **map<int,int>** key will be horizontal distance of the node and value will be the data of node. As we have to maintain 1:1 relation that is 1 node for 1 horizontal distance.
And **queue<pair<Node*,int>>** for storing the node and horizontal distance. Because we are going to do level order traversal.

1. We will push root and horizontal distance 0 in queue.
2. And then check if horizontal distance is not present in the map then store data of node in map , horizontal distance as key.
3. then check if root->left is not NULL then push {node,hd-1} in queue.
4. Same with right if root->right is not NULL then push {node,hd+1} in queue.
5.  Now we have all horizontal distance and data in map. The only thing we have to do is to node data from map and copy to the array.

![[top_view_approach.png]]

As you can see in the bottom there is one eye. At horizontal distance *0* there are to nodes but eye can only see the FIRST node at horizontal distance 0.

```C++
vector<int> topView(Node* root)
{
    vector<int> ans;
    if(root==NULL)
        return ans;
    map<int,int> topNode;   // int1 -> horizontal distance, int2 -> Node data
    queue<pair<Node*,int>> q;
    q.push({root,0});
    while(!q.empty())
    {
        pair<Node*,int> temp=q.front();
        q.pop();
        int hd=temp.second;
        if(topNode.find(hd)==topNode.end())
            topNode[hd]=temp.first->data;
        if(temp.first->left)
            q.push({temp.first->left,hd-1});
        if(temp.first->right)
            q.push({temp.first->right,hd+1});
    }
    for(auto i:topNode)
        ans.push_back(i.second);
    return ans;
}
```


### Question
https://practice.geeksforgeeks.org/problems/top-view-of-binary-tree/1/#

### Reference
https://www.youtube.com/watch?v=s1d8UGDCCN8&list=PLDzeHZWIZsTo87y1ytEAqp7wYlEP3nner&index=14&ab_channel=CodeHelp-byBabbar

