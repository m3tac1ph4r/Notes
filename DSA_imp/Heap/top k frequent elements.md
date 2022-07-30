# Top k frequent elements

Given an integer array `nums` and an integer `k`, return _the_ `k` _most frequent elements_. You may return the answer in **any order**.

**Example 1:**

**Input:** nums = [1,1,1,2,2,3], k = 2
**Output:** [1,2]

**Example 2:**

**Input:** nums = [1], k = 1
**Output:** [1]

### Approach

We will use min heap using priority queue.

```cpp
vector<int> topKFrequents(vector<int> nums,int k)
{
    vector<int> ans;
    if(nums.size()==1)
    {
        ans.push_back(nums[0]);
        return ans;
    }
    priority_queue<pair<int,int>,vector<pair<int,int>>,greater<pair<int,int>>> pq;
    unordered_map<int,int> m;
    for(auto i:nums)
        m[i]++;
    for(auto i:m)
    {
        pq.push({i.second,i.first});  // count is key and number is value in min_heap
        if(pq.size()>k)	//removing whose size is smaller than k elements from min_heap
            pq.pop();
    }
    while (k--)
    {
        ans.push_back(pq.top().second);
        pq.pop();
    }
    return ans;
}
```
