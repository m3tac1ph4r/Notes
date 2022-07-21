# BURNING TREE

Given a binary tree and a node called target. Find the minimum time required to burn the complete binary tree if the target is set on fire. It is known that in 1 second all nodes connected to a given node get burned. That is its left child, right child, and parent.

**Example1 :**
![[burning_tree_ex1.png]]

**Example 2 :**
![[burning_tree_ex2.png]]

### Approach

1. Map child nodes with their parent node
2. While mapping if you found target node save that into some variable and return that
3. Then start levelorder traversal from target node and mark the nodes which are visited in map and increase the time if you find change in queue size

![[burning_tree_approach.png]]

```cpp
class Solution
{
public:
    Node *createMapping(Node *root, int target, map<Node *, Node *> &childToParent)
    {
        Node *res;
        queue<Node *> q;
        q.push(root);
        childToParent[root] == NULL;
        while (!q.empty())
        {
            Node *front = q.front();
            q.pop();

            if (front->data == target)
                res = front;

            if (front->left)
            {
                childToParent[front->left] = front;
                q.push(front->left);
            }
            if (front->right)
            {
                childToParent[front->right] = front;
                q.push(front->right);
            }
        }
        return res;
    }

    int solve(Node *target, map<Node *, Node *> &childToParent)
    {
        map<Node *, bool> visited;
        queue<Node *> q;
        q.push(target);
        visited[target] = true;
        int ans = 0;
        while (!q.empty())
        {
            int size = q.size();
            bool flag = false;

            for (int i = 0; i < size; i++)
            {
                Node *front = q.front();
                q.pop();

                if (front->left and !visited[front->left])
                {
                    flag = true;
                    visited[front->left] = true;
                    q.push(front->left);
                }
                if (front->right and !visited[front->right])
                {
                    flag = true;
                    visited[front->right] = true;
                    q.push(front->right);
                }
                if (childToParent[front] and !visited[childToParent[front]])
                {
                    flag = true;
                    visited[childToParent[front]] = true;
                    q.push(childToParent[front]);
                }
            }
            if (flag)
                ans++;
        }
        return ans;
    }
    int minTime(Node *root, int target)
    {
        // 1. Map child nodes with their parent
        // 2. Return target Node
        // 3. Map visited node and find the minimum time required to burn the tree
        map<Node *, Node *> childToParent;
        Node *tar = createMapping(root, target, childToParent);

        int ans = solve(tar, childToParent);

        return ans;
    }
};
```

### Question :

https://practice.geeksforgeeks.org/problems/burning-tree/1

### Reference :

https://youtu.be/XLdpy0_6MR4?list=PLDzeHZWIZsTo87y1ytEAqp7wYlEP3nner
