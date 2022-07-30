# Maximum width of binary tree

Ex 1:
![[maximum_width_ex1.png]]

Ex 2 :
![[maximum_width_ex2.png]]

### Approach

So In this program we will use level order traversal with indexing.

![[approach_1.png]]

- As you can see we marked root as 0.
- Then it's left will be **(2\*i+1)** i.e (2\*0+1)=1
- Then it's right will be **(2\*i+2)** i.e (2\*0+2)=2
- Now we will change accordingly and we will find it's left and right
- Width of binary tree will be maximum of (start-end+1) from all the levels.
- For Ex: int ans=0;
  - For level 1 first node is at index=1 and last node is at index=2. ans=max(0,2-1+1) i.e **2**
  - For level 2 first node is at index=3 and last node is at index=6. ans=max(2,6-3+1) i.e **4**
  - For level 3 first node is at index=7 and last node is at index=14.
    ans=max(4,14-7+1) i.e **8**

```cpp
int widthOfBinaryTree(Node* root)
{
    int ans=0;
    queue<pair<Node*,int>> q;
    q.push({root,0});
    while(!q.empty())
    {
        int n=q.size();
        int start=q.front().second;
        int end=q.back().second;
        ans=max(ans,end-start+1);
        for(int i=0;i<n;i++)
        {
            pair<Node*,int> temp=q.front();
            q.pop();
            Node* node=temp.first;
            long idx=temp.second;
            if(node->left!=NULL)
                q.push({node->left,idx*2+1});
            if(node->right!=NULL)
                q.push({node->right,idx*2+2});
        }
    }
    return ans;
}
```

### Question Link

https://leetcode.com/problems/maximum-width-of-binary-tree/
