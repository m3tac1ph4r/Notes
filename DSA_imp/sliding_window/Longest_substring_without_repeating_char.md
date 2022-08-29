# Longest Substring without repeating char

Given a string `s`, find the length of the **longest substring** without repeating characters.

**Example 1:**

**Input:** s = "abcabcbb"
**Output:** 3
**Explanation:** The answer is "abc", with the length of 3.

**Example 2:**

**Input:** s = "bbbbb"
**Output:** 1
**Explanation:** The answer is "b", with the length of 1.

**Example 3:**

**Input:** s = "pwwkew"
**Output:** 3
**Explanation:** The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.



### Approach 1 (Using sliding window) :

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
         unordered_set<char> st;
    int l=0,max_len=0;
    for(int i=0;i<s.length();i++)
    {
        if(st.find(s[i])!=st.end())
        {
            while(l<i and st.find(s[i])!=st.end())
            {
                st.erase(s[l]);
                l++;
            }
        }
            st.insert(s[i]);
            max_len=max(max_len,i-l+1);
    }
    return max_len;   
    }
};
```


### Question :
https://leetcode.com/problems/longest-substring-without-repeating-characters/