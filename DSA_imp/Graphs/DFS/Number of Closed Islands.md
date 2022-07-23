# Number of closed Islands

Given a 2D `grid` consists of `0s` (land) and `1s` (water).  An _island_ is a maximal 4-directionally connected group of `0s` and a _closed island_ is an island **totally** (all left, top, right, bottom) surrounded by `1s.`

Return the number of _closed islands_.

**Example 1:**

![[number_of_closed_islands_ex1.png]]

**Input:** grid = [ [1,1,1,1,1,1,1,0],[1,0,0,0,0,1,1,0],[1,0,1,0,1,1,1,0],[1,0,0,0,0,1,0,1],[1,1,1,1,1,1,1,0] ]
**Output:** 2
**Explanation:** 
Islands in gray are closed because they are completely surrounded by water (group of 1s).

**Example 2:**
![[number of closed island ex2.png]]

**Input:** grid = [ [0,0,1,0,0],[0,1,0,1,0],[0,1,1,1,0] ]
**Output:** 1


### Approach(Using DFS) :

```cpp

bool solve(int i, int j, vector<vector<int>> &grid, int n, int m)
{
    if (i < 0 || i >= n || j < 0 || j >= m)
        return false; // invalid condition
    if (grid[i][j] == 1 || grid[i][j] == 2)
        return true; // if grid[i][j] is water or grid[i][j] is already visited

    grid[i][j] = 2;
    bool top = solve(i + 1, j, grid, n, m);
    bool bottom = solve(i - 1, j, grid, n, m);
    bool left = solve(i, j - 1, grid, n, m);
    bool right = solve(i, j + 1, grid, n, m);

    return top and bottom and left and right;
}
int closedIsland(vector<vector<int>> &grid)
{
    int count = 0;
    int n = grid.size();
    int m = grid[0].size();
    // will start a loop from 1 to n-1 bcz boundary elements will not be considered
    for (int i = 1; i < n - 1; i++)
    {
        // will start a loop from 1 to m-1 bcz boundary elements will not be considered
        for (int j = 1; j < m - 1; j++)
        {
            if (grid[i][j] == 0)
            {
                if (solve(i, j, grid, n, m))
                    count++;
            }
        }
    }
    return count;
}
```


### Question :
https://leetcode.com/problems/number-of-closed-islands/