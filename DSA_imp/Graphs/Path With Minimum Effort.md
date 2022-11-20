# Path with minimum effort
#dijkstra_algo 

You are a hiker preparing for an upcoming hike. You are given `heights`, a 2D array of size `rows x columns`, where `heights[row][col]` represents the height of cell `(row, col)`. You are situated in the top-left cell, `(0, 0)`, and you hope to travel to the bottom-right cell, `(rows-1, columns-1)` (i.e., **0-indexed**). You can move **up**, **down**, **left**, or **right**, and you wish to find a route that requires the minimum **effort**.

A route's **effort** is the **maximum absolute difference** in heights between two consecutive cells of the route.

Return _the minimum **effort** required to travel from the top-left cell to the bottom-right cell._

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/10/04/ex1.png)

**Input:** heights = [[1,2,2],[3,8,2],[5,3,5]]
**Output:** 2
**Explanation:** The route of [1,3,5,3,5] has a maximum absolute difference of 2 in consecutive cells.
This is better than the route of [1,2,2,2,5], where the maximum absolute difference is 3.

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/10/04/ex2.png)

**Input:** heights = [[1,2,3],[3,8,4],[5,3,5]]
**Output:** 1
**Explanation:** The route of [1,2,3,4,5] has a maximum absolute difference of 1 in consecutive cells, which is better than route [1,3,5,3,5].

**Example 3:**

![](https://assets.leetcode.com/uploads/2020/10/04/ex3.png)

**Input:** heights = [[1,2,1,1,1],[1,2,1,2,1],[1,2,1,2,1],[1,2,1,2,1],[1,1,1,2,1]]
**Output:** 0
**Explanation:** This route does not require any effort.




### Intuition :

We will use Dijkstra Algorithm to find the shortest path from source to destination. And use priority_queue min-heap to get the minimum one first. We have to find the minimum effort from (0,0) to (n-1,m-1)

### Approach
1. We will create distance matrix of size n * m for storing effort.
2. Then we will create a priority_queue using min-heap to get the minimum effort first. Priority_Queue will store {effort,{row,col}} where effort will be key
3. Distance[0][0] will be 0. So store {0,{0,0}} in priority_queue.
4. Start a while loop until queue is not empty
	1. Get the top element of priority_queue
	2. Check if row== n-1 and col== m-1 is *true* then update the ans.
	3. Else we will check for UP,LEFT,RIGHT,DOWN and update the distance matrix and add it into the queue.


### Code :

```cpp
class Solution {
public:
    int minimumEffortPath(vector<vector<int>>& heights) {
        priority_queue<pair<int,pair<int,int>>,vector<pair<int,pair<int,int>>>,
        greater<pair<int,pair<int,int>>>> pq;

        int n=heights.size();
        int m=heights[0].size();

        int delRow[4]={-1,0,1,0};
        int delCol[4]={0,1,0,-1};
        vector<vector<int>> distance(n,vector<int>(m,INT_MAX));
        
        pq.push({0,{0,0}});
        distance[0][0]=0;
        int ans=INT_MAX;
        while(!pq.empty())
        {
            int dist=pq.top().first;
            int row=pq.top().second.first;
            int col=pq.top().second.second;
            pq.pop();

            if(row==n-1 and col==m-1)
            {
                ans=min(ans,dist);
                continue;
                // return dist;
            }
            for(int i=0;i<4;i++)
            {
                int newRow=row+delRow[i];
                int newCol=col+delCol[i];
                
                if(newRow>=0 and newCol>=0 and newRow<n and newCol<m)
                {
                    int newEffort=max(abs(heights[newRow][newCol]-heights[row][col]),dist);
                    if(newEffort<distance[newRow][newCol])
                    {
                        distance[newRow][newCol]=newEffort;
                        pq.push({newEffort,{newRow,newCol}});
                    }
                }
            }
        }
        return ans==INT_MAX?0:ans;
    }
};
```


### Complexity
- Time complexity:
*n - number of rows in grid*
*m - number of cols in grid*
So time complexity of Dijkstra Algo is : $$O(ElogV)$$
where V is number of vertices in our case nodes are : $$n*m$$
E is number of edges, so in our case number of edges are : $$n*m*4$$ 
because every node has 4 direction edges UP, RIGHT, DOWN, LEFT
So **time complexity :** $$O((n*m*4)log(n*m))$$
- Space complexity: $$O(n*m)$$

### Link :
https://youtu.be/0ytpZyiZFhA?list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn


### Question :
https://leetcode.com/problems/path-with-minimum-effort/description/