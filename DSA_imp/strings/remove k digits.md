# Remove k Digits

Given string num representing a non-negative integer `num`, and an integer `k`, return _the smallest possible integer after removing_ `k` _digits from_ `num`.

**Example 1:**

**Input:** num = "1432219", k = 3
**Output:** "1219"
**Explanation:** Remove the three digits 4, 3, and 2 to form the new number 1219 which is the smallest.

**Example 2:**

**Input:** num = "10200", k = 1
**Output:** "200"
**Explanation:** Remove the leading 1 and the number is 200. Note that the output must not contain leading zeroes.

**Example 3:**

**Input:** num = "10", k = 2
**Output:** "0"
**Explanation:** Remove all the digits from the number and it is left with nothing which is 0.


### Approach (Using stack):

We will  remove k digits from starting bcz they are on the higher place.


```cpp
 string removeKdigits(string num, int k) {

   if (k >= num.size()) return "0";

   stack < char > s;

   for (int i = 0; i < num.size(); i++) {
     if (s.empty()) s.push(num[i]);
     else {
       while (!s.empty() && s.top() > num[i] && k > 0) {
         s.pop();
         k--;
       }
       s.push(num[i]);
     }
   }

   while (k > 0) {
     s.pop();
     k--;
   }

   if (s.empty()) return "0";

   string ans;
   while (!s.empty()) {
     ans = s.top() + ans;
     s.pop();
   }

   int i = 0;
   while (ans[i] == '0') {
     i++;
   }

   return (ans.substr(i) == "") ? "0" : ans.substr(i);
 }
```



### Question :
https://leetcode.com/problems/remove-k-digits/

### Reference :
https://youtu.be/hJnpt4_-DsI