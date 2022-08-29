# Longest K unique characters substring

Given a string you need to print the size of the longest possible substring that has exactly K unique characters. If there is no possible substring then print -1.

  
**Example 1:**

**Input:**
S = "aabacbebebe", K = 3
**Output:** 7
**Explanation**: "cbebebe" is the longest 
substring with K distinct characters.

**Example 2:**

**Input**: 
S = "aaaa", K = 2
**Output:** -1
**Explanation**: There's no substring with K
distinct characters.

### Approach 1 (Using sliding window) :

Firstly we will use set to count the number of distinct char in the string. If they are less than k means we have to return -1.
Then I used to map to store char and frequency of it. If size of the map is greater than k means we have to remove one char from left(starting). So we will decrease the frequency of the char from left and if frequency of char is 0 then delete that char from the map.

```cpp
class Solution{
  public:
    int longestKSubstr(string s, int k) {
        unordered_map<char,int> mp;
        int n=s.length();
        int left=0,ans=0;
        unordered_set<char> st;
        for(int i=0;i<n;i++)
        {
            st.insert(s[i]);
        }
        if(st.size()<k)
            return -1;
        for(int i=0;i<n;i++)
        {
            mp[s[i]]++;
            if(mp.size()>k)
            {
                while(mp[s[left]]>0 and left<i)
                {
                    mp[s[left]]--;
                    if(mp[s[left]]==0)
                    {
                        mp.erase(s[left]);
                        left++;
                        break;
                    }
                    left++;
                }
            }
            ans=max(ans,i-left+1);
        }
        return ans;
    }
};
```


### Question :
https://practice.geeksforgeeks.org/problems/longest-k-unique-characters-substring0853