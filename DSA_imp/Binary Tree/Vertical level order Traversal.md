# Vertical order Traversal

#important_for_interview

We have given a binary tree and we have to find vertical order traversal.

![[vertical_traversal_ex.png]]

Ex2 :-
![[vertical_traversal_ex2.png]]

<pre>
As you can see node{5} and node{6} are having same{level,vertical_distance}. 
If {level,vertical_distance} are same then sort those nodes in ascending order.
</pre>

\
**Nodes are maked as (level,vertical_distance from root)**

> So if we move left from root then **left ->[root->vertical-1,root->level+1]**
> So if we move right from root then **right ->[root->vertical+1,root->level+1]**

![[written_1.png]]

![[written_2.png]]

```cpp
vector<vector<int>> verticalTraversal(Node* root)
{
    vector<vector<int>> ans;
    queue<pair<Node*,pair<int,int>>> q;     // queue -> (node,vertical,level)
    map<int,map<int,multiset<int>>> m;      // map -> (vertical,{level,multinode})
    q.push({root,{0,0}});
    while(!q.empty())
    {
        auto temp=q.front();
        q.pop();
        int vertical=temp.second.first;
        int level=temp.second.second;
        Node* node=temp.first;
        m[vertical][level].insert(node->data);

        if(node->left)
            q.push({node->left,{vertical-1,level+1}});
        if(node->right)
            q.push({node->right,{vertical+1,level+1}});
    }

    for (auto p : m)      //first for map i.e map<int,map<int,multiset<int>>> m;
    {
        vector<int> col;
        for (auto q : p.second)     //second for map i.e map<int,multiset<int>>
        {
            for (auto i : q.second) // for multiset in second map i.e multiset<int>
                col.push_back(i);

            // col.insert(col.end(),q.second.begin(),q.second.end());  //this is the alternative for above for loop
        }
        ans.push_back(col);
    }
    return ans;
}
```

#### Question Link

https://leetcode.com/problems/vertical-order-traversal-of-a-binary-tree/
