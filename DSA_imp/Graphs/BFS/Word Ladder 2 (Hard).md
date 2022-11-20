# Word Ladder 2
#interesting 

A **transformation sequence** from word `beginWord` to word `endWord` using a dictionary `wordList` is a sequence of words `beginWord -> s1 -> s2 -> ... -> sk` such that:

-   Every adjacent pair of words differs by a single letter.
-   Every `si` for `1 <= i <= k` is in `wordList`. Note that `beginWord` does not need to be in `wordList`.
-   `sk == endWord`

Given two words, `beginWord` and `endWord`, and a dictionary `wordList`, return _all the **shortest transformation sequences** from_ `beginWord` _to_ `endWord`_, or an empty list if no such sequence exists. Each sequence should be returned as a list of the words_ `[beginWord, s1, s2, ..., sk]`.

**Example 1:**

**Input:** beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log","cog"]
**Output:** [ ["hit","hot","dot","dog","cog"],["hit","hot","lot","log","cog"] ]
**Explanation:** There are 2 shortest transformation sequences:
"hit" -> "hot" -> "dot" -> "dog" -> "cog"
"hit" -> "hot" -> "lot" -> "log" -> "cog"

**Example 2:**

**Input:** beginWord = "hit", endWord = "cog", wordList = ["hot","dot","dog","lot","log"]
**Output:** []
**Explanation:** The endWord "cog" is not in wordList, therefore there is no valid transformation sequence.


### Approach 1 (Using BFS + level Queue) :

1. We will add some logic in previous code of Word Ladder 1
2. This time we will create a `queue<vector<string>>` to store the pattern of word change
3. And we will use usedOnLevel `vector<string>` to store the word which are used in that level, then erase all word in next level.


**Queue Structure :**
![[queue_structure.png]]
As you can why in *for loop* I added the word then inserted the updated vector in queue and then pop_back that word from the queue. Because we have to insert the new word in the existing vector and then insert that in the queue.


```cpp
class Solution {
public:
    vector<vector<string>> findLadders(string beginWord, string endWord, 
    vector<string>& wordList) {
        unordered_set<string> st(wordList.begin(),wordList.end());
        queue<vector<string>> q;
        q.push({beginWord});
        vector<string> usedOnLevel;
        usedOnLevel.push_back(beginWord);
        int level=0;
        vector<vector<string>> ans;

        while(!q.empty())
        {
            vector<string> vec=q.front();
            q.pop();
            
            // erase all the words that are used in previous levels
            if(vec.size()>level)
            {
                level++;
                for(auto it:usedOnLevel)
                    st.erase(it);
                usedOnLevel.clear();
            }

            string word=vec.back();
            if(word==endWord)
            {
                // first sequence or check other sequence is equal to the previous sequence
                if(ans.size()==0 || ans[0].size()==vec.size())
                    ans.push_back(vec);
                else
                    continue;
            }

            for(int i=0;i<word.size();i++)
            {
                char ch=word[i];
                for(char j='a';j<='z';j++)
                {
                    word[i]=j;
                    if(st.count(word)>0)
                    {
                        vec.push_back(word);
                        q.push(vec);
                        usedOnLevel.push_back(word);
                        vec.pop_back();
                    }
                }
                word[i]=ch;
            }
        }
        return ans;
    }
};
```


### Optimized Code(Using DFS and map)


```cpp
class Solution {
public:
    unordered_map<string,int> mp;
    vector<vector<string>> ans;

    void dfs(string word,string beginWord,vector<string> &vec)
    {
        if(word==beginWord)
        {
            reverse(vec.begin(),vec.end());
            ans.push_back(vec);
            reverse(vec.begin(),vec.end());
            return;
        }
        int level=mp[word];
        int sz=word.size();
        for(int i=0;i<sz;i++)
        {
            char ch=word[i];
            for(char newCh='a';newCh<='z';newCh++)
            {
                word[i]=newCh;
                if(mp.find(word)!=mp.end() and mp[word]+1==level)
                {
                    vec.push_back(word);
                    dfs(word,beginWord,vec);
                    vec.pop_back();
                }
            }
            word[i]=ch;
        }
    }
    vector<vector<string>> findLadders(string beginWord, string endWord, 
    vector<string>& wordList) {
        unordered_set<string> st(wordList.begin(),wordList.end());
        int bw_size=beginWord.size();
        queue<string> q;
        q.push(beginWord);
        mp[beginWord]=1;
        st.erase(beginWord);
        while(!q.empty())
        {
            string word=q.front();
            int level=mp[word];
            q.pop();
            if(word==endWord)
                break;
            for(int i=0;i<bw_size;i++)
            {
                char ch=word[i];
                for(char newCh='a';newCh<='z';newCh++)
                {
                    word[i]=newCh;
                    if(st.find(word)!=st.end())
                    {
                        q.push(word);
                        st.erase(word);
                        mp[word]=level+1;
                    }
                }
                word[i]=ch;
            }
        }
        if(mp.find(endWord)!=mp.end())
        {
            vector<string> vec;
            vec.push_back(endWord);
            dfs(endWord,beginWord,vec);
        }

        return ans;
    }
};
```



### Link :
https://youtu.be/DREutrv2XD0?list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn

*Optimized Code Link*
https://youtu.be/AD4SFl7tu7I?list=PLgUwDviBIf0oE3gA41TKO2H5bHpPd7fzn

### Question :
In leetcode only optimized solution will be accepted.
https://leetcode.com/problems/word-ladder-ii/description/
https://practice.geeksforgeeks.org/problems/word-ladder-ii/1