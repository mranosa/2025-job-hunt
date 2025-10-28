# Day 1, Session 3 Quiz: Dynamic Programming Introduction

**Duration**: 30 minutes
**Success Criteria**: Solve 2/3 problems and explain both memoization and tabulation

---

## Problem 1: Climbing Stairs 🟢

**Difficulty**: Easy
**Time Limit**: 8 minutes

You are climbing a staircase. It takes `n` steps to reach the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

**Example:**
```
Input: n = 3
Output: 3
Explanation: Three ways to climb to the top:
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```

**Constraints:**
- 1 <= n <= 45

**Your Solution:**
```typescript
function climbStairs(n: number): number {
    // Your code here
}
```

---

## Problem 2: House Robber 🟡

**Difficulty**: Medium
**Time Limit**: 12 minutes

You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. Adjacent houses have security systems connected, and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given an integer array `nums` representing the amount of money of each house, return the maximum amount of money you can rob tonight without alerting the police.

**Example:**
```
Input: nums = [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9), and rob house 5 (money = 1).
Total = 2 + 9 + 1 = 12.
```

**Constraints:**
- 1 <= nums.length <= 100
- 0 <= nums[i] <= 400

**Your Solution:**
```typescript
function rob(nums: number[]): number {
    // Your code here
}
```

---

## Problem 3: Coin Change 🟡

**Difficulty**: Medium
**Time Limit**: 10 minutes

You are given an integer array `coins` representing coins of different denominations and an integer `amount` representing a total amount of money.

Return the fewest number of coins that you need to make up that amount. If that amount cannot be made up by any combination of the coins, return -1.

You may assume that you have an infinite number of each kind of coin.

**Example:**
```
Input: coins = [1,2,5], amount = 11
Output: 3
Explanation: 11 = 5 + 5 + 1
```

**Constraints:**
- 1 <= coins.length <= 12
- 1 <= coins[i] <= 2^31 - 1
- 0 <= amount <= 10^4

**Your Solution:**
```typescript
function coinChange(coins: number[], amount: number): number {
    // Your code here
}
```

---

# Solutions

## Solution 1: Climbing Stairs

**Approach 1: Memoization (Top-Down DP)**
```typescript
function climbStairs(n: number): number {
    const memo = new Map<number, number>();

    function climb(steps: number): number {
        if (steps <= 2) return steps;
        if (memo.has(steps)) return memo.get(steps)!;

        const result = climb(steps - 1) + climb(steps - 2);
        memo.set(steps, result);
        return result;
    }

    return climb(n);
}
```

**Time Complexity**: O(n)
**Space Complexity**: O(n) - recursion stack + memoization

**Approach 2: Tabulation (Bottom-Up DP)**
```typescript
function climbStairs(n: number): number {
    if (n <= 2) return n;

    const dp: number[] = new Array(n + 1);
    dp[1] = 1;
    dp[2] = 2;

    for (let i = 3; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }

    return dp[n];
}
```

**Time Complexity**: O(n)
**Space Complexity**: O(n)

**Approach 3: Space Optimized**
```typescript
function climbStairs(n: number): number {
    if (n <= 2) return n;

    let prev2 = 1;  // dp[i-2]
    let prev1 = 2;  // dp[i-1]

    for (let i = 3; i <= n; i++) {
        const current = prev1 + prev2;
        prev2 = prev1;
        prev1 = current;
    }

    return prev1;
}
```

**Time Complexity**: O(n)
**Space Complexity**: O(1)

**Explanation:**
- Base case: 1 step = 1 way, 2 steps = 2 ways
- Recurrence: `dp[i] = dp[i-1] + dp[i-2]` (Fibonacci sequence!)
- At step i, you either came from step i-1 (1 step) or i-2 (2 steps)

---

## Solution 2: House Robber

**Approach 1: Memoization**
```typescript
function rob(nums: number[]): number {
    const memo = new Map<number, number>();

    function robFrom(index: number): number {
        if (index >= nums.length) return 0;
        if (memo.has(index)) return memo.get(index)!;

        // Rob current house + skip next, OR skip current house
        const result = Math.max(
            nums[index] + robFrom(index + 2),
            robFrom(index + 1)
        );

        memo.set(index, result);
        return result;
    }

    return robFrom(0);
}
```

**Approach 2: Tabulation (Better)**
```typescript
function rob(nums: number[]): number {
    if (nums.length === 1) return nums[0];

    const dp: number[] = new Array(nums.length);
    dp[0] = nums[0];
    dp[1] = Math.max(nums[0], nums[1]);

    for (let i = 2; i < nums.length; i++) {
        // Rob current + best from i-2, OR skip current (best from i-1)
        dp[i] = Math.max(nums[i] + dp[i - 2], dp[i - 1]);
    }

    return dp[nums.length - 1];
}
```

**Time Complexity**: O(n)
**Space Complexity**: O(n)

**Approach 3: Space Optimized**
```typescript
function rob(nums: number[]): number {
    if (nums.length === 1) return nums[0];

    let prev2 = nums[0];
    let prev1 = Math.max(nums[0], nums[1]);

    for (let i = 2; i < nums.length; i++) {
        const current = Math.max(nums[i] + prev2, prev1);
        prev2 = prev1;
        prev1 = current;
    }

    return prev1;
}
```

