# Maximum Sum of non adjacent nodes

Given a binary tree with a value associated with each node, we need to choose a subset of these nodes such that sum of chosen nodes is maximum under a constraint that no two chosen node in subset should be directly connected that is, if we have taken a node in our sum then we can’t take its any children or parents in consideration and vice versa.

![[maximum_sum_of_non_adjacent_nodesEx.png]]

**Example 1:**

**Input:**     
 ```
     11
    /  \
   1    2
```
**Output:** 11
**Explanation:** The maximum sum is sum of
node 11.

**Example 2:**

**Input:**
```
        1
      /   \
     2     3
    /     /  \
   4     5    6
```
**Output:** 16
**Explanation:** The maximum sum is sum of
nodes 1 4 5 6 , i.e 16. These nodes are
non adjacent.

### Approach(Recursion)
1.  We will use pair for every node i,e **pair<a,b>**
		a- will indicate sum including that node at that level. That is now you can not include root's children and parent.
		b- will indicate sum excluding that node at that level. That is now you can include root's children and parent.
2.  So there will be two condition
	1.  If we take that node then sum will be ** root->data+lefttreesum(excluding left child of that node) + righttreesum(excluding right child of that node)**
	2.  If we don't take that node then sum will be **max(leftsubtree)+max(rightsubtree)**

3. In the last find the **maximum of including and excluding trees**

![[maximum sum of adjacent nodes approach.png]]

```C++
pair<int,int> solve(Node* root)
{
    // base case
    if(root==NULL)
        return {0,0};
    
    pair<int,int> leftSum=solve(root->left);
    pair<int,int> rightSum=solve(root->right);

    pair<int,int> res;
    res.first=root->data+leftSum.second+rightSum.second;    // including root and excluding child of root
    res.second=max(leftSum.first,leftSum.second)+max(rightSum.first,rightSum.second);
    // excluding root and including there child
    return res;
}
int getMaxSum(Node* root)
{
    /*
    // pair<int a,int b>
    // a means including that node at that level now its parent and child cannnot be included
    // b means excluding that node at that level 
    */
    pair<int,int> ans=solve(root);
    return max(ans.first,ans.second);
}
```