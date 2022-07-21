# Kth largest element in a stream

Design a class to find the `kth` largest element in a stream. Note that it is the `kth` largest element in the sorted order, not the `kth` distinct element.

Implement `KthLargest` class:

- `KthLargest(int k, int[] nums)` Initializes the object with the integer `k` and the stream of integers `nums`.
- `int add(int val)` Appends the integer `val` to the stream and returns the element representing the `kth` largest element in the stream.

**Example 1:**

<pre>
Input
["KthLargest", "add", "add", "add", "add", "add"]
[[3, [4, 5, 8, 2]], [3], [5], [10], [9], [4]]
Output
[null, 4, 5, 5, 8, 8]

Explanation
KthLargest kthLargest = new KthLargest(3, [4, 5, 8, 2]);
kthLargest.add(3);   // return 4
kthLargest.add(5);   // return 5
kthLargest.add(10);  // return 5
kthLargest.add(9);   // return 8
kthLargest.add(4);   // return 8
</pre>

### Approach

We will use min heap using priority queue.
![[kth_largest_element.png]]

```cpp
class KthLargest {
public:
    priority_queue<int,vector<int>,greater<int>> pq; //min heap
    int size;
    KthLargest(int k, vector<int>& nums) {
        size=k;
        for(int i=0;i<nums.size();i++)
        {
            pq.push(nums[i]);
            if(pq.size()>k)
                pq.pop();
}
    }
    int add(int val) {
        pq.push(val);
        if(pq.size()>size)
            pq.pop();
        return pq.top();
    }
};
```

### Question

https://leetcode.com/problems/kth-largest-element-in-a-stream/

### Reference

https://youtu.be/0tFmP1Eiilg
