# Snake And Ladder


So we will be given a matrix which will be consisting of **-1** and a number between **1 to n^2**.

![[snake_ladder_draw.png]]


### Approach


![[snake_ladder_approach.png]]

The main tricky part in this question is to find coordinate. So I created a seperate function for that.

1. As you will  observe **if n is even then continuation of numbers from right side is in even rows.** and **if n is odd then continuation of numbers from right side is in odd rows**
2. So if n is even and row is also even then we will find coloumn from back side i.e if col=2  means n-col-1

![[snake_ladder_coloumn.png]]

```C++
pair<int, int> findCoordinates(int sum, int n)
{
    int r = n - ((sum - 1) / n) - 1;
    int c = (sum - 1) % n;

    if (r % 2 == n % 2)   // since there is a reversal in cell position after every row,
        return {r, n - 1 - c}; // this check will take care of that
    else
        return {r, c};
}
int snakesAndLadders(vector<vector<int>> &board)
{
    queue<int> q;
    int n = board.size();
    int steps = 0;
    vector<vector<bool>> visited(n, vector<bool>(n, false));

    q.push(1);
    visited[n - 1][0] = true;

    while (!q.empty())
    {
        int size = q.size();

        for (int i = 0; i < size; i++)
        {
            int num = q.front();
            q.pop();

            if (num == n * n)
                return steps;

            for (int dice = 1; dice <= 6; dice++)
            {
                if (num + dice > n * n)
                    break;

                pair<int, int> coordinate = findCoordinates(num + dice, n);
                int r = coordinate.first;
                int c = coordinate.second;

                if (visited[r][c] == true)
                    continue;
                visited[r][c] = true;

                if (board[r][c] == -1)
                    q.push(num + dice);
                else
                    q.push(board[r][c]);
            }
        }
        steps++;
    }
    return -1;
}
```

### Reference :

https://youtu.be/zWS2fCJGxmU


### Question :

https://leetcode.com/problems/snakes-and-ladders/