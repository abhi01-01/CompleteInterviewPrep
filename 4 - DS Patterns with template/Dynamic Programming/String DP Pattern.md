# THE 6 CORE STRING DP PATTERNS

✅ **Pattern 1 — Edit Distance Family (Convert One String → Another)**

> * This is the GOD-TIER pattern.
> * If you master this, you auto-solve 10+ classic problems.

**Recurrence:**
```cpp
if s1[i] == s2[j]
    dp[i][j] = dp[i-1][j-1]
else
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
        if (a[i-1] == b[j-1])
            dp[i][j] = dp[i-1][j-1];
        else
            dp[i][j] = 1 + min({dp[i-1][j], dp[i][j-1], dp[i-1][j-1]});
    }
}
```
> Classic Problems:
>> LC 72: Edit Distance
>> 
>> LC 161: One Edit Distance
>> 
>> LC 583: Delete To Make Strings Equal
>> 
>> LC 712: Min ASCII Delete Sum
>> 
>> LC 97: Interleaving String

---


✅ **Pattern 2 — Palindromic String DP (Substring + Subsequence)**

This is the most common DP in palindrome problems.

<span style="color:yellow">**(a) Palindromic Subsequence (LPS)**</span>

Compare string with itself via subsequence logic.

**Recurrence:**
```cpp
if s[l] == s[r]
    dp[l][r] = 2 + dp[l+1][r-1]
else
    dp[l][r] = max(dp[l+1][r], dp[l][r-1])
```

**Template:**
```cpp
for (int len = 2; len <= n; len++) {
    for (int l = 0; l + len - 1 < n; l++) {
        int r = l + len - 1;
        dp[l][r] = (s[l] == s[r])
                    ? 2 + dp[l+1][r-1]
                    : max(dp[l+1][r], dp[l][r-1]);
    }
}
```

<span style="color:yellow">**(b) Palindromic Substring DP**</span>

Check whether substring is palindrome.

**Template:**
```cpp
if (s[l] == s[r] && dp[l+1][r-1]) dp[l][r] = true;
```

> Classic Problems:
>> LC 516: Longest Palindromic Subsequence
>> 
>> LC 1312: Minimum Insertions to Palindrome
>> 
>> LC 5: Longest Palindromic Substring
>> 
>> LC 647: Count Palindromic Substrings

----

✅ **Pattern 3 — Wildcard/Regex Matching (Pattern Matching DP)**

> Used in `? *` matching and full regex-style DP.

<span style="color:yellow">**Wildcard Matching (? and *)**</span>

**Recurrence:**
```cpp
if p[j] == s[i] or p[j] == '?'
      dp[i][j] = dp[i-1][j-1]

if p[j] == '*'
      dp[i][j] = dp[i-1][j] (use *) OR dp[i][j-1] (ignore *)
```

**Template:**
```cpp
if (p[j-1] == '*')
    dp[i][j] = dp[i-1][j] || dp[i][j-1];
else if (p[j-1] == s[i-1] || p[j-1] == '?')
    dp[i][j] = dp[i-1][j-1];
```

<span style="color:yellow">**Regex Matching (. and *)**</span>

> Harder because `*` means "zero or more of previous character".

**Key Logic:**
```cpp
if char matches:
    dp[i][j] = dp[i-1][j-1]

if '*' present:
    dp[i][j] = dp[i][j-2]          // ignore char*
                OR
                dp[i-1][j]         // use one more repeat
```

> Classic Problems:
>> * LC 44: Wildcard Matching
>> * LC 10: Regular Expression Matching

---

✅ **Pattern 4 — Subsequence DP (LCS, SCS, delete ops)**

* Same pattern as LCS, used EVERYWHERE.

**Recurrence:**
```cpp
if s1[i] == s2[j]:
    dp = 1 + dp[i-1][j-1]
else:
    dp = max(dp[i-1][j], dp[i][j-1])
```

**Template:**

(same as standard LCS)

> Classic Problems:
>> LC 1143: LCS
>> 
>> LC 1092: Shortest Common Supersequence
>> 
>> LC 583: Delete Operations
>> 
>> LC 1312: Min Insertions for Palindrome
>> 
>> LC 712: Min ASCII Delete Sum

---

✅ **Pattern 5 — DP on Prefix Matches (KMP-like DP)**

**Used for:**

* String compression

* Count distinct subsequences

* Repeated string matching

* DP with prefix transitions

Example: LC 115 — Distinct Subsequences

```cpp
if s[i] == t[j]
   dp[i][j] = dp[i-1][j-1] + dp[i-1][j]
else
   dp[i][j] = dp[i-1][j]
```

----

✅ **Pattern 6 — Optimal Partition DP**

Break a string into pieces, minimize cost.

> Examples:
>> LC 132: Palindrome Partitioning II
>> 
>> LC 139: Word Break
>> 
>> LC 140: Word Break II
>> 
>> LC 1278: Palindrome Partitioning III

**Template:**
```cpp
for (i from n-1 → 0):
    dp[i] = INF;
    for (j from i → n-1):
        if substring(i,j) satisfies condition:
            dp[i] = min(dp[i], 1 + dp[j+1]);
```

----

### <span style="color:yellow">DP Pattern Map: How to Recognize problems</span>

When to use which:

```sql
If problem says:

Insert/Delete/Replace to convert string
➡️ Edit Distance DP
```

```sql
If problem says:

Is palindrome / build palindrome / min insertions
➡️ Palindromic DP
```
```sql
If problem says:

Compare two strings
➡️ LCS-based DP
```

```sql
If problem says

wildcard / regex / pattern matching
➡️ Pattern Matching DP
```

```sql
If problem says:

Break string into words / partitions
➡️ Partition DP
```

```sql
If problem says:

Count subsequences / count ways
➡️ Counting subsequences DP
```

----

### <span style="color:yellow">BEST STRING DP PROBLEMS TO MASTER (ordered)</span>


🟢 Beginner:

> LC 5: Longest Palindromic Substring
> 
> LC 647: Count Palindromic Substrings
> 
> LC 392: Is Subsequence
> 
> LC 1143: LCS

🟡 Intermediate:

> LC 1312: Min Insertions to Palindrome
> 
> LC 516: Longest Palindromic Subsequence
> 
> LC 72: Edit Distance
> 
> LC 712: Min ASCII Delete Sum

🔥 Advanced:

> LC 10: Regular Expression Matching
> 
> LC 44: Wildcard Matching
> 
> LC 1092: Shortest Common Supersequence
> 
> LC 115: Distinct Subsequences
> 
> LC 132: Palindrome Partitioning II
> 
> LC 140: Word Break II

----

### <span style="color:yellow">STRING DP</span>


| Pattern             | When                    |
| ------------------- | ----------------------- |
| Edit Distance       | Convert s → t           |
| LPS / Palindrome DP | Build/check palindromes |
| LCS                 | Compare two strings     |
| Regex / Wildcard DP | Pattern matches         |
| Partition DP        | Cut string into pieces  |
| Counting DP         | Count subsequences      |
