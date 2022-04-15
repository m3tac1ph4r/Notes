# K sum paths

Given a binary tree and an integer K. Find the number of paths in the tree which have their sum equal to K.  
A path may start from any node and end at any node in the downward direction.

**Example 1:**

**Input:** 
Tree = 
```
          1                               
        /   \                          
       2     3
```
K = 3
**Output:** 2
**Explanation:**
Path 1 : 1 + 2 = 3
Path 2 : only leaf node 3

**Example 2:**

**Input:** 
Tree =
```
           1
        /     \
      3        -1
    /   \     /   \
   2     1   4     5                        
        /   / \     \                    
       1   1   2     6    
```
K = 5                    
**Output:** 8
**Explanation:**
The following paths sum to K.  
3 2 
3 1 1 
1 3 1 
4 1 
1 -1 4 1 
-1 4 2 
5 
1 -1 5


### Approach(recursion and backtracking)

![[k_sum_path_approach.png]]


```C++
void findCount(Node *root, int k, int &count, vector<int> ans)
{
    if (root == NULL)
        return;
    ans.push_back(root->data);
    findCount(root->left, k, count, ans);
    findCount(root->right, k, count, ans);
    int sum = 0;
    for (int i = ans.size() - 1; i >= 0; i--)
    {
        sum += ans[i];
        if (sum == k)
        {
            count++;
        }
    }
    ans.pop_back();
}
int sumK(Node *root, int k)
{
    // code here
    int count = 0;
    vector<int> ans;
    findCount(root, k, count, ans);
    return count;
}
```


### Question
https://practice.geeksforgeeks.org/problems/k-sum-paths/1/#