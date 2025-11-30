# THE COMPLETE KNAPSACK PATTERN GUIDE

## <span style="color:yellow">PART 1 — 0/1 KNAPSACK (Choose or Skip Once)</span>

> You either take the item ONCE or skip it.

**Core recursion:**
```sql
dp[i][w] = max profit using first i items with capacity w
```

💥 **Standard Template (2D → 1D optimized):**

✔️ 2D DP:
```cpp
for (int i = 1; i <= n; i++) {
    for (int w = 0; w <= W; w++) {
        if (wt[i] <= w)
            dp[i][w] = max(dp[i-1][w], dp[i-1][w - wt[i]] + val[i]);
        else
            dp[i][w] = dp[i-1][w];
    }
}
```

✔️ 1D optimized (REVERSE loop):

```cpp
for (int i = 1; i <= n; i++) {
    for (int w = W; w >= wt[i]; w--) {
        dp[w] = max(dp[w], dp[w - wt[i]] + val[i]);
    }
}
```

> Why reverse?
>> To prevent reusing the same item multiple times.

----

## <span style="color:yellow">PART 2 — UNBOUNDED KNAPSACK (Infinite Supply Items)</span>

> You can pick the same item multiple times.

Template (NOTICE: forward loop):
```cpp
for (int i = 1; i <= n; i++) {
    for (int w = wt[i]; w <= W; w++) {
        dp[w] = max(dp[w], dp[w - wt[i]] + val[i]);
    }
}
```

> Why forward loop?
>> Because `dp[w]` depends on `dp[w - wt[i]]` in the same iteration, allowing reuse.

----

## <span style="color:yellow">PART 3 — Subset Sum / Count Subsets / Target Sum (Boolean Knapsack)</span>

> Instead of max profit → can you form a sum?

✔️ Template:
```cpp
dp[0] = true;

for (int num : nums) {
    for (int w = target; w >= num; w--) {
        dp[w] = dp[w] || dp[w - num];
    }
}
```

> Uses:
>> * Subset sum
>> * Partition equal subset sum
>> * Target sum (can be modified)

----

## <span style="color:yellow">PART 4 — Minimum Subset Difference (Partition Style DP)</span>

> classic DP for splitting into two parts.

Template:

Same as subset-sum, but compute:
```cpp
for (i in range sum/2 down to 0)
    if dp[i] == true:
        ans = sum - 2*i
```

## <span style="color:yellow">PART 5 — Bounded (Multiple) Knapsack</span>

* Each item has limited counts.
* You convert bounded → multiple 0/1 knapsacks OR binary split trick.

⭐ Binary Split (Most efficient):

If an item has count k → represent it as sums of powers of 2:
```cpp
1, 2, 4, ..., remaining
```

Then treat as 0/1 knapsack for each.

----

## <span style="color:yellow">PART 6 — Combination Sum Style (Counting ways)</span>

How many ways to reach sum?

✔️ Order-independent:
```cpp
for (num in nums)
    for (w = num..target)
        dp[w] += dp[w - num];
```
✔️ Order-dependent:
```cpp
for (w = 0..target)
    for (num in nums)
        dp[w] += dp[w - num];
```

----

## <span style="color:yellow">PART 7 — Knapsack with Exact Fill</span>

> "Reach sum EXACTLY" pattern.

Template:
```cpp
vector<int> dp(target+1, INF);
dp[0] = 0;

for (num : nums) {
    for (int w = target; w >= num; w--) {
        dp[w] = min(dp[w], dp[w-num] + 1);
    }
}
```

> Used in:
>> * coin change (min coins)
>> * rod cutting

---


## <span style="color:yellow">PART 8 — Knapsack on Trees</span>

Heavy but powerful — combine DP from child subtrees.

> Used in:
>> * DP on rooted tree with capacity
>> * Maximum independent set in tree
>> * Apple collecting problems

Template looks like:
```cpp
dfs(u):
  start with dp[u][c] = 0
  for each child v:
      dfs(v)
      merge dp[u] and dp[v]
```

----

## <span style="color:yellow">PART 9 — Game Theory Knapsack</span>

> Used when you choose piles / stones optimally.

----

## <span style="color:yellow">KNAPSACK CHEAT SHEET (MEMORIZE THIS)</span>
✔️ 0/1 knapsack → reverse loop
```cpp
for (w = W → 0)
```
✔️ Unbounded knapsack → forward loop
```cpp
for (w = 0 → W)
```
✔️ Subset sum → boolean dp
```cpp
dp[w] = dp[w] || dp[w - x];
```
✔️ Min coins → dp with min + INF
```cpp
dp[w] = min(dp[w], dp[w-x] + 1);
```
✔️ Count ways → additive dp
```cpp
dp[w] += dp[w-x];
```

----

### <span style="color:yellow">**PROBLEMS TO MASTER (THE OFFICIAL LIST)**</span>

> 0/1 Knapsack Style:
>> * LC 416: Partition Equal Subset Sum
>> * LC 494: Target Sum
>> * LC 474: Ones and Zeroes
>> * LC 698: Partition into k subsets

> Unbounded:
>> * LC 322: Coin Change
>> * LC 518: Coin Change II
>> * LC 279: Perfect Squares
>> * LC 1449: Form Largest Integer With Digits

> Combinational:
>> * LC 39: Combination Sum
>> * LC 40: Combination Sum II
>> * LC 377: Combination Sum IV

> Advanced:
>> * LC 474: Ones and Zeroes (2D knapsack)
>> * LC 879: Profitable Schemes (3D knapsack)
>> * LC 1049: Last Stone Weight II (balanced partition)
>> * LC 494: Target Sum