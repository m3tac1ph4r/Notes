# Group Anagrams :

Given an array of strings `strs`, group **the anagrams** together. You can return the answer in **any order**.

An **Anagram** is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

**Example 1:**

**Input:** strs = ["eat","tea","tan","ate","nat","bat"]
**Output:** [ ["bat"],["nat","tan"],["ate","eat","tea"]]

**Example 2:**

**Input:** strs = [""]
**Output:** [ [""]]

**Example 3:**

**Input:** strs = ["a"]
**Output:** [ ["a"]]


### Approach (Using Map and Sorting) :

1. We will create a map of string as key and `vector<int>` as value.
2. Then sort the string and add the index of string in map.
3. Then traverse the map and add all same anagram in vector.

```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        vector<vector<string>> ans;
        unordered_map<string,vector<int>> mp;
        for(int i=0;i<strs.size();i++){
            string str=strs[i];
            sort(str.begin(),str.end());
            mp[str].push_back(i);
        }
        for(auto a : mp){
            vector<string> temp;
            for(auto b : a.second){
                temp.push_back(strs[b]);
            }
            ans.push_back(temp);
        }
        return ans;
    }
};
```



### Question :
https://leetcode.com/problems/group-anagrams/