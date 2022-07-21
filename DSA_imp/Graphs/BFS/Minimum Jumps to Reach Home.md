# Minimum Jumps to Reach Home

> **Whereever SHORTEST OR MINIMUM word is there means we have to use bfs**

A certain bug's home is on the x-axis at position `x`. Help them get there from position `0`.

The bug jumps according to the following rules:

- It can jump exactly `a` positions **forward** (to the right).
- It can jump exactly `b` positions **backward** (to the left).
- It cannot jump backward twice in a row.
- It cannot jump to any `forbidden` positions.

The bug may jump forward **beyond** its home, but it **cannot jump** to positions numbered with **negative** integers.

Given an array of integers `forbidden`, where `forbidden[i]` means that the bug cannot jump to the position `forbidden[i]`, and integers `a`, `b`, and `x`, return *the minimum number of jumps needed for the bug to reach its home*. If there is no possible sequence of jumps that lands the bug on position `x`, return `-1.`

**Example 1:**

**Input:** forbidden = [14,4,18,1,15], a = 3, b = 15, x = 9
**Output:** 3
**Explanation:** 3 jumps forward (0 -> 3 -> 6 -> 9) will get the bug home.

**Example 2:**

**Input:** forbidden = [8,3,16,6,12,20], a = 15, b = 13, x = 11
**Output:** -1

**Example 3:**

**Input:** forbidden = [1,6,2,14,5,17,4], a = 16, b = 9, x = 7
**Output:** 2
**Explanation:** One jump forward (0 -> 16) then one jump backward (16 -> 7) will get the bug home.

### Approach :

1. We will use queue to store the {number,state}. State will be of two types
   1. **true - for forward**
   2. **false - for backward**
2. And we will use set instead of visited array, because we can't make array of size more than 6000 . Because SET will take less space complexity and it will do operations in O(1) TIME

```cpp

int minimumJumps(vector<int> &forbidden, int a, int b, int x)
{
    queue<pair<int, bool>> q;
    unordered_set<int> st(forbidden.begin(), forbidden.end());
    st.insert(0);

    q.push({0, true});
    int steps = 0;

    while (!q.empty())
    {
        int size = q.size();
        while (size--)
        {
            auto front = q.front();
            q.pop();

            if (front.first == x)
                return steps;

            // forward
            int forward_pos = front.first + a;
            if (forward_pos <= 6000 and st.count(forward_pos) == 0)
            {
                q.push({forward_pos, true});
                st.insert(forward_pos);
            }

            // backward
            int backward_pos = front.first - b;
            if (front.second == true and backward_pos <= 6000 and backward_pos >= 0 and st.count(backward_pos) == 0)
            {
                q.push({backward_pos, false});
            }
        }

        steps++;
    }
    return -1;
}
```

### Question :

https://leetcode.com/problems/minimum-jumps-to-reach-home/
