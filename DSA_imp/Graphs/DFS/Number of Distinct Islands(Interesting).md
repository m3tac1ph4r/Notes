# Number of Distinct Islands


Given a boolean 2D matrix **grid** of size **n** * **m**. You have to find the number of distinct islands where a group of connected 1s (horizontally or vertically) forms an island. Two islands are considered to be distinct if and only if one island is not equal to another (not rotated or reflected).

**Example 1:**

**Input:**
grid[][] = 
		{{1, 1, 0, 0, 0},
            {1, 1, 0, 0, 0},
            {0, 0, 0, 1, 1},
            {0, 0, 0, 1, 1}}
**Output:**
1
**Explanation:**
grid[][] = 
		{{*1*, *1*, 0, 0, 0}, 
            {*1*, *1*, 0, 0, 0}, 
            {0, 0, 0, *1*, *1*}, 
            {0, 0, 0, *1*, *1*}}
Same colored islands are equal.
We have 2 equal islands, so we 
have only 1 distinct island.

**Example 2:**

**Input:**
grid[][] =     
		{{1, 1, 0, 1, 1},
            {1, 0, 0, 0, 0},
            {0, 0, 0, 0, 1},
            {1, 1, 0, 1, 1}}
**Output:**
3
**Explanation:**
grid[][] = 
		{{*1*, *1*, 0, *1*, *1*}, 
            {*1*, 0, 0, 0, 0}, 
            {0, 0, 0, 0, *1*}, 
            {*1*, *1*, 0, *1*, *1*}}
Same colored islands are equal.
We have 4 islands, but 2 of them
are equal, So we have 3 distinct islands



### Approach :

If the island have same shape then it will not be counted.

For Example the two are having shape and other two also:
![[Number_of_distinct_island_shapeEx.png]]

**So how to find the shape is same or different ?**
We will use SET to store the shape of island. But HOW ?

![[number_of_distinct_set_explaination.png]]


### Code :

```cpp
class Solution {

  private:
    void dfs(int i,int j,int n,int m,vector<vector<bool>> &visited,vector<pair<int,int>> &vec,
    vector<vector<int>> &grid,int basei,int basej)
    {
        visited[i][j]=true;
        vec.push_back({i-basei,j-basej});
        
        int delRow[]={-1,0,1,0};
        int delCol[]={0,-1,0,1};
        
        for(int k=0;k<4;k++)
        {
            int newRow=i+delRow[k];
            int newCol=j+delCol[k];
            
            if(newRow>=0 and newRow<n and newCol>=0 and newCol<m and visited[newRow][newCol]==false
            and grid[newRow][newCol]==1)
                dfs(newRow,newCol,n,m,visited,vec,grid,basei,basej);
        }
    }
  public:
    int countDistinctIslands(vector<vector<int>>& grid) {
        // https://youtu.be/7zmgQSJghpo?list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn
        int n=grid.size();
        int m=grid[0].size();
        vector<vector<bool>> visited(n,vector<bool>(m,false));
        set<vector<pair<int,int>>> st;
        
        for(int i=0;i<n;i++)
        {
            for(int j=0;j<m;j++)
            {
                if(visited[i][j]==false and grid[i][j]==1)
                {
                    vector<pair<int,int>> vec;
                    dfs(i,j,n,m,visited,vec,grid,i,j);
                    st.insert(vec);
                }
            }
        }
        return st.size();
    }
};
```



### Resource :
https://youtu.be/7zmgQSJghpo?list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn


### Question :
https://practice.geeksforgeeks.org/problems/number-of-distinct-islands/1