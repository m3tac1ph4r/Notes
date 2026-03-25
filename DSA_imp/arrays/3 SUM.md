# 3 SUM

Given an integer array nums, return all the triplets `[nums[i], nums[j], nums[k]]` such that `i != j`, `i != k`, and `j != k`, and `nums[i] + nums[j] + nums[k] == 0`.

Notice that the solution set must not contain duplicate triplets.

**Example 1:**
**Input:** nums = [-1,0,1,2,-1,-4]
**Output:** [[-1,-1,2],[-1,0,1]]
**Explanation:** 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.

**Example 2:**
**Input:** nums = [0,1,1]
**Output:** []
**Explanation:** The only possible triplet does not sum up to 0.

**Example 3:**

**Input:** nums = [0,0,0]
**Output:** [ [0,0,0] ]
**Explanation:** The only possible triplet sums up to 0.

### Bruteforce Approach :
You can run three loops and then find all the unique elements using HashSet. But time complexity will O(n3).

### Optimized Approach :
#### The Logic: Two Loops + Hashing
1. **Fix the first element (`i`):** Run an outer loop to pick the first number.
2. **Search for the pair (`j`):** Run an inner loop starting from $i + 1$.
3. **The Math:** For every pair $(nums[i], nums[j])$, calculate the required third value:
    > $Target = -(nums[i] + nums[j])$
4. **The Set Check:**
    - Look at your "history" (the `HashSet`).
    - **If Target exists:** You found a triplet! Sort it and add it to your results.
    - **If Target doesn't exist:** Move on.
5. **Update History:** Always add the current `nums[j]` to the `HashSet` _after_ checking for the target. This ensures you don't use the same element twice for the same triplet, but keep it available for future pairs in that same outer loop.

**Why do we reset the `HashSet` inside the first loop?**
You must create a `new HashSet<Integer>()` at the start of every `i` iteration. This is because the "third element" ($nums[k]$) must always be a number that exists _between_ index $i$ and index $j$. If you don't reset it, you might accidentally pick a number from a previous, unrelated iteration.
#### Dry Run
**Input:** `nums = [-1, 0, 1, 2]`
**Goal:** Find triplets that sum to `0`.

---
##### **Iteration 1: `i = 0` (nums[i] = -1)**
- **Target** we need to find: $-( -1 + nums[j] )$
- **`existingSet`**: `[]` (Empty at start of every `i` loop)
- **`j = 1` (nums[j] = 0):**
    - Need: $-( -1 + 0 ) = 1$
    - Is `1` in `existingSet`? **No**.
    - Add `nums[j]` to `existingSet`: `[0]`

- **`j = 2` (nums[j] = 1):**    
    - Need: $-( -1 + 1 ) = 0
    - Is `0` in `existingSet`? **Yes!**
    - **Triplet Found:** `[-1, 0, 1]`
    - Add `nums[j]` to `existingSet`: `[0, 1]`
    
- **`j = 3` (nums[j] = 2):**
    - Need: $-( -1 + 2 ) = -1
    - Is `-1` in `existingSet`? **No**.
    - Add `nums[j]` to `existingSet`: `[0, 1, 2]`
---
##### **Iteration 2: `i = 1` (nums[i] = 0)**
- **`existingSet`**: `[]` (Reset!)
- **`j = 2` (nums[j] = 1):**
    - Need: $-( 0 + 1 ) = -1
    - Is `-1` in `existingSet`? **No**.
    - Add `1` to `existingSet`: `[1]`
- **`j = 3` (nums[j] = 2):**
    - Need: $-( 0 + 2 ) = -2
    - Is `-2` in `existingSet`? **No**.
    - Add `2` to `existingSet`: `[1, 2]`
---
#### Key Takeaways for your Notes
- **The Look-Back:** When we are at index `j`, we are looking back at the values between `i` and `j` to see if our missing piece exists.
- **Order Matters:** We check the `existingSet` **before** adding the current `nums[j]`. This prevents us from using the same element at index `j` twice to satisfy the equation.
- **The Set Reset:** Notice how in Iteration 2, the set was empty again. This ensures that triplets found for `i=1` are independent of what happened when `i=0`.

#### Code

```Java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        Set<List<Integer>> hashSet=new HashSet<>();
        for(int i=0;i<nums.length-2;i++){
           Set<Integer> existingSet=new HashSet<>();
            for(int j=i+1;j<nums.length;j++){
                int remainingSum=-(nums[i]+nums[j]);
                if(existingSet.contains(remainingSum)){
                    List<Integer> temp = Arrays.asList(nums[i], nums[j], remainingSum);
                    Collections.sort(temp);
                    hashSet.add(temp);
                }
                existingSet.add(nums[j]);
            }
        }
        return new ArrayList<>(hashSet);
    }
}
```

### Optimized Approach using pointers and without using extra space : 

#### Short & Crisp Notes
**The Goal:** Find $a + b + c = 0$ using $O(1)$ extra space.
1. **Sort:** Arrange numbers (e.g., `[-4, -1, -1, 0, 1, 2]`).
2. **Anchor (`i`):** Fix the first number. If it’s the same as the last one, `continue` (Skip duplicates).
3. **Pointers (`j` & `k`):**
    - **Sum < 0:** Move `j` right (`j++`) to increase the sum.
    - **Sum > 0:** Move `k` left (`k--`) to decrease the sum.
    - **Sum == 0:** * Save triplet.
        - Move **both** `j++` and `k--`.
        - **Skip Duplicates:** Use `while` loops to skip any $j$ or $k$ values you just used.
---
####  Example Walkthrough
**Input:** `[-1, 0, 1, 2, -1, -4]` $\rightarrow$ **Sorted:** `[-4, -1, -1, 0, 1, 2]`
- **Iteration 1 ($i = -4$):**
    - $j = -1, k = 2$. Sum is $-3$.
    - Move $j$ right. Eventually, $j$ and $k$ meet. **No Triplet.**
    
- **Iteration 2 ($i = -1$):**
    - $j = -1, k = 2$. **Sum is $0$.** ✅ **Result: `[-1, -1, 2]`**
    - Move $j \rightarrow 0$ and $k \rightarrow 1$.
    - **Sum is $0$.** ✅ **Result: `[-1, 0, 1]`**
    - Move $j$ and $k$. They cross.
        
- **Iteration 3 ($i = -1$):**
    - `nums[2]` is $-1$, which is the same as `nums[1]`.
    - **Skip it!** This prevents finding `[-1, 0, 1]` all over again.

---

#### 💡 Why `while(j < k)` inside the loop?
The `j < k` condition is a safety boundary. It ensures that while you are skipping duplicates, your pointers don't accidentally run past each other and start pointing at the same elements or elements you've already processed.
#### Code:
```Java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> ans=new ArrayList<>();
        Arrays.sort(nums);
        for(int i=0;i<nums.length-2;i++){
            if(i>0 && nums[i]==nums[i-1])
                continue;
            int j=i+1;
            int k=nums.length-1;
            while(j<k){
                int sum=nums[i]+nums[j]+nums[k];
                if(sum<0){
                    j++;
                }else if(sum>0){
                    k--;
                }else{
                    List<Integer> tempAns=Arrays.asList(nums[i],nums[j],nums[k]);
                    ans.add(tempAns);
                    j++;
                    k--;
                    while(j<k && nums[j]==nums[j-1])
                        j++;
                    while(j<k & nums[k]==nums[k+1])
                        k--;
                }
            }
        }
        return ans;
    }
}
```