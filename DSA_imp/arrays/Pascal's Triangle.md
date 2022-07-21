# Pascal's Triangle

Given an integer `numRows`, return the first numRows of **Pascal's triangle**.

In **Pascal's triangle**, each number is the sum of the two numbers directly above it as shown:

![](pascalTriangleAnimated2.gif)

**Example 1:**

**Input:** numRows = 5
**Output:** [[1],[1,1],[1,2,1],[1,3,3,1],[1,4,6,4,1]]

**Example 2:**

**Input:** numRows = 1
**Output:** [[1]]

### Code :

```cpp
vector<vector<int>> generate(int numRows)
{
    vector<vector<int>> ans;
    ans.push_back({1});
    if (numRows == 1)
        return ans;
    ans.push_back({1, 1});
    if (numRows == 2)
        return ans;
    ans.push_back({1, 2, 1});
    vector<int> temp = {1, 2, 1};
    vector<int> temp2;
    for (int j = 3; j < numRows; j++)
    {
        temp2.push_back(temp[0]);
        for (int i = 1; i < temp.size(); i++)
        {
            temp2.push_back(temp[i - 1] + temp[i]);
        }
        temp2.push_back(temp[temp.size() - 1]);
        ans.push_back(temp2);
        temp = temp2;
        temp2 = {};
    }
    return ans;
}
```

### Question:

https://leetcode.com/problems/pascals-triangle/
