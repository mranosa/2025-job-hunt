# Day 1, Session 1 Quiz: Arrays, Strings, Hash Maps

**Duration**: 30 minutes
**Success Criteria**: Solve 3/4 problems

---

## Problem 1: Two Sum 🟢

**Difficulty**: Easy
**Time Limit**: 7 minutes

Given an array of integers `nums` and an integer `target`, return indices of the two numbers that add up to `target`.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

**Example:**
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: nums[0] + nums[1] = 2 + 7 = 9
```

**Constraints:**
- 2 <= nums.length <= 10^4
- -10^9 <= nums[i] <= 10^9
- Only one valid answer exists

**Your Solution:**
```typescript
function twoSum(nums: number[], target: number): number[] {
    // Your code here
}
```

---

## Problem 2: Longest Substring Without Repeating Characters 🟡

**Difficulty**: Medium
**Time Limit**: 10 minutes

Given a string `s`, find the length of the longest substring without repeating characters.

**Example:**
```
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.
```

**Constraints:**
- 0 <= s.length <= 5 * 10^4
- s consists of English letters, digits, symbols and spaces

**Your Solution:**
```typescript
function lengthOfLongestSubstring(s: string): number {
    // Your code here
}
```

---

## Problem 3: Valid Anagram 🟢

**Difficulty**: Easy
**Time Limit**: 6 minutes

Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

**Example:**
```
Input: s = "anagram", t = "nagaram"
Output: true
```

**Constraints:**
- 1 <= s.length, t.length <= 5 * 10^4
- s and t consist of lowercase English letters

**Your Solution:**
```typescript
function isAnagram(s: string, t: string): boolean {
    // Your code here
}
```

---

## Problem 4: Valid Palindrome 🟢

**Difficulty**: Easy
**Time Limit**: 7 minutes

A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward.

Given a string `s`, return `true` if it is a palindrome, or `false` otherwise.

**Example:**
```
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.
```

**Your Solution:**
```typescript
function isPalindrome(s: string): boolean {
    // Your code here
}
```

---

# Solutions

## Solution 1: Two Sum

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

    return []; // Should never reach here based on constraints
}
```

**Time Complexity**: O(n)
**Space Complexity**: O(n)

**Explanation:**
- Use hash map to store seen numbers and their indices
- For each number, check if complement (target - num) exists in map
- If found, return both indices
- Otherwise, add current number to map

---

## Solution 2: Longest Substring Without Repeating Characters

```typescript
function lengthOfLongestSubstring(s: string): number {
    const charSet = new Set<string>();
    let left = 0;
    let maxLength = 0;

    for (let right = 0; right < s.length; right++) {
        // Shrink window until no duplicates
        while (charSet.has(s[right])) {
            charSet.delete(s[left]);
            left++;
        }

        charSet.add(s[right]);
        maxLength = Math.max(maxLength, right - left + 1);
    }

    return maxLength;
}
```

**Time Complexity**: O(n)
**Space Complexity**: O(min(n, m)) where m is charset size

**Explanation:**
- Sliding window with two pointers (left, right)
- Use Set to track characters in current window
- If duplicate found, shrink window from left
- Track maximum window size seen

---

## Solution 3: Valid Anagram

**Approach 1: Sorting**
```typescript
function isAnagram(s: string, t: string): boolean {
    if (s.length !== t.length) return false;

    const sortedS = s.split('').sort().join('');
    const sortedT = t.split('').sort().join('');

    return sortedS === sortedT;
}
```

**Time Complexity**: O(n log n)
**Space Complexity**: O(n)

**Approach 2: Hash Map (Better)**
```typescript
function isAnagram(s: string, t: string): boolean {
    if (s.length !== t.length) return false;

    const charCount = new Map<string, number>();

    // Count characters in s
    for (const char of s) {
        charCount.set(char, (charCount.get(char) || 0) + 1);
    }

    // Decrement counts with characters from t
    for (const char of t) {
        if (!charCount.has(char)) return false;
        charCount.set(char, charCount.get(char)! - 1);
        if (charCount.get(char)! < 0) return false;
    }

    return true;
}
```

**Time Complexity**: O(n)
**Space Complexity**: O(1) - at most 26 lowercase letters

---

## Solution 4: Valid Palindrome

```typescript
function isPalindrome(s: string): boolean {
    // Clean string: lowercase and alphanumeric only
    const cleaned = s.toLowerCase().replace(/[^a-z0-9]/g, '');

    let left = 0;
    let right = cleaned.length - 1;

    while (left < right) {
        if (cleaned[left] !== cleaned[right]) {
            return false;
        }
        left++;
        right--;
    }

    return true;
}
```

**Time Complexity**: O(n)
**Space Complexity**: O(n) - for cleaned string

**Optimized (O(1) space):**
```typescript
function isPalindrome(s: string): boolean {
    let left = 0;
    let right = s.length - 1;

    while (left < right) {
        // Skip non-alphanumeric from left
        while (left < right && !isAlphanumeric(s[left])) {
            left++;
        }

        // Skip non-alphanumeric from right
        while (left < right && !isAlphanumeric(s[right])) {
            right--;
        }

        if (s[left].toLowerCase() !== s[right].toLowerCase()) {
            return false;
        }

        left++;
        right--;
    }

    return true;
}

function isAlphanumeric(char: string): boolean {
    return /[a-zA-Z0-9]/.test(char);
}
```

**Time Complexity**: O(n)
**Space Complexity**: O(1)

---

## Self-Assessment

**Problem 1 (Two Sum):**
- [ ] Solved independently
- [ ] Identified hash map pattern
- [ ] O(n) time complexity
- [ ] Handled edge cases

**Problem 2 (Longest Substring):**
- [ ] Solved independently
- [ ] Used sliding window correctly
- [ ] Understood when to shrink window
- [ ] O(n) time complexity

**Problem 3 (Valid Anagram):**
- [ ] Solved independently
- [ ] Used hash map approach (not sorting)
- [ ] Handled frequency counting correctly
- [ ] O(n) time complexity

**Problem 4 (Valid Palindrome):**
- [ ] Solved independently
- [ ] Used two pointers
- [ ] Handled non-alphanumeric filtering
- [ ] O(1) space (bonus) or O(n) space

**Overall:**
- [ ] Completed in 30 minutes
- [ ] Solved 3+ problems
- [ ] Can explain time/space complexity
- [ ] Ready to move to next session

---

**If you struggled:**
- Review hash map pattern (Problems 1, 3)
- Practice sliding window (Problem 2)
- Watch NeetCode's explanation videos
- Redo these problems tomorrow

**If you succeeded:**
- Great! Move to Session 2
- Note any insights in your study log
- Remember these patterns for interviews

---

*Last updated: 2025-10-28*
