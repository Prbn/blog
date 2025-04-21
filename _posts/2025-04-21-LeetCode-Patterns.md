
# 15 Essential LeetCode Patterns That Make Interviews Easier

**success isn’t about solving the most problems—it’s about recognizing the right patterns.** Patterns help you break down unfamiliar problems efficiently, reduce time complexity, and ace interviews at top companies like **Google and Amazon**.

Here are **15 must-know patterns**, complete with explanations, examples, and recommended problems to practice.

---

### 1. **Prefix Sum**
**When to Use**: When dealing with multiple subarray sum queries.

**Idea**: Precompute a running sum (`prefixSum[i] = sum(nums[0] to nums[i])`). Then,
```text
Sum[i...j] = prefixSum[j] - prefixSum[i-1]
```

```python
def create_prefix_sum(arr):
  for i in range(1, len(arr)):
    arr[i] += arr[i-1]
  return arr
```


**Why it Helps**: Reduces time complexity of each query from O(n) to O(1).

**Practice**: Range Sum Query, Subarray Sum Equals K

Below are some of the leet code problem to practice:
#### 1. [303. Range Sum Query - Immutable](https://leetcode.com/problems/range-sum-query-immutable/description/) *(Easy)*
#### 2. [525. Contiguous Array](https://leetcode.com/problems/contiguous-array/description/) *(Medium)*
#### 3. [560. Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/description/) *(Hard)*

---

### 2. **Two Pointers**
**When to Use**: When comparing elements from both ends or traversing pairs.

**Example**: Check if a string is a palindrome by moving two pointers toward the center.

**Why it Helps**: Converts O(n²) brute-force solutions into efficient O(n) approaches.

**Practice**: Two Sum II, 3Sum, Valid Palindrome

---

### 3. **Sliding Window**
**When to Use**: For problems involving subarrays or substrings with a fixed or dynamic size.

**Example**: Max sum of subarray of size `k`. Slide the window across the array, updating the sum efficiently.

**Why it Helps**: Reduces redundant calculations; time complexity becomes O(n).

**Practice**: Maximum Sum Subarray of Size K, Longest Substring Without Repeating Characters

---

### 4. **Fast and Slow Pointers**
**When to Use**: Detecting cycles, finding middle of a linked list.

**Example**: Floyd’s cycle detection – fast pointer moves two steps, slow moves one. If they meet, there's a cycle.

**Practice**: Linked List Cycle, Find Middle of Linked List

---

### 5. **In-place Linked List Reversal**
**When to Use**: Reversing nodes, modifying link directions.

**Technique**: Use three pointers: `prev`, `curr`, `next`. Update links while traversing.

**Practice**: Reverse Linked List, Reverse Nodes in k-Group

---

### 6. **Monotonic Stack**
**When to Use**: Next greater/smaller element problems.

**Technique**: Maintain a stack of indices or elements in monotonic order while traversing.

**Practice**: Daily Temperatures, Next Greater Element, Largest Rectangle in Histogram

---

### 7. **Top K Elements (Heap)**
**When to Use**: When you need top `k` frequent/largest/smallest elements.

**Technique**: Use a **min-heap** for top largest and **max-heap** for top smallest.

**Bonus**: Learn QuickSelect for an even faster average-case solution.

**Practice**: Top K Frequent Elements, Kth Largest Element in an Array

---

### 8. **Overlapping Intervals**
**When to Use**: Merge, insert, or find overlaps in intervals.

**Technique**: Sort intervals by start time. Then merge or compare with the last interval in the merged list.

**Practice**: Merge Intervals, Meeting Rooms, Insert Interval

---

### 9. **Modified Binary Search**
**When to Use**: When arrays are rotated, contain duplicates, or aren't perfectly sorted.

**Examples**:
- Rotated sorted array: Determine which side is sorted and binary search accordingly.
- Find first/last occurrence of an element.

**Practice**: Search in Rotated Sorted Array, First Bad Version

---

### 10. **Binary Tree Traversals**
**When to Use**: Any tree problem.

**Traversals**:
- **In-order**: For BSTs (sorted values)
- **Pre-order**: Serialization, cloning
- **Post-order**: Deletion
- **Level-order**: Layer-wise problems (BFS on trees)

**Practice**: Binary Tree Inorder Traversal, Level Order Traversal

---

### 11. **Depth-First Search (DFS)**
**When to Use**: Explore paths, find components, or backtrack in graphs/trees.

**Technique**: Recursion or stack-based traversal.

**Practice**: Number of Islands, Clone Graph, Path Sum

---

### 12. **Breadth-First Search (BFS)**
**When to Use**: Find the shortest path in unweighted graphs or traverse level by level.

**Technique**: Use a queue; track visited nodes to prevent cycles.

**Practice**: Word Ladder, Binary Tree Right Side View

---

### 13. **Matrix Traversal**
**When to Use**: When dealing with 2D grids.

**Approach**: Treat each cell as a node in a graph. Use BFS/DFS for problems like island counting, maze solving.

**Practice**: Number of Islands, Rotten Oranges, Word Search

---

### 14. **Backtracking**
**When to Use**: Generate all combinations, permutations, or valid sequences.

**Technique**: Recursively explore all paths, undo choices when needed.

**Practice**: Subsets, Permutations, N-Queens, Sudoku Solver

---

### 15. **Dynamic Programming (DP)**
**When to Use**: When a problem has **overlapping subproblems** and **optimal substructure**.

**Common Patterns**:
- Fibonacci
- Knapsack
- Longest Common Subsequence
- Subset Sum

**Approach**: Use memoization (top-down) or tabulation (bottom-up) to cache results.

**Practice**: House Robber, Coin Change, Longest Increasing Subsequence

---

## Final Thoughts

Mastering these patterns is like learning the grammar of problem-solving. With these tools, you can approach almost any coding interview question with confidence and efficiency.

🔗 Check out **AlgoMastery** or the [blog](https://blog.algomaster) for deeper dives and practice problems on each pattern.

📌 **Pro Tip**: Don’t just memorize solutions—**learn to recognize the pattern behind the problem**. That’s what makes 1,500+ problems feel manageable.

---

Would you like me to turn this into a downloadable PDF or add example code for each pattern?
