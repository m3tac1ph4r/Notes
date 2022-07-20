# Remove Invalid Parentheses
#leetcode-hard


Given a string `s` that contains parentheses and letters, remove the minimum number of invalid parentheses to make the input string valid.

Return _all the possible results_. You may return the answer in **any order**.

**Example 1:**

**Input:** s = "()())()"
**Output:** ["(())()","()()()"]

**Example 2:**

**Input:** s = "(a)())()"
**Output:** [ "(a())()","(a)()()" ]

**Example 3:**

**Input:** s = ")("
**Output:** [""]



### Approach (Stack and recusion) :

![[remove_valid_parenthesis_app.png]]

1. We will count the  minimum number of invalid charachter required to delete to make paranthesis balanced
2. We will use an **unordered_map<string,int>** for storing string and count. We will use map to prevent repetitions of same string. If we have checked string s is invalid then again we will not check.
3. In SOLVE():
	1. We will check whether string s is present in map or not. If YES then return else STORE IN THE MAP
	2. Then check **minInvalid char is less 0** , if TRUE then RETURN
	3. Then check **minInvalid char is equal to  0** ,if the string is valid then add in the result and then return
	4. Then start a for loop from 0 to string size. And remove one character and then call for (minInvalid-1) bcz now the minimum invalid chars will be decrease by one

```C++

class Solution {
public:
    vector<string> res;
    unordered_map<string,int> mp;
    int getInvalid(string s)
    {
        if(s.length()==0)
            return 0;
        stack<char> st;
        for(auto ch:s)
        {
            if(ch=='(')
                st.push(ch);
            else if(ch==')')
            {
                if(!st.empty() and st.top()=='(')
                    st.pop();
                else
                    st.push(')');
            }
        }
        return st.size();
    }
    void solve(string s,int minInvalid)
    {
        if(mp[s]==0)
            mp[s]++;
        else
            return;
        if(minInvalid<0)
            return;
        if(minInvalid==0)
        {
            if(getInvalid(s)==0)
                res.push_back(s);
            return;
        }
        
        for(int i=0;i<s.size();i++)
        {
            string left=s.substr(0,i);
            string right=s.substr(i+1);
            solve(left+right,minInvalid-1);
        }
        return;
    }
    vector<string> removeInvalidParentheses(string s) {
        solve(s,getInvalid(s));
        return res;
    }
};
```

### Question :
https://leetcode.com/problems/remove-invalid-parentheses/


### Reference :
https://youtu.be/y7Us-H5um0M