**Time Complexity**: O(n)
**Space Complexity**: O(1)

**Explanation:**
- State: `dp[i]` = maximum money can rob up to house i
- Recurrence: `dp[i] = max(nums[i] + dp[i-2], dp[i-1])`
- Either rob current house (can't rob i-1) or skip it (take i-1's best)

---

## Solution 3: Coin Change

**Approach: Tabulation (Bottom-Up DP)**
```typescript
function coinChange(coins: number[], amount: number): number {
    const dp: number[] = new Array(amount + 1).fill(Infinity);
    dp[0] = 0; // Base case: 0 coins needed for amount 0

    for (let i = 1; i <= amount; i++) {
        for (const coin of coins) {
            if (coin <= i) {
                dp[i] = Math.min(dp[i], dp[i - coin] + 1);
            }
        }
    }

    return dp[amount] === Infinity ? -1 : dp[amount];
}
```

**Time Complexity**: O(amount × coins.length)
**Space Complexity**: O(amount)

**Explanation:**
- State: `dp[i]` = minimum coins needed to make amount i
- Base case: `dp[0] = 0` (0 coins for amount 0)
- Recurrence: For each amount, try each coin and take minimum
- `dp[i] = min(dp[i], dp[i - coin] + 1)` for all coins <= i

**Example Walkthrough (coins=[1,2,5], amount=11):**
```
dp[0] = 0
dp[1] = 1 (coin 1)
dp[2] = 1 (coin 2)
dp[3] = 2 (dp[2] + coin 1 = 1 + 1)
dp[4] = 2 (dp[2] + coin 2 = 1 + 1)
dp[5] = 1 (coin 5)
dp[6] = 2 (dp[5] + coin 1 = 1 + 1)
...
dp[11] = 3 (dp[6] + coin 5 = 2 + 1)  or  (dp[10] + coin 1 = 2 + 1)
```

---

## Key DP Concepts Practiced

### 1. Overlapping Subproblems
All three problems have repeated calculations:
- Climbing Stairs: climb(5) calls climb(4) and climb(3), both call climb(2)
- House Robber: robbing houses [0..n] uses results from [0..n-1] and [0..n-2]
- Coin Change: amount 11 might try (6+5), (9+2), (10+1) - reusing smaller amounts

### 2. Optimal Substructure
Optimal solution contains optimal solutions to subproblems:
- Climbing Stairs: Best way to n = Best to (n-1) + Best to (n-2)
- House Robber: Best to rob n houses uses best from n-1 or n-2 houses
- Coin Change: Fewest coins for amount uses fewest for (amount - coin)

### 3. Memoization vs Tabulation

| Aspect | Memoization (Top-Down) | Tabulation (Bottom-Up) |
|--------|----------------------|----------------------|
| Approach | Recursive | Iterative |
| Start | Problem → Subproblems | Base case → Problem |
| Space | Recursion stack + cache | DP array only |
| When to use | Natural recursion | Space-sensitive |

---

## Self-Assessment

**Problem 1 (Climbing Stairs):**
- [ ] Solved independently
- [ ] Identified Fibonacci pattern
- [ ] Implemented both memoization and tabulation
- [ ] Optimized to O(1) space (bonus)

**Problem 2 (House Robber):**
- [ ] Solved independently
- [ ] Correct recurrence relation
- [ ] Handled edge cases (1 house, 2 houses)
- [ ] O(n) time, O(1) space solution (bonus)

**Problem 3 (Coin Change):**
- [ ] Solved independently
- [ ] Used DP (not greedy - greedy doesn't work!)
- [ ] Handled impossible cases (-1 return)
- [ ] Can explain why greedy fails

**Conceptual Understanding:**
- [ ] Can explain memoization vs tabulation
- [ ] Identified overlapping subproblems
- [ ] Wrote correct recurrence relations
- [ ] Understand when to use DP

**Overall:**
- [ ] Completed in 30 minutes
- [ ] Solved 2+ problems
- [ ] Can explain DP approach for each
- [ ] Ready for Day 2

---

## Common DP Mistakes to Avoid

1. **Using Greedy for Coin Change**: Greedy (take largest coin first) doesn't always work
   - Example: coins=[1,3,4], amount=6 → Greedy: 4+1+1=3 coins, Optimal: 3+3=2 coins

2. **Wrong Base Cases**: Always verify your base cases
   - Climbing Stairs: n=1 → 1 way, n=2 → 2 ways

3. **Off-by-One Errors**: Be careful with array indices
   - House Robber: dp[0] vs dp[1] initialization

4. **Not Considering All Subproblems**: Ensure you try all possibilities
   - Coin Change: Try every coin for each amount

---

**If you struggled:**
- Re-watch Errichto's DP video
- Focus on identifying state and recurrence
- Practice writing recurrence relations before coding
- Start with memoization (easier to think about)

**If you succeeded:**
- Excellent! You understand DP fundamentals
- Try space-optimized versions for all problems
- Read about more DP patterns (2D DP, state machines)
- Move to Day 2 with confidence

---

*Last updated: 2025-10-28*
