# Spiral Matrix II

Given a positive integer `n`, generate an `n x n` `matrix` filled with elements from `1` to `n2` in spiral order.

![[spiral_matrix_II_example.png]]



### Approach

1. Take four variables r1=0, r2=n-1 ,c1=0, c2=n-1
2. Moving from **left to right** r1 will be constant and column will be change
	Moving from **top to bottom** c2 will be constant and row will be change
	Moving from **right to left** row will be constant and column will be change
	Moving from **bottom to top** row will be change and column will be constant
3. This will store the values in border ,  
	then r1++ , c1++ and r2-- , c2--.

![[spiral_matrix_II approach.png]]


```C++
vector<vector<int>> generateMatrix(int n)
{
    vector<vector<int>> ans(n,vector<int>(n));
    int r1=0,r2=n-1,c1=0,c2=n-1;
    int val=1;
    while(r1<=r2 and c1<=c2)
    {
        // left to right
        for(int c=c1;c<=c2;c++)
            ans[r1][c]=val++;
        
        //top to bottom
        for(int r=r1+1;r<=r2;r++)
            ans[r][c2]=val++;
        
        //right to left
        for(int c=c2-1;c>=c1;c--)
            ans[r2][c]=val++;
        
        //bottom to top
        for(int r=r2-1;r>r1;r--)
            ans[r][c1]=val++;
        
        //updating values
        r1++;
        r2--;
        c1++;
        c2--;
    }
    return ans;
}
```


### Question
https://leetcode.com/problems/spiral-matrix-ii/

### Reference
https://www.youtube.com/watch?v=yeGAAUzAPnU&ab_channel=AlgorithmsMadeEasy