# Maximum Points You Can Obtain from Cards

There are several cards **arranged in a row**, and each card has an associated number of points. The points are given in the integer array `cardPoints`.

In one step, you can take one card from the beginning or from the end of the row. You have to take exactly `k` cards.

Your score is the sum of the points of the cards you have taken.

Given the integer array `cardPoints` and the integer `k`, return the *maximum score* you can obtain.

**Example 1:**

**Input:** cardPoints = [1,2,3,4,5,6,1], k = 3
**Output:** 12
**Explanation:** After the first step, your score will always be 1. However, choosing the rightmost card first will maximize your total score. The optimal strategy is to take the three cards on the right, giving a final score of 1 + 6 + 5 = 12.

![[maximum_points_ex.png]]

![[max_points_from_card_app2.png]]
### Approach :

1. We will find sum of first k elements of array.
2. Then will traverse k-1 to 0
   1. Remove ith element from the window
   2. Add (n-k+i)th element from last of array to the window. Then update the max_sum

```cpp
class Solution {
public:
    int maxScore(vector<int>& cardPoints, int k) {
        int sum=0;
        int max_sum=0;
        int n=cardPoints.size();
        for(int i=0;i<k;i++){
            sum+=cardPoints[i];
        }
        max_sum=sum;
        for(int i=k-1;i>=0;i--){
            sum-=cardPoints[i];
            sum+=cardPoints[n-k+i];
            max_sum=max(sum,max_sum);
        }
        return max_sum;
    }
};
```

### Question :

https://leetcode.com/problems/maximum-points-you-can-obtain-from-cards/
