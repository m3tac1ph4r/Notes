# Shift 2-D Grid

Given a 2D `grid` of size `m x n` and an integer `k`. You need to shift the `grid` `k` times.

In one shift operation:

- Element at `grid[i][j]` moves to `grid[i][j + 1]`.
- Element at `grid[i][n - 1]` moves to `grid[i + 1][0]`.
- Element at `grid[m - 1][n - 1]` moves to `grid[0][0]`.

Return the *2D grid* after applying shift operation `k` times.

![[shif_2d_grid_ex1.png]]
![[shif_2d_grid_ex2.png]]

### Approach 1 (Bruteforce):

```cpp
class Solution {
public:
    vector<vector<int>> shiftGrid(vector<vector<int>>& grid, int k) {
        int m = grid.size(); //rows
        int n = grid[0].size(); //cols
        vector<vector<int>> temp(m, vector<int>(n, 0));
        int a=0,b=0;
        while(k--)
        {
            for(int i=0;i<m;i++)
            {
                for(int j=0;j<n;j++)
                {
                    if(i!=m-1 and j==n-1)
                        temp[i+1][0]=grid[i][j];
                    else if(i==m-1 and j==n-1)
                        temp[0][0]=grid[i][j];
                    else
                        temp[i][j+1]=grid[i][j];
}
}
            grid=temp;
}
        return grid;
    }
};
```

### Approach 2 (Optimal) :-

```cpp
class Solution {
public:
    vector<vector<int>> shiftGrid(vector<vector<int>>& grid, int k) {
        int m = grid.size(); //rows
        int n = grid[0].size(); //cols
        vector<vector<int>> temp(m, vector<int>(n, 0));

        for(int r = 0; r < m; r++) {
            for(int c = 0; c < n; c++) {
                int newVal = ((r*n + c) + k) % (m*n);
                int newr = newVal/n;
                int newc = newVal%n;
                temp[newr][newc] = grid[r][c];

            }
        }
        return temp;
    }
};
```

### Question:

https://leetcode.com/problems/shift-2d-grid/
