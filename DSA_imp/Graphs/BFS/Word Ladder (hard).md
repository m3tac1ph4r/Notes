# Word Ladder - leetcode Hard

A **transformation sequence** from word `beginWord` to word `endWord` using a dictionary `wordList` is a sequence of words `beginWord -> s1 -> s2 -> ... -> sk` such that:

- Every adjacent pair of words differs by a single letter.
- Every `si` for `1 <= i <= k` is in `wordList`. Note that `beginWord` does not need to be in `wordList`.
- `sk == endWord`

Given two words, `beginWord` and `endWord`, and a dictionary `wordList`, return *the **number of words** in the **shortest transformation sequence** from* `beginWord` *to* `endWord`*, or* `0` *if no such sequence exists.*

**Example 1:**

**Input:** beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
**Output:** 5
**Explanation:** One shortest transformation sequence is "hit" -> "hot" -> "dot" -> "dog" -> cog", which is 5 words long.

**Example 2:**

**Input:** beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]
**Output:** 0
**Explanation:** The endWord "cog" is not in wordList, therefore there is no valid transformation sequence.

### Approach (BFS) :

![[word_ladder_app.png]]

```cpp

int ladderLength(string beginWord, string endWord, vector<string> &wordList)
{

    queue<pair<string, int>> q;
    unordered_set<string> st(wordList.begin(), wordList.end());
    q.push({beginWord, 1});
    while (!q.empty())
    {
        string word = q.front().first;
        int ladder = q.front().second;
        q.pop();
        if (word == endWord)
            return ladder;
        st.erase(word);
        for (int i = 0; i < word.size(); i++)
        {
            char ch = word[i];
            for (int j = 0; j < 26; j++)
            {
                word[i] = 'a' + j;
                if (st.find(word) != st.end())
                {
                    q.push({word, ladder + 1});
                }
            }
            word[i] = ch;
        }
    }
    return 0;
}
```

### Question

https://leetcode.com/problems/word-ladder/

### Reference

https://youtu.be/Lu7xJ94m5tU
