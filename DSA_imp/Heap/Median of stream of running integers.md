# Median of stream of running integers

The **median** is the middle value in an ordered integer list. If the size of the list is even, there is no middle value and the median is the mean of the two middle values.

- For example, for `arr = [2,3,4]`, the median is `3`.
- For example, for `arr = [2,3]`, the median is `(2 + 3) / 2 = 2.5`.

Implement the MedianFinder class:

- `MedianFinder()` initializes the `MedianFinder` object.
- `void addNum(int num)` adds the integer `num` from the data stream to the data structure.
- `double findMedian()` returns the median of all elements so far. Answers within `10-5` of the actual answer will be accepted.

**Example 1:**

<pre>
Input
["MedianFinder", "addNum", "addNum", "findMedian", "addNum", "findMedian"]
[[], [1], [2], [], [3], []]
Output
[null, null, null, 1.5, null, 2.0]

Explanation
MedianFinder medianFinder = new MedianFinder();
medianFinder.addNum(1);    // arr = [1]
medianFinder.addNum(2);    // arr = [1, 2]
medianFinder.findMedian(); // return 1.5 (i.e., (1 + 2) / 2)
medianFinder.addNum(3);    // arr[1, 2, 3]
medianFinder.findMedian(); // return 2.0
</pre>

### Approach (Using priority queue) :

1. We will divide the stream in two half
   1. First Half will use **maxHeap**
   2. Second Half will use **minHeap**

**Example:**
123456
123 -> maxHeap i.e it will give {3}
456 -> minHeap i.e it will give {4}

1. Firstly we will check whether the size of minHeap and maxHeap is same or not
2. Then check if size of maxHeap is 0 then store num in maxHeap. Else num is less than maxHeap.top() then store in maxHeap , else store in minHeap
3. If minHeap.size() > maxHeap.size() then we have two option to store either in minHeap or maxHeap

```cpp
class MedianFinder {
public:

    // We will use maxHeap to store first half and minHeap to store second half
    // 123456
    // 123 -> maxHeap i.e it will give {3}
    // 456 -> minHeap i.e it will give {4}

    priority_queue<int> maxHeap;
    priority_queue<int,vector<int>,greater<int>> minHeap;
    MedianFinder() {

    }

    void addNum(int num) {
        if(maxHeap.size()==minHeap.size())
        {
            if(maxHeap.size()==0)
            {
                maxHeap.push(num);
                return;
            }

            if(num<maxHeap.top())
                maxHeap.push(num);
            else
                minHeap.push(num);

}
        else
        {
            // two cases will be available :
            // 1. maxHeap size will be greater than minHeap
            //2. minHeap size will be greater than maxheap

            if(minHeap.size()>maxHeap.size())
            {
                if(num<=minHeap.top())
                {
                    maxHeap.push(num);
                }
                else
                {
                    int temp=minHeap.top();
                    minHeap.pop();
                    minHeap.push(num);
                    maxHeap.push(temp);
}
            }
            else
            {
                if(num>=maxHeap.top())
                    minHeap.push(num);
                else
                {
                    int temp=maxHeap.top();
                    maxHeap.pop();
                    maxHeap.push(num);
                    minHeap.push(temp);
                }
}
        }
    }

    double findMedian() {
        if(minHeap.size()==maxHeap.size())
            return (minHeap.top() + maxHeap.top())/2.0;
        else if(minHeap.size()>maxHeap.size())
            return minHeap.top();
        else
            return maxHeap.top();
    }
};
```

### Question :

https://leetcode.com/problems/find-median-from-data-stream/

### References :

https://www.youtube.com/watch?v=EcNbRjEcb14&ab_channel=KeertiPurswani
