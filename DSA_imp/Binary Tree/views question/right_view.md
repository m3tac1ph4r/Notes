# Left view of binary Tree

#binary_tree_view_question

Given a Binary Tree, find **Right view** of it. Right view of a Binary Tree is set of nodes visible when tree is viewed from **right** side.

Right view of following tree is 1 3 7 8.

```
 		  1
       /     \
     2        3
   /   \      / \
  4     5   6    7
    \
     8
```

**Example 1:**

**Input:**

```
	  1
    /    \
   3      2
```

**Output:** 1 2

**Example 2:**

**Input:**

```
	 10
    /   \
  20     30
 /   \
40  60
```

**Output:** 10 30 60

### Approach(level order traversal)

The approach is same as left view.
We will store the LAST node in every level.

We will use **map<int,int>** key will be level of the node and value will be the data of node. As we have to maintain 1:1 relation that is 1 node for 1 level.
And **queue<pair<Node\*,int>>** for storing the node and level. Because we are going to do level order traversal.

1. We will push root and level 0 in queue.
2. push the node in the map at that level because we want LAST node.
3. then check if root->left is not NULL then push {node,level+1} in queue.
4. Same with right if root->right is not NULL then push {node,level+1} in queue.
5. Now we have all level and data in map. The only thing we have to do is to node data from map and copy to the array.

![[right_view_approach.png]]

```cpp
vector<int> leftView(Node *root)
{
    vector<int> ans;
    if (root == NULL)
        return ans;
    map<int, int> hash_map;
    queue<pair<Node *, int>> q;
    q.push({root, 0});
    while (!q.empty())
    {
        pair<Node *, int> tempNode = q.front();
        q.pop();
        int level = tempNode.second;
        hash_map[level] = tempNode.first->data;
        if (tempNode.first->left)
            q.push({tempNode.first->left, level + 1});
        if (tempNode.first->right)
            q.push({tempNode.first->right, level + 1});
    }
    for (auto i : hash_map)
    {
        ans.push_back(i.second);
    }
    return ans;
}
```

### Question

https://practice.geeksforgeeks.org/problems/right-view-of-binary-tree/1/
https://leetcode.com/problems/binary-tree-right-side-view/

### Refernce

https://youtu.be/s1d8UGDCCN8?list=PLDzeHZWIZsTo87y1ytEAqp7wYlEP3nner&t=3688
