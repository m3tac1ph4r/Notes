# Longest Repeating Character Replacement

You are given a string `s` and an integer `k`. You can choose any character of the string and change it to any other uppercase English character. You can perform this operation at most `k` times.

Return _the length of the longest substring containing the same letter you can get after performing the above operations_.

**Example 1:**

**Input:** s = "ABAB", k = 2
**Output:** 4
**Explanation:** Replace the two 'A's with two 'B's or vice versa.

**Example 2:**

**Input:** s = "AABABBA", k = 1
**Output:** 4
**Explanation:** Replace the one 'A' in the middle with 'B' and form "AABBBBA".
The substring "BBBB" has the longest repeating letters, which is 4.


### Approach (Using Sliding Window) :

```cpp
class Solution {
public:
    int characterReplacement(string s, int k) {
        int left=0,right=0;
        int maxFrq=0;
        int n=s.length();
        int maxLen=0;
        map<char,int> mp;
        while(right<n)
        {
            mp[s[right]]++;
            maxFrq=max(maxFrq,mp[s[right]]);
            int currLen=right-left+1;
            while(currLen-maxFrq>k)
            {
                mp[s[left]]--;
                maxFrq=max(maxFrq,mp[s[left]]);
                left++;
                currLen=right-left+1;
            }
            maxLen=max(maxLen,right-left+1);
            right++;
        }
        return maxLen;
        
    }
};
```


### Question :
https://leetcode.com/problems/longest-repeating-character-replacement/

### Reference :
https://youtu.be/gqXU1UyA8pk