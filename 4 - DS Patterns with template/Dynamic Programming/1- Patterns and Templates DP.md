## ⚡ THE 12 CORE DP PATTERNS (FAANG + CP)

✅ **Pattern 1 — 1D DP (Linear DP)**

> Build answer from left → right.

**Template:**

```cpp
dp[i] = best using dp[i-1], dp[i-2], ...;
```

> **Common Problems:**
>> * Climbing Stairs
>> * House Robber
>> * Fibonacci
>> * Min cost climb stairs

---

✅ **Pattern 2 — 2D Grid DP (Bottom-Up Table)**

> DP on a matrix, usually moving right/down.

**Template:**
```cpp
for (i)
  for (j)
    dp[i][j] = min/max(dp[i-1][j], dp[i][j-1]) + cost;
```

> Problems:
>> * Unique Paths
>> * Min Path Sum
>> * Cherry Pickup
>> * Dungeon Game

---

✅ **Pattern 3 — Knapsack DP (0/1 Knapsack)**

> Choose or skip each item.

**Template:**
```cpp
for (i items)
  for (cap from W to 0)
    dp[cap] = max(dp[cap], dp[cap - wt[i]] + val[i]);
```

> **Problems:**
>> * 0/1 Knapsack
>> * Last Stone Weight II
>> * Target Sum

---

✅ **Pattern 4 — Unbounded Knapsack (Reuse allowed)**

> You can pick an item multiple times.

**Template:**
```cpp
for (cap)
  for (item)
    dp[cap] = max(dp[cap], dp[cap - wt[item]] + val[item]);
```
> **Problems:**
>> * Coin Change II
>> * Rod Cutting
>> * Perfect Squares

---

✅ **Pattern 5 — Subsequence DP (Strings / LCS / LIS)**

> Compare two pointers or build longest subsequence.

**Template:**
```cpp
for (i)
  for (j)
    if (s1[i-1] == s2[j-1])
        dp[i][j] = 1 + dp[i-1][j-1];
    else
        dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
```

> **Problems:**
>> * LCS
>> * Edit Distance
>> * Longest Palindromic Subsequence
>> * Minimum Insertions to Palindrome

---

✅ **Pattern 6 — Partition DP**

> Split array into segments and minimize/maximize result.

**Template:**

```cpp
for (len = 1..n)
  for (l = 0..n-len)
    for (k = l..r-1)
       dp[l][r] = best(dp[l][r], dp[l][k] + dp[k+1][r] + cost);
```

> **Problems:**
>> * Burst Balloons
>> * Matrix Chain Multiplication
>> * Palindrome Partitioning

---

✅ **Pattern 7 — Interval DP**

> Similar to partition DP but focused on ranges.

Same template as above.

> **Problems:**
>> * Guess Number Higher/Lower II
>> * Minimum Score Triangulation
>> * Stone Game VII

----

✅ **Pattern 8 — Digit DP**

> DP with digits, constraints, numbers.

**Template:**
```cpp
dp[pos][tight][sum][state] = ways;
```

Used when digit-by-digit scanning number.

> **Problems:**
>> * Count numbers with certain property
>> * Numbers without repeating digits
>> * Hard LC digit problems

---

✅ **Pattern 9 — Bitmask DP**

> State = subset. Used when N ≤ 20.

**Template:**
```cpp
for (mask)
  for (bit in mask)
    dp[mask] = best(dp[mask ^ bit] + cost(bit, mask));
```

> **Problems:**
>> * Can I Win
>> * Traveling Salesman Problem
>> * Stickers to Spell Word

----

✅ **Pattern 10 — DP on Trees (Tree DP)**

> DFS + return info up.

**Template:**
```cpp
int dfs(u, parent) {
    for all children v:
        compute dp[v]
    combine children results
    return dp[u];
}
```

> **Problems:**
>> * Diameter of Tree
>> * Count Good Nodes
>> * Max Independent Set in Tree

---

✅ **Pattern 11 — Game Theory DP (Minimax + DP)**

> Two players taking turns.

**Template:**
```cpp
int solve(l, r):
    return max(
        nums[l] - solve(l+1, r),
        nums[r] - solve(l, r-1)
    );
```

> **Problems:**
>> * Predict the Winner
>> * Stone Games
>> * Flip Game II
>> * Can I Win

----

✅ **Pattern 12 — Memoized Recursion (Top-Down DP)**

> The universal pattern for when you can’t see bottom-up immediately.

**Template:**
```cpp
int solve(state):
    if (dp[state] exists) return dp[state]
    compute answer from subproblems
    return dp[state] = answer;
```

> Problems:
>> Almost ALL hard DP problems start with this.

----

<span style="color:yellow">**DP MASTER TEMPLATE (universal)**</span>

> Whenever you see a DP problem, follow these 4 steps:

```cpp
// 1. define dp state
dp[...] = ?

// 2. identify transitions
dp[cur] = best of { dp[substates] + cost }

// 3. set base cases
dp[base] = something

// 4. compute in order (memo or table)
```

This works for EVERYTHING.
