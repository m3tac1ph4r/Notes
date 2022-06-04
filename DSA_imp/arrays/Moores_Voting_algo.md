# Moore's  Voting Algorithm

The **Boyer-Moore voting** algorithm is one of the popular optimal algorithms which is used to find the majority element among the given elements that have more than N/ 2 occurrences. This works perfectly fine for finding the majority element which takes 2 traversals over the given elements, which works in O(N) time complexity and O(1) space complexity

This algorithm works on the fact that if an element occurs more than N/2 times, it means that the remaining elements other than this would definitely be less than N/2. So let us check the proceeding of the algorithm.

-   First, choose a candidate from the given set of elements if it is the same as the candidate element, increase the votes. Otherwise, decrease the votes if votes become 0, select another new element as the new candidate.

**Intuition Behind Working :**  
When the elements are the same as the candidate element, votes are incremented when some other element is found not equal to the candidate element. We decreased the count. This actually means that we are decreasing the priority of winning ability of the selected candidate, since we know that if the candidate is a majority it occurs more than N/2 times and the remaining elements are less than N/2. We keep decreasing the votes since we found some different element than the candidate element. When votes become 0, this actually means that there are the same number of different elements, which should not be the case for the element to be the majority element. So the candidate element cannot be the majority, so we choose the present element as the candidate and continue the same till all the elements get finished. The final candidate would be our majority element. We check using the 2nd traversal to see whether its count is greater than N/2. If it is true, we consider it as the majority element.

**Step 1 –** Find a candidate with the majority –

-   Initialize a variable say **i ,votes = 0, candidate =-1** 
-   Traverse through the array using for loop
-   If **votes = 0,** choose the **candidate = arr[i]** , make **votes=1**.
-   else if the current element is the same as the candidate increment votes
-   else decrement votes.

**Step 2 –** Check if the candidate has more than N/2 votes –

-   Initialize a variable count =0 and increment count if it is the same as the candidate.
-   If the count is >N/2, return the candidate.
-   else return -1.


## Questions:

#### Majority Element N/2

Given an array `nums` of size `n`, return _the majority element_.

The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array.

**Example 1:**

**Input:** nums = [3,2,3]
**Output:** 3

**Example 2:**

**Input:** nums = [2,2,1,1,1,2,2]
**Output:** 2

```C++
int majority(vector<int> nums)
{
    int count = 0;
    int candidate = 0;

    for (int num : nums)
    {
        if (count == 0)
        {
            candidate = num;
        }
        if (num == candidate)
            count += 1;
        else
            count -= 1;
    }
    return candidate;
}
```


**Link :** https://leetcode.com/problems/majority-element/


#### Majority Element II :

Given an integer array of size `n`, find all elements that appear more than `⌊ n/3 ⌋` times.

**Example 1:**

**Input:** nums = [3,2,3]
**Output:** [3]

**Example 2:**

**Input:** nums = [1]
**Output:** [1]

**Example 3:**

**Input:** nums = [1,2]
**Output:** [1,2]

##### Approach (Extenstion of Boyre Moore's Voting Algorithm) :

```C++
vector<int> majorityElement(vector<int> nums)
{
    int count1=0,count2=0,num1=-1,num2=-1,i;
    for(i=0;i<nums.size();i++)
    {
        if(nums[i]==num1)
            count1++;
        else if(nums[i]==num2)
            count2++;
        else if(count1==0)
        {
            num1=nums[i];
            count1++;
        }
        else if(count2==0)
        {
            num2=nums[i];
            count2++;
        }
        else
        {
            count1--;
            count2--;
        }
    }
    vector<int> ans;
    count1=count2=0;
    for(i=0;i<nums.size();i++)
    {
        if(nums[i]==num1)
            count1++;
        else if(nums[i]==num2)
            count2++;
    }
    if(count1>nums.size()/3)
        ans.push_back(num1);
    if(count2>nums.size()/3)
        ans.push_back(num2);
    return ans;
}
```

**Link :** https://leetcode.com/problems/majority-element-ii/