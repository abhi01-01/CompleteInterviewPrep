# THE MASTER IDEA OF INTERVAL DP

> Interval DP shows up in:
>> Guess Number (Minimax)
>> 
>> Stone Games
>> 
>> Palindrome DP
>> 
>> Matrix Chain Multiplication
>> 
>> Burst Balloons
>> 
>> Merging stones
>> 
>> DP on brackets
>> 
>> Optimal partitions

They all follow ONE MASTER PATTERN. This one pattern solves EVERY interval DP problem.

* You are trying to compute something for a range `[l, r]`.
* The answer for `[l, r]` depends on smaller subintervals inside it.

Meaning:

* Solve smaller intervals first

* Build to larger ones

* Use `dp[l][r]` as the key state

```cpp
for (int len = 2; len <= n; len++) {
    for (int l = 0; l + len - 1 < n; l++) {
        int r = l + len - 1;

        dp[l][r] = INF or -INF;

        for (int k = l; k < r; k++) {
            dp[l][r] = min/max(
                dp[l][r],
                dp[l][k] + dp[k+1][r] + cost(l, k, r)
            );
        }
    }
}
```

* ✔️ len grows
* ✔️ l moves
* ✔️ r = l + len - 1
* ✔️ break interval at every k


<span style="color:yellow">**WHY THIS WORKS?**</span>

Because for any interval `[l, r]`:
* It splits at some pivot `k`
* Both left `[l, k]` and right `[k+1, r]` are smaller intervals
* And the order of solving ensures they are pre-computed.

This loop pattern ensures:
* length 1 intervals → trivial
* length 2 intervals → easy
* …
* length n intervals → final answer

----


### <span style="color:yellow">Let's break out all variants used in real problems.(6 OF THEM)</span>

✅ **Pattern 1 — Classic Split DP (`k` between `l..r`)**

Used in:
* Matrix Chain Multiplication
* Burst Balloons
* Minimum Cost to Merge Stones
* Evaluate Expression
* Partition problems

**Template:**
```cpp
for k in [l..r]:
    dp[l][r] = min(dp[l][k] + dp[k+1][r] + cost)
```

> Problems:
>> * LC 312: Burst Balloons
>> * LC 1000: Minimum Cost to Merge Stones
>> * Matrix chain multiplication
>> * Stone Game V

✅ **Pattern 2 — Minimax Interval DP (Game Theory inside interval)**

Used when two players choose from sides:
* Predict the Winner
* Stone Game series
* Guess Number Higher/Lower II

**Template:**
```cpp
dp[l][r] = max(
   nums[l] - dp[l+1][r],
   nums[r] - dp[l][r-1]
)
```

or
```cpp
dp[l][r] = min(
   x + max(dp[l][x-1], dp[x+1][r])
)
```

> Problems:
>> * LC 486: Predict the Winner
>> * LC 877: Stone Game
>> * LC 375: Guess Number Higher/Lower II
>> * LC 1690: Stone Game VII

✅ **Pattern 3 — Palindrome Interval DP**

Special interval DP where cost depends on endpoints.

**Recurrence:**
```cpp
if s[l] == s[r]:
    dp[l][r] = dp[l+1][r-1]
else:
    dp[l][r] = 1 + min(dp[l+1][r], dp[l][r-1])
```

> Problems:
>> * LC 1312: Min Insertions to Palindrome
>> * LC 516: Longest Palindromic Subsequence
>> * LC 730: Count Palindromic Subsequences

✅ **Pattern 4 — Merge Cost DP (like merging files)**

Cost = sum of interval.

**Recurrence:**
```cpp
dp[l][r] = min over k ( dp[l][k] + dp[k+1][r] ) + sum(l,r)
```

> Problems:
>> * Merge Stones
>> * Minimum Cost to Merge Files
>> * Burst Balloons (modified)

✅ **Pattern 5 — Interval DP with Prefix Sums**

Used when merging or cost = `sum(l..r)`.

**Template:**
```cpp
int cost = prefix[r] - prefix[l-1];
dp[l][r] = min(dp[l][r], dp[l][k] + dp[k+1][r] + cost);
```

> Problems:
>> * Merge Stones
>> * Min Cost Tree From Leaf Values

✅ **Pattern 6 — Interval DP + Memoized Recursion**

Sometimes easier to write top-down.

**Template:**
```cpp
int solve(l, r):
    if dp[l][r] exists return dp[l][r]

    for k in [l..r]:
        dp[l][r] = best(solve(l,k) + solve(k+1,r))
```

> Problems:
>> * Stone Game III
>> * Burst Balloons
>> * Guess Number II

----

HOW TO RECOGNIZE INTERVAL DP PROBLEMS

Look for ANY of these signs:

✔️ The problem asks about subarray/subsequence `[l, r]`

✔️ You choose a pivot OR split in middle

✔️ Cost depends on combining intervals

✔️ Order of picking choices matters

✔️ Minimize/maximize something over a contiguous segment

✔️ DP dimension is `dp[l][r]`

If any of these show up → it's interval DP.

----

### <span style="color:yellow">TOP INTERVAL DP PROBLEMS</span>

🟢 Beginner:

> LC 516: Longest Palindromic Subsequence
> 
> LC 1312: Min Insertions to Palindrome
> 
> LC 647: Count Palindromic Substrings (subset)

🟡 Intermediate:

> LC 375: Guess Number Higher or Lower II
> 
> LC 486: Predict the Winner
> 
> LC 877: Stone Game
> 
> LC 1690: Stone Game VII

🔥 Advanced:

> LC 312: Burst Balloons
> 
> LC 1000: Minimum Cost to Merge Stones
> 
> LC 1039: Minimum Score Triangulation
> 
> LC 1547: Minimum Cost to Cut Stick