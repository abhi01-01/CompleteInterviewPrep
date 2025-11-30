# BITMASK DP
* If DP is the final boss, then Bitmask DP is the boss’s boss. The most POWERFUL DP pattern in competitive programming. Master this, you can crush:

> * Can I Win
> 
> * Traveling Salesman (TSP)
> 
> * Assignment problems
> 
> * Subset DP
> 
> * Hard LC problems like Stickers to Spell Word, Pizza for 3, Partition to K subsets
> 
> * ANY problem involving subsets of size ≤ 20

<span style="color:yellow">**WHY BITMASK DP EXISTS**<span>

If `N ≤ 20` → number of subsets = `2^20` ≈ `1,048,576`
That's small enough to iterate.

Bitmask DP is basically:

> DP on all subsets of a small set.

Mask = integer where each bit = `0/1` indicating if element is included.


### ULTIMATE BITMASK DP PATTERN

```cpp
int dp[1<<n];
fill(dp, dp+(1<<n), INF);

dp[0] = base;

for (int mask = 0; mask < (1<<n); mask++) {
    for (int bit = 0; bit < n; bit++) {
        if (!(mask & (1<<bit))) {
            int next = mask | (1<<bit);
            dp[next] = min(dp[next], dp[mask] + cost(mask, bit));
        }
    }
}
```

run this structure → you can solve ANY bitmask DP problem on LC.

---
### <span style="color:yellow">5 CORE BITMASK DP PATTERNS<span>

✅ **Pattern 1 — Subset DP (`dp[mask]`)**

> This is the core pattern: each state is a subset mask.

Universal Template:
```cpp
for (int mask = 0; mask < (1<<n); mask++) {
    for (int bit = 0; bit < n; bit++) {
        if (mask & (1<<bit)) {
            dp[mask] = combine(dp[mask], dp[mask ^ (1<<bit)] + cost(bit));
        }
    }
}
```

This hits like 20 LC problems.

> Typical Uses:
>> * Precompute something for every subset
>> * Sum of subset elements
>> * Count number of elements
>> * Toggle bits
>> * DP over all groups

> Example Problem:
>> * LC 526: Beautiful Arrangement
>> * LC 1986: Min Sessions

✅ **Pattern 2 — DP on Subsets for Assignment (Perfect Matching)**

> Assign worker → job using DP over subsets.

State:

```pgsql
dp[mask] = min cost to complete jobs in mask
```

Template:

```cpp
dp[0] = 0;

for (int mask = 0; mask < (1<<n); mask++) {
    int worker = popcount(mask); // number of jobs taken

    for (int job = 0; job < n; job++) {
        if (!(mask & (1<<job))) {
            dp[mask | (1<<job)] =
                min(dp[mask | (1<<job)],
                    dp[mask] + cost[worker][job]);
        }
    }
}
```

> Problems:
>> * LC 1879: Minimum XOR Sum
>> * LC 1723: Minimum Time to Finish Jobs
>> * LC 2305: Fair Distribution of Cookies

✅ **Pattern 3 — Traveling Salesman Problem (TSP)**

> This is the MOST FAMOUS bitmask DP.

State:

```pgsql
dp[mask][i] = min cost ending at i after visiting mask
```

Template:

```cpp
for (int mask = 0; mask < (1<<n); mask++) {
    for (int u = 0; u < n; u++) {
        if (!(mask & (1<<u))) continue;

        for (int v = 0; v < n; v++) {
            if (mask & (1<<v)) continue;

            dp[mask | (1<<v)][v] =
                min(dp[mask | (1<<v)][v],
                    dp[mask][u] + dist[u][v]);
        }
    }
}
```

> Problems:
>> * Standard TSP
>> * LC 847: Shortest Path Visiting All Nodes

✅ **Pattern 4 — Bitmask + Memoized Recursion**

> Used in Can I Win, word breakup, partition, subset picking, etc.

Template:
```cpp
int solve(int mask):
    if dp[mask] exists return dp[mask]

    for each choice i:
        if bit i not used in mask:
            if solve(mask | (1<<i)) == losing for opponent:
                return dp[mask] = win

    return dp[mask] = lose
```

> Problems:
>> * LC 464: Can I Win
>> * LC 473: Matchsticks to Square
>> * LC 698: Partition Into K Equal Subsets

✅ **Pattern 5 — Iterate Over Submasks**

God-level trick.

Sometimes you need all submasks of a mask.

Template:
```cpp
for (int sub = mask; sub; sub = (sub - 1) & mask) {
    // all submasks of mask
}
```

> Problems:
>> * LC 1595: Minimum Cost to Connect Two Groups
>> * LC 1681: Minimum Incompatibility
>> * LC Hard problems involving partitioning subsets

---

### <span style="color:yellow">HOW TO RECOGNIZE BITMASK DP PROBLEMS<span>

Ask:

✔️ N ≤ 20?

✔️ Must track subsets of used things?

✔️ "Pick/unpick", "assign", "partition", "cover", "visit"?

✔️ State needs memory of which items used?

If yes → bitmask DP.

If you see ANY of these words:

* subset
* choose elements
* visited nodes
* used numbers
* distribute items
* assign jobs
* pick K out of N
* order doesn't matter

---

### <span style="color:yellow">THE UNIVERSAL BITMASK TRICKS</span>

✔️ Set a bit:
```cpp
mask | (1<<i)
```

✔️ Clear a bit:
```cpp
mask & ~(1<<i)
```
✔️ Toggle:
```cpp
mask ^ (1<<i)
```

✔️ Check:
```cpp
mask & (1<<i)
```
✔️ Count bits:
```cpp
__builtin_popcount(mask)
```
---

### <span style="color:yellow">TOP 10 BITMASK DP PROBLEMS</span>

🟢 Easy-Moderate:

> LC 78: Subsets
> 
> LC 1986: Minimum Sessions to Complete Tasks
> 
> LC 526: Beautiful Arrangement

🟡 Medium:

> LC 473: Matchsticks to Square
> 
> LC 698: Partition to K Equal Sum Subsets
> 
> LC 1879: Minimum XOR Sum of Two Arrays
> 
> LC 2305: Fair Distribution of Cookies
> 
> LC 1681: Minimum Incompatibility

🔥 Advanced:

> LC 464: Can I Win
> 
> LC 847: Shortest Path Visiting All Nodes (TSP)
> 
> LC 1125: Smallest Sufficient Team
> 
> LC 1595: Min Cost to Connect Two Groups