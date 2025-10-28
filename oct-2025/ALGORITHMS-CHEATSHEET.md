# Algorithms & Data Structures Cheat Sheet

Quick reference guide for common algorithm patterns and data structures for technical interviews.

---

## Table of Contents
1. [Time & Space Complexity](#time--space-complexity)
2. [Array & String Patterns](#array--string-patterns)
3. [Hash Map Patterns](#hash-map-patterns)
4. [Two Pointers](#two-pointers)
5. [Sliding Window](#sliding-window)
6. [Binary Search](#binary-search)
7. [Tree Algorithms](#tree-algorithms)
8. [Graph Algorithms](#graph-algorithms)
9. [Dynamic Programming](#dynamic-programming)
10. [Common Tricks & Tips](#common-tricks--tips)

---

## Time & Space Complexity

### Big O Notation (Best to Worst)
```
O(1)        - Constant
O(log n)    - Logarithmic (binary search)
O(n)        - Linear
O(n log n)  - Linearithmic (merge sort, heap sort)
O(n²)       - Quadratic (nested loops)
O(2ⁿ)       - Exponential (recursive Fibonacci)
O(n!)       - Factorial (permutations)
```

### Common Operations
| Data Structure | Access | Search | Insert | Delete |
|---------------|--------|--------|--------|--------|
| Array         | O(1)   | O(n)   | O(n)   | O(n)   |
| Hash Map      | O(1)   | O(1)   | O(1)   | O(1)   |
| Binary Search Tree | O(log n) | O(log n) | O(log n) | O(log n) |
| Heap          | O(log n) | O(n)  | O(log n) | O(log n) |
| Stack/Queue   | O(n)   | O(n)   | O(1)   | O(1)   |

---

## Array & String Patterns

### 1. Prefix Sum
Calculate cumulative sums for range query optimization.

```python
def prefix_sum(arr):
    prefix = [0]
    for num in arr:
        prefix.append(prefix[-1] + num)
    return prefix

# Range sum from i to j: prefix[j+1] - prefix[i]
```

**Use Cases:** Range sum queries, subarray sum problems

---

### 2. Kadane's Algorithm
Maximum subarray sum in O(n).

```python
def max_subarray(nums):
    max_sum = current_sum = nums[0]
    for num in nums[1:]:
        current_sum = max(num, current_sum + num)
        max_sum = max(max_sum, current_sum)
    return max_sum
```

**Use Cases:** Maximum subarray, stock profit problems

---

### 3. Dutch National Flag
Sort array with 3 distinct values in one pass.

```python
def sort_colors(nums):
    low, mid, high = 0, 0, len(nums) - 1
    while mid <= high:
        if nums[mid] == 0:
            nums[low], nums[mid] = nums[mid], nums[low]
            low += 1
            mid += 1
        elif nums[mid] == 1:
            mid += 1
        else:
            nums[mid], nums[high] = nums[high], nums[mid]
            high -= 1
```

**Use Cases:** Sort array with limited distinct values

---

## Hash Map Patterns

### 1. Frequency Counter
Track occurrences of elements.

```typescript
function frequencyMap(arr: number[]): Map<number, number> {
    const freq = new Map<number, number>();
    for (const num of arr) {
        freq.set(num, (freq.get(num) || 0) + 1);
    }
    return freq;
}
```

**Use Cases:** Anagram, duplicate detection, frequency analysis

---

### 2. Two Sum Pattern
Find pairs with specific sum.

```typescript
function twoSum(nums: number[], target: number): number[] {
    const seen = new Map<number, number>();
    for (let i = 0; i < nums.length; i++) {
        const complement = target - nums[i];
        if (seen.has(complement)) {
            return [seen.get(complement)!, i];
        }
        seen.set(nums[i], i);
    }
    return [];
}
```

**Use Cases:** Two sum, three sum, four sum problems

---

## Two Pointers

### 1. Opposite Ends
Start from both ends, move inward.

```python
def is_palindrome(s: str) -> bool:
    left, right = 0, len(s) - 1
    while left < right:
        if s[left] != s[right]:
            return False
        left += 1
        right -= 1
    return True
```

**Use Cases:** Palindrome, reverse string, pair sum in sorted array

---

### 2. Fast & Slow Pointers
Detect cycles or find middle element.

```python
def has_cycle(head):
    slow = fast = head
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        if slow == fast:
            return True
    return False
```

**Use Cases:** Linked list cycle, find middle, remove nth from end

---

### 3. Same Direction
Both pointers move forward at different speeds.

```python
def remove_duplicates(nums):
    if not nums:
        return 0
    slow = 0
    for fast in range(1, len(nums)):
        if nums[fast] != nums[slow]:
            slow += 1
            nums[slow] = nums[fast]
    return slow + 1
```

**Use Cases:** Remove duplicates, partition array

---

## Sliding Window

### 1. Fixed Size Window
Window of constant size k.

```typescript
function maxSumSubarray(nums: number[], k: number): number {
    let windowSum = 0;
    let maxSum = 0;

    // Initial window
    for (let i = 0; i < k; i++) {
        windowSum += nums[i];
    }
    maxSum = windowSum;

    // Slide window
    for (let i = k; i < nums.length; i++) {
        windowSum = windowSum - nums[i - k] + nums[i];
        maxSum = Math.max(maxSum, windowSum);
    }
    return maxSum;
}
```

**Use Cases:** Average of k elements, max sum of k elements

---

### 2. Variable Size Window
Window size changes based on condition.

```typescript
function longestSubstringKDistinct(s: string, k: number): number {
    const charCount = new Map<string, number>();
    let left = 0;
    let maxLength = 0;

    for (let right = 0; right < s.length; right++) {
        charCount.set(s[right], (charCount.get(s[right]) || 0) + 1);

        while (charCount.size > k) {
            charCount.set(s[left], charCount.get(s[left])! - 1);
            if (charCount.get(s[left]) === 0) {
                charCount.delete(s[left]);
            }
            left++;
        }
        maxLength = Math.max(maxLength, right - left + 1);
    }
    return maxLength;
}
```

**Use Cases:** Longest substring, minimum window, subarray sum

---

## Binary Search

### 1. Basic Binary Search
Find exact value in sorted array.

```python
def binary_search(nums, target):
    left, right = 0, len(nums) - 1
    while left <= right:
        mid = left + (right - left) // 2
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```

**Time:** O(log n)

---

### 2. Find First/Last Occurrence
Modified binary search for duplicates.

```python
def find_first(nums, target):
    left, right = 0, len(nums) - 1
    result = -1
    while left <= right:
        mid = left + (right - left) // 2
        if nums[mid] == target:
            result = mid
            right = mid - 1  # Keep searching left
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return result
```

**Use Cases:** Find boundaries, range search

---

### 3. Search in Rotated Array
Binary search variant for rotated sorted array.

```python
def search_rotated(nums, target):
    left, right = 0, len(nums) - 1
    while left <= right:
        mid = left + (right - left) // 2
        if nums[mid] == target:
            return mid

        # Left half is sorted
        if nums[left] <= nums[mid]:
            if nums[left] <= target < nums[mid]:
                right = mid - 1
            else:
                left = mid + 1
        # Right half is sorted
        else:
            if nums[mid] < target <= nums[right]:
                left = mid + 1
            else:
                right = mid - 1
    return -1
```

---

## Tree Algorithms

### 1. DFS Traversals

```python
# Inorder (Left, Root, Right) - gives sorted order for BST
def inorder(root):
    if not root:
        return []
    return inorder(root.left) + [root.val] + inorder(root.right)

# Preorder (Root, Left, Right) - copy tree structure
def preorder(root):
    if not root:
        return []
    return [root.val] + preorder(root.left) + preorder(root.right)

# Postorder (Left, Right, Root) - delete tree
def postorder(root):
    if not root:
        return []
    return postorder(root.left) + postorder(root.right) + [root.val]
```

**Iterative with Stack:**
```python
def inorder_iterative(root):
    result, stack = [], []
    current = root
    while current or stack:
        while current:
            stack.append(current)
            current = current.left
        current = stack.pop()
        result.append(current.val)
        current = current.right
    return result
```

---

### 2. BFS (Level Order Traversal)

```python
from collections import deque

def level_order(root):
    if not root:
        return []

    result = []
    queue = deque([root])

    while queue:
        level_size = len(queue)
        level = []

        for _ in range(level_size):
            node = queue.popleft()
            level.append(node.val)

            if node.left:
                queue.append(node.left)
            if node.right:
                queue.append(node.right)

        result.append(level)
    return result
```

**Use Cases:** Level order, right side view, zigzag traversal

---

### 3. Tree Height/Depth

```python
def max_depth(root):
    if not root:
        return 0
    return 1 + max(max_depth(root.left), max_depth(root.right))

def is_balanced(root):
    def dfs(node):
        if not node:
            return 0
        left = dfs(node.left)
        right = dfs(node.right)
        if left == -1 or right == -1 or abs(left - right) > 1:
            return -1
        return 1 + max(left, right)

    return dfs(root) != -1
```

---

### 4. Lowest Common Ancestor (LCA)

```python
def lowest_common_ancestor(root, p, q):
    if not root or root == p or root == q:
        return root

    left = lowest_common_ancestor(root.left, p, q)
    right = lowest_common_ancestor(root.right, p, q)

    if left and right:
        return root
    return left if left else right
```

---

## Graph Algorithms

### 1. DFS (Depth-First Search)

```python
def dfs(graph, start, visited=None):
    if visited is None:
        visited = set()

    visited.add(start)
    print(start)

    for neighbor in graph[start]:
        if neighbor not in visited:
            dfs(graph, neighbor, visited)

    return visited
```

**Iterative with Stack:**
```python
def dfs_iterative(graph, start):
    visited = set()
    stack = [start]

    while stack:
        node = stack.pop()
        if node not in visited:
            visited.add(node)
            print(node)
            for neighbor in graph[node]:
                if neighbor not in visited:
                    stack.append(neighbor)
    return visited
```

---

### 2. BFS (Breadth-First Search)

```python
from collections import deque

def bfs(graph, start):
    visited = set([start])
    queue = deque([start])

    while queue:
        node = queue.popleft()
        print(node)

        for neighbor in graph[node]:
            if neighbor not in visited:
                visited.add(neighbor)
                queue.append(neighbor)
    return visited
```

**Use Cases:** Shortest path (unweighted), level traversal

---

### 3. Detect Cycle (Undirected Graph)

```python
def has_cycle(graph):
    visited = set()

    def dfs(node, parent):
        visited.add(node)
        for neighbor in graph[node]:
            if neighbor not in visited:
                if dfs(neighbor, node):
                    return True
            elif neighbor != parent:
                return True
        return False

    for node in graph:
        if node not in visited:
            if dfs(node, None):
                return True
    return False
```

---

### 4. Topological Sort (DAG)

```python
def topological_sort(graph):
    visited = set()
    stack = []

    def dfs(node):
        visited.add(node)
        for neighbor in graph[node]:
            if neighbor not in visited:
                dfs(neighbor)
        stack.append(node)

    for node in graph:
        if node not in visited:
            dfs(node)

    return stack[::-1]  # Reverse to get correct order
```

**Use Cases:** Build order, course schedule

---

### 5. Union-Find (Disjoint Set)

```python
class UnionFind:
    def __init__(self, n):
        self.parent = list(range(n))
        self.rank = [0] * n

    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])  # Path compression
        return self.parent[x]

    def union(self, x, y):
        px, py = self.find(x), self.find(y)
        if px == py:
            return False

        # Union by rank
        if self.rank[px] < self.rank[py]:
            self.parent[px] = py
        elif self.rank[px] > self.rank[py]:
            self.parent[py] = px
        else:
            self.parent[py] = px
            self.rank[px] += 1
        return True
```

**Use Cases:** Detect cycle, connected components, network connectivity

---

## Dynamic Programming

### 1. Fibonacci (Memoization)

```python
def fib_memo(n, memo=None):
    if memo is None:
        memo = {}
    if n in memo:
        return memo[n]
    if n <= 1:
        return n

    memo[n] = fib_memo(n-1, memo) + fib_memo(n-2, memo)
    return memo[n]
```

### 2. Fibonacci (Tabulation)

```python
def fib_tab(n):
    if n <= 1:
        return n

    dp = [0] * (n + 1)
    dp[1] = 1

    for i in range(2, n + 1):
        dp[i] = dp[i-1] + dp[i-2]

    return dp[n]
```

---

### 3. Coin Change

```python
def coin_change(coins, amount):
    dp = [float('inf')] * (amount + 1)
    dp[0] = 0

    for i in range(1, amount + 1):
        for coin in coins:
            if coin <= i:
                dp[i] = min(dp[i], dp[i - coin] + 1)

    return dp[amount] if dp[amount] != float('inf') else -1
```

---

### 4. Knapsack (0/1)

```python
def knapsack(weights, values, capacity):
    n = len(weights)
    dp = [[0] * (capacity + 1) for _ in range(n + 1)]

    for i in range(1, n + 1):
        for w in range(capacity + 1):
            if weights[i-1] <= w:
                dp[i][w] = max(
                    values[i-1] + dp[i-1][w - weights[i-1]],
                    dp[i-1][w]
                )
            else:
                dp[i][w] = dp[i-1][w]

    return dp[n][capacity]
```

---

### 5. Longest Common Subsequence

```python
def lcs(text1, text2):
    m, n = len(text1), len(text2)
    dp = [[0] * (n + 1) for _ in range(m + 1)]

    for i in range(1, m + 1):
        for j in range(1, n + 1):
            if text1[i-1] == text2[j-1]:
                dp[i][j] = dp[i-1][j-1] + 1
            else:
                dp[i][j] = max(dp[i-1][j], dp[i][j-1])

    return dp[m][n]
```

---

### 6. Longest Increasing Subsequence

```python
def longest_increasing_subsequence(nums):
    if not nums:
        return 0

    dp = [1] * len(nums)

    for i in range(1, len(nums)):
        for j in range(i):
            if nums[j] < nums[i]:
                dp[i] = max(dp[i], dp[j] + 1)

    return max(dp)
```

**Optimized O(n log n):**
```python
from bisect import bisect_left

def lis_optimized(nums):
    sub = []
    for num in nums:
        pos = bisect_left(sub, num)
        if pos == len(sub):
            sub.append(num)
        else:
            sub[pos] = num
    return len(sub)
```

---

## Common Tricks & Tips

### 1. XOR Tricks
```python
# Find single number in array where every other appears twice
def single_number(nums):
    result = 0
    for num in nums:
        result ^= num
    return result

# Swap without temp variable
a ^= b
b ^= a
a ^= b
```

---

### 2. Bit Manipulation
```python
# Check if power of 2
def is_power_of_two(n):
    return n > 0 and (n & (n - 1)) == 0

# Count set bits
def count_bits(n):
    count = 0
    while n:
        count += 1
        n &= (n - 1)  # Remove rightmost set bit
    return count
```

---

### 3. String Palindrome Check
```python
# Ignore non-alphanumeric
def is_palindrome(s):
    cleaned = ''.join(c.lower() for c in s if c.isalnum())
    return cleaned == cleaned[::-1]
```

---

### 4. Reverse Integer
```python
def reverse_integer(x):
    sign = -1 if x < 0 else 1
    x = abs(x)
    result = 0

    while x:
        result = result * 10 + x % 10
        x //= 10

    return sign * result
```

---

### 5. Fast Power (Exponentiation)
```python
def pow(x, n):
    if n == 0:
        return 1
    if n < 0:
        x = 1 / x
        n = -n

    result = 1
    while n:
        if n % 2:
            result *= x
        x *= x
        n //= 2
    return result
```

---

## Problem-Solving Framework

1. **Understand the Problem**
   - Read carefully, identify inputs/outputs
   - Ask clarifying questions
   - Consider edge cases

2. **Plan Your Approach**
   - Brute force first (establish baseline)
   - Identify patterns (two pointers, sliding window, etc.)
   - Consider data structures (hash map, heap, stack)

3. **Implement**
   - Write clean, readable code
   - Use meaningful variable names
   - Handle edge cases

4. **Test**
   - Test with examples from problem
   - Test edge cases (empty, single element, duplicates)
   - Dry run with small input

5. **Optimize**
   - Analyze time/space complexity
   - Look for redundant operations
   - Consider trade-offs

6. **Communicate**
   - Think out loud during interviews
   - Explain your approach before coding
   - Walk through your solution after

---

## Interview Tips

- **Start Simple**: Explain brute force before optimizing
- **Use Examples**: Walk through with concrete examples
- **Test Your Code**: Don't assume it works, verify
- **Handle Edge Cases**: Empty input, single element, duplicates, negatives
- **Complexity Analysis**: Always state time and space complexity
- **Ask Questions**: Clarify ambiguity before diving in

---

**Quick Pattern Recognition:**
- Sorted array → Binary search, two pointers
- Find pairs/triplets → Hash map, two pointers
- Substring/subarray → Sliding window
- Tree problems → DFS/BFS
- Graph connectivity → Union-find, DFS
- Optimization (min/max) → DP, greedy
- Top K elements → Heap
- Path finding → BFS (shortest), DFS (all paths)

---

*Last updated: 2025-10-28*
