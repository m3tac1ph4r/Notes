# Longest Valid Parenthesis

Given a string containing just the characters `'('` and `')'`, find the length of the longest valid (well-formed) parentheses substring.

**Example 1:**

**Input:** s = "(()"
**Output:** 2
**Explanation:** The longest valid parentheses substring is "()".

**Example 2:**

**Input:** s = ")()())"
**Output:** 4
**Explanation:** The longest valid parentheses substring is "()()".

**Example 3:**

**Input:** s = ""
**Output:** 0

### Approach 1(Using stacks) :

Instead of finding every possible string and checking its validity, we can make use of a stack while scanning the given string to:

1.  Check if the string scanned so far is valid.
2.  Find the length of the longest valid string.

In order to do so, we start by pushing -1−1 onto the stack. For every \text{‘(’}‘(’ encountered, we push its index onto the stack.

For every \text{‘)’}‘)’ encountered, we pop the topmost element. Then, the length of the currently encountered valid string of parentheses will be the difference between the current element's index and the top element of the stack.

If, while popping the element, the stack becomes empty, we will push the current element's index onto the stack. In this way, we can continue to calculate the length of the valid substrings and return the length of the longest valid string at the end.

```cpp
    int longestValidParentheses(string s) {
        int max_len=0;
        stack<int> nums;
        nums.push(-1);
        for(int i=0;i<s.length();i++)
        {
            if(s[i]=='(')
                nums.push(i);
            else
            {
                nums.pop();
                if(nums.empty())
                    nums.push(i);
                else
                    max_len=max(max_len,i-nums.top());
			}
		}
        return max_len;
	}
```

**Complexity Analysis**

- Time complexity: O(n). n is the length of the given string.
- Space complexity: O(n). The size of stack can go up to nn.

### Appproach 2(Without extra Space) :

In this approach, we make use of two counters left and right. First, we start traversing the string from the left towards the right and for every \text{‘(’}‘(’ encountered, we increment the leftleft counter and for every \text{‘)’}‘)’ encountered, we increment the rightright counter. Whenever leftleft becomes equal to rightright, we calculate the length of the current valid string and keep track of maximum length substring found so far. If rightright becomes greater than leftleft we reset leftleft and rightright to 00.

Next, we start traversing the string from right to left and similar procedure is applied.

```cpp
  int longestValidParentheses(string s) {
        int left=0,right=0;
        int max_len=0;
        for(int i=0;i<s.length();i++)
        {
            if(s[i]=='(')
                left++;
            else if(s[i]==')')
                right++;
            if(left==right)
                max_len=max(max_len,2*right);
            else if(right>left)
            {
                left=0;
                right=0;
			}
        }
        left=right=0;
        for(int i=s.length()-1;i>=0;i--)
        {
            if(s[i]=='(')
                left++;
            else if(s[i]==')')
                right++;
            if(left==right)
                max_len=max(max_len,2*left);
            else if(left>right)
            {
                left=0;
                right=0;
			}
		}
        return max_len;
    }
```

**Complexity Analysis**

- Time complexity: O(n)O(n). Two traversals of the string.
- Space complexity: O(1)O(1). Only two extra variables leftleft and rightright are needed.

### Question :

https://leetcode.com/problems/longest-valid-parentheses/
