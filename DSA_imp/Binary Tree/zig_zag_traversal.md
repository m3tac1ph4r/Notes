# Zig Zag Traversal Level Order Traversal :-

Given the `root` of a binary tree, return _the zigzag level order traversal of its nodes' values_. (i.e., from left to right, then right to left for the next level and alternate between).

![[zig zag example.png]]

![[zigzag_explain.png]]

### Approach :-

We will solve this using level order traversal.

<pre>
1. Firstly we will intialize one variable <b>leftToRight=true</b> and queue for storing nodes.
2. Then we will start a while loop with condition that q is not empty.
			Started a for loop from 0 to queue.size().
					Then checked if <b>leftToRIght==true</b> 
						then store the value at ith index.
					If <b>leftToRIght==false</b> 
						then store the value in array at last ith index.
3. Then invert the value of leftToRight. Like if it is true then make it false and vice versa.
</pre>

```cpp
vector<vector<int>> zigzagLevelOrder(Node* root)
{
    vector<vector<int>> ans;
    if(root==NULL)
        return ans;
    queue<Node*> q;
    bool leftToRight=true;
    q.push(root);
    while(!q.empty())
    {
        int size=q.size();
        vector<int> arr(size);
        for(int i=0;i<size;i++)
        {
            Node* frontNode=q.front();
            q.pop();
            int index=(leftToRight==true)?i:size-i-1;
            arr[index]=frontNode->data;
            if(frontNode->left)
                q.push(frontNode->left);
            if(frontNode->right)
                q.push(frontNode->right);
        }
        ans.push_back(arr);
        leftToRight=!leftToRight;
    }
    return ans;
}
```

### Question

https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/

### Reference

https://www.youtube.com/watch?v=s1d8UGDCCN8&list=PLDzeHZWIZsTo87y1ytEAqp7wYlEP3nner&index=5
