# Number of Islands

Given an `m x n` 2D binary grid `grid` which represents a map of `'1'`s (land) and `'0'`s (water), return *the number of islands*.

An **island** is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example 1:**

**Input:** grid = [
["1","1","1","1","0"],
["1","1","0","1","0"],
["1","1","0","0","0"],
["0","0","0","0","0"]
]
**Output:** 1

**Example 2:**

**Input:** grid = [
["1","1","0","0","0"],
["1","1","0","0","0"],
["0","0","1","0","0"],
["0","0","0","1","1"]
]
**Output:** 3

### Approach (DFS) :

![[number_of_island.png]]

1. We will mark 2 if _grid[i[j] == 1_ and check for all vertical and horizontal island
   1. grid[i+1][j]
   2. grid[i-1][j]
   3. grid[i][j+1]
   4. grid[i][j-1]

```cpp

void markIslands(int i, int j, int r, int c, vector<vector<char>> &grid)
{
    grid[i][j] = '2';
    if (i - 1 >= 0 and grid[i - 1][j] == '1')
        markIslands(i - 1, j, r, c, grid);
    if (i + 1 < r and grid[i + 1][j] == '1')
        markIslands(i + 1, j, r, c, grid);
    if (j - 1 >= 0 and grid[i][j - 1] == '1')
        markIslands(i, j - 1, r, c, grid);
    if (j + 1 < c and grid[i][j + 1] == '1')
        markIslands(i, j + 1, r, c, grid);
}
int numIslands(vector<vector<char>> &grid)
{
    int res = 0;
    int r = grid.size();
    int c = grid[0].size();
    for (int i = 0; i < r; i++)
    {
        for (int j = 0; j < c; j++)
        {
            if (grid[i][j] == '1')
            {
                res++;
                markIslands(i, j, r, c, grid);
            }
        }
    }
    return res;
}
```

### Question

https://leetcode.com/problems/number-of-islands/
