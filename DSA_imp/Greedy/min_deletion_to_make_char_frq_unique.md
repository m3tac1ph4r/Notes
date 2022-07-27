# Minimum Deletions to Make Character Frequencies Unique

A string `s` is called **good** if there are no two different characters in `s` that have the same **frequency**.

Given a string `s`, return _the **minimum** number of characters you need to delete to make_ `s` _**good**._

The **frequency** of a character in a string is the number of times it appears in the string. For example, in the string `"aab"`, the **frequency** of `'a'` is `2`, while the **frequency** of `'b'` is `1`.

**Example 1:**

**Input:** s = "aab"
**Output:** 0
**Explanation:** `s` is already good.

**Example 2:**

**Input:** s = "aaabbbcc"
**Output:** 2
**Explanation:** You can delete two 'b's resulting in the good string "aaabcc".
Another way it to delete one 'b' and one 'c' resulting in the good string "aaabbc".

**Example 3:**

**Input:** s = "ceabaacb"
**Output:** 2
**Explanation:** You can delete both 'c's resulting in the good string "eabaab".
Note that we only care about characters that are still in the string at the end (i.e. frequency of 0 is ignored).


### Approach :

![[min_deletion_to_make_frq_unique_app.png]]

1. We will store all the frequencies in the vector. And then sort them in descending order.
2. Then declare variable **cuttOff=max_frq**. The cuttOff frq checks whether the frq[i] of ith char is unique or not.
3. If **frq[i] is less than cuttOff frequency** means *frq[i] is unique and we don't need to delete any char from the string*. 
4. Else if frq[i] is greater than cuttOff frequency means *frq[i] is repeated and previous char has already have that frequency.* 
	1. If **cuttOff frq is greater than 0** means *deleting some character will give the unique frq to ith alphabet*
	2. Else *means we have to delete all the frequency of that specific alphabet.*
5. Update the cuttOff by minimum of (decreasing of cuttOff  by 1) or (frq[i]-1)

**Why we will update the cuttOff by frq[i]-1 ?**
Because suppose frequency array is :

| 9 | 4 | 2 |
|---|---|---|

If we update cutOff by decreasing by 1 i.e 8. And the next frequency is 4. Then all the frequencies ranging from 8...to...4 will  be empty. Means we have to update the cuttOff according to the last frequency[i].

![[unique_frq_why.png]]


```cpp
int minDeletions(string s)
{
    vector<int> frq(26, 0);

    for (int i = 0; i < s.length(); i++)
    {
        frq[s[i] - 'a']++;
    }

    sort(frq.begin(), frq.end(), greater<int>());

    int ans = 0, cuttOff = frq[0];
    for (int i = 0; i < frq.size(); i++)
    {
        if (frq[i] > cuttOff)
        {
            if (cuttOff > 0)
            {
                ans += frq[i] - cuttOff;
            }
            else
                ans += frq[i];
        }
        cuttOff = min(frq[i] - 1, cuttOff - 1);
    }
    return ans;
}
```

### Question :
https://leetcode.com/problems/minimum-deletions-to-make-character-frequencies-unique/

### Reference :
https://youtu.be/xzsAFSFiVF8