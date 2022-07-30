# SeanPrashad LeetCode Patterns TIPS

**Link :** https://seanprashad.com/leetcode-patterns/

### If in question it is asked to find maximum of a should be minimum

* Binary search
<pre>
> You have to allocate books to **B** number of students so that maximum number of pages alloted to a student is minimum.
> such that the minimum distance between any two of them is as large as possible. Return the largest minimum distance
</pre>

### If input array is sorted then 
- Binary search
- Two pointers

### If asked for all permutations/subsets then
- Backtracking

### If given a tree then
- DFS
- BFS

### If given a graph then
- DFS
- BFS
- > **Whereever SHORTEST OR MINIMUM word is there means we have to use bfs**

### If given a linked list then
- Two pointers

### If you are asked to try all possible ways
* Recursion
* DP


### If recursion is banned then
- Stack

### If must solve in-place then
- Swap corresponding values
- Store one or more different values in the same pointer

### If asked for maximum/minimum subarray/subset/options then
- Dynamic programming

### If asked for top/least K items then
- Heap

### If asked for common strings then
- Map
- Trie

### Else
- Map/Set for O(1) time & O(n) space
- Sort input for O(nlogn) time and O(1) space
