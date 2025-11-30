# SUBSEQUENCE DP — THE 6 CORE PATTERNS

✅ **Pattern 1 — Longest Increasing Subsequence (LIS Pattern)**

This is the core subsequence structure.

**Recurrence:**
```cpp
dp[i] = length of LIS ending at i
dp[i] = 1 + max(dp[j]) for all j < i and nums[j] < nums[i]
```
**Template:**
```cpp
for (int i = 0; i < n; i++) {
    dp[i] = 1;
    for (int j = 0; j < i; j++) {
        if (nums[j] < nums[i])
            dp[i] = max(dp[i], dp[j] + 1);
    }
}
```
> Problems:
>> * LC 300 — Longest Increasing Subsequence
>> * LC 673 — Number of LIS
>> * LC 1713 — Minimum Operations to Make Target Subsequence

----

✅ **Pattern 2 — Longest Common Subsequence (LCS Pattern)**

* This is the mother of string DP.
* If you know LCS, you can solve 10+ problems instantly.

**Recurrence:**
```cpp
if s1[i] == s2[j]
    dp[i][j] = 1 + dp[i-1][j-1]
else
    dp[i][j] = max(dp[i-1][j], dp[i][j-1])
```

**Template:**
```cpp
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= m; j++) {
        if (s1[i-1] == s2[j-1])
            dp[i][j] = 1 + dp[i-1][j-1];
        else
            dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
    }
}
```

> Problems:
>> * LC 1143 — LCS
>> * LC 583 — Delete to Make Strings Equal
>> * LC 1312 — Minimum Insertions to Make a String Palindrome (via LCS)
>> * LC 712 — Minimum ASCII Delete Sum

----

✅ **Pattern 3 — Edit Distance (Levenshtein Distance)**

> Core idea: convert string A → B with min operations.

**Recurrence:**
```cpp
if s1[i] == s2[j] → dp[i][j] = dp[i-1][j-1]
else:
 dp[i][j] = 1 + min(
    dp[i-1][j],   // delete
    dp[i][j-1],   // insert
    dp[i-1][j-1]  // replace
 )
```

**Template:**
```cpp
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= m; j++) {
        if (s1[i-1] == s2[j-1])
            dp[i][j] = dp[i-1][j-1];
        else
            dp[i][j] = 1 + min({ dp[i-1][j], dp[i][j-1], dp[i-1][j-1] });
    }
}
```

> Problems:
>> * LC 72 — Edit Distance
>> * LC 161 — One Edit Distance
>> * LC 97 — Interleaving String

---

✅ **Pattern 4 — Palindromic Subsequence DP (LPS Pattern)**

> The DP that solves all palindrome problems.

**Recurrence:**
```cpp
if s[l] == s[r]:
    dp[l][r] = 2 + dp[l+1][r-1]
else:
    dp[l][r] = max(dp[l+1][r], dp[l][r-1])
```

**Template:**
```cpp
for (int len = 2; len <= n; len++) {
    for (int l = 0; l + len - 1 < n; l++) {
        int r = l + len - 1;

        if (s[l] == s[r])
            dp[l][r] = 2 + dp[l+1][r-1];
        else
            dp[l][r] = max(dp[l+1][r], dp[l][r-1]);
    }
}
```

> Problems:
>> * LC 516 — Longest Palindromic Subsequence
>> * LC 1312 — Make Palindrome With Min Insertions
>> * LC 730 — Count Palindromic Subsequences

----

✅ **Pattern 5 — Subsequence Counting (Count Ways DP)**

> Answer = number of subsequences, not length.

**Recurrence:**
```cpp
if match:
   dp[i][j] = dp[i-1][j-1] + dp[i-1][j]
else:
   dp[i][j] = dp[i-1][j]
```
**Template:**
```cpp
for (int i = 1; i <= n; i++) {
    for (int j = 1; j <= m; j++) {
        if (s1[i-1] == s2[j-1])
            dp[i][j] = dp[i-1][j-1] + dp[i-1][j];
        else
            dp[i][j] = dp[i-1][j];
    }
}
```

> Problems:
>> * LC 115 — Distinct Subsequences
>> * LC 392 — Is Subsequence
>> * LC 940 — Distinct Subsequences II

----

✅ **Pattern 6 — "Take or Skip" Recursion → DP (Subsequence core recursion)**

> Almost ANY subsequence DP starts with:

* Recursion Template (Top-Down):
```cpp
int solve(int i, int j) {
    if (i == n or j == m) return base;

    if (match)
        return 1 + solve(i+1, j+1);
    else
        return max(solve(i+1, j), solve(i, j+1));
}
```

Then you memoize:
```cpp
dp[i][j] = result;
```

----

# HACK (Memoize this)

1. <span style="color:yellow">If comparing two sequences → LCS grid</span>

> Examples:
>> * LCS
>> * Edit distance
>> * Delete operations
>> * Minimum insertions
>> * Strings become equal

2. <span style="color:yellow">If comparing a sequence with itself reversed → Palindromic DP</span>

> Examples:
>> * LPS
>> * Min insertions to palindrome

3. <span style="color:yellow">If finding strictly increasing or decreasing → LIS DP</span>

> Examples:
>> * LIS
>> * Russian doll envelopes
>> * Minimum removals to make mountain array

4. <span style="color:yellow">If counting ways to pick subsequences → Counting DP</span>

> Examples:
>> * Distinct subsequences
>> * Count palindromic subsequences

5. <span style="color:yellow">If choose/skip behavior → Top-down subsequence DP</span>

> Examples:
>> * Any DP where index increments but not in sync
>> * DP with constraints like "take or skip this character"

-----

## 🧩 TOP PROBLEMS TO MASTER (ordered)

🟢 **Beginner:**

> LC 300 — LIS
> 
> LC 1143 — LCS
> 
> LC 392 — Is Subsequence
> 
> LC 583 — Delete Operation

🟡 **Intermediate:**

> LC 516 — LPS
> 
> LC 718 — Longest Common Substring
> 
> LC 647 — Count Palindromic Substrings
> 
> LC 72 — Edit Distance

🔥 **Advanced:**

> LC 115 — Distinct Subsequences
> 
> LC 1092 — Shortest Common Supersequence
> 
> LC 730 — Count Palindromic Subsequences
> 
> LC 1035 — Uncrossed Lines
> 
> LC 1312 — Min Insertions to Palindrome

