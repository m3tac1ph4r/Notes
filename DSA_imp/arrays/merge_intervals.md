# Merge Intervals

Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return _an array of the non-overlapping intervals that cover all the intervals in the input_.

**Example 1:**

**Input:** intervals = [[1,3],[2,6],[8,10],[15,18]]
**Output:** [[1,6],[8,10],[15,18]]
**Explanation:** Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].

**Example 2:**

**Input:** intervals = [[1,4],[4,5]]
**Output:** [[1,5]]
**Explanation:** Intervals [1,4] and [4,5] are considered overlapping.

### Approach:

1. Sort the intervals.
2. Then extract the last element from result vector i.e start1 and end1, Then extract start2,end2 from given interval and check
	*  **if end1>start2** then find max of end1 and end2 and pop the start1,end1 and insert start1 and max(end1,end2)
	*  **else** insert {start2,end2}

![[DSA_imp/arrays/img/merge_intervals_approach.png]]

![[merge_intervals_approach2.png]]


```C++
int main()
{
    int n;
    cin >> n;
    vector<pair<int, int>> v;
    for (int i = 0; i < n; i++)
    {
        int x, y;
        cin >> x >> y;
        v.push_back({x, y});
    }
    sort(v.begin(), v.end());
    vector<pair<int, int>> s;
    s.push_back({v[0].first, v[0].second});
    for (int i = 1; i < n; i++)
    {
        int start1 = s[s.size() - 1].first;
        int end1 = s[s.size() - 1].second;
        int start2 = v[i].first;
        int end2 = v[i].second;
        if (end1 >= start2)
        {
            s.pop_back();
            end1 = max(end1, end2);
            s.push_back({start1, end1});
        }
        else
            s.push_back({start2, end2});
    }
    cout << s.size() << endl;
    for (int i = 0; i < s.size(); i++)
        cout << s[i].first << " " << s[i].second << endl;
    return 0;
}
```

### Question:
https://leetcode.com/problems/merge-intervals/


### Reference:
https://www.youtube.com/watch?v=2JzRBPFYbKE