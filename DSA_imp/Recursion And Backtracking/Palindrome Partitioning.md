# Palindrome Partitioning

Given a string `s`, partition `s` such that every substring of the partition is a **palindrome**. Return all possible palindrome partitioning of `s`.

A **palindrome** string is a string that reads the same backward as forward.

**Example 1:**

**Input:** s = "aab"
**Output:** [ ["a","a","b"],["aa","b"]]

**Example 2:**

**Input:** s = "a"
**Output:** [ ["a"]]


### Approach(Using Recursion and backtracking) :

![[palindrome_partitioning_ex1.png]]

![[palindrome_partitioning_ex2.png]]


```cpp
bool checkPalindrome(string s)
{
    int start = 0;
    int end = s.size() - 1;
    while (start <= end)
    {
        if (s[start++] != s[end--])
            return false;
    }
    return true;
}
void solve(string s, vector<string> &temp, vector<vector<string>> &ans)
{
    if (s.length() == 0)
    {
        ans.push_back(temp);
        return;
    }
    for (int i = 0; i < s.length(); i++)
    {
        string subString = s.substr(0, i + 1);
        if (checkPalindrome(subString))
        {
            temp.push_back(subString);
            solve(s.substr(i + 1), temp, ans);
            temp.pop_back();
        }
    }
}
vector<vector<string>> partition(string s)
{
    vector<vector<string>> ans;
    vector<string> temp;
    solve(s, temp, ans);
    return ans;
}
```


### Question :
https://leetcode.com/problems/palindrome-partitioning/

### Reference :
https://youtu.be/pkBG7lB-1N8