# DP (Only 8 patterns which cover entire DP) - Revision Sheeet

* ***DP Tree***
```rust
          (1) Subsequence DP
               /       \
      String DP      Edit Distance
       /   \
   LCS      LIS

          (2) Interval DP
              ↓
         Game Theory DP

          (3) 1D Running DP
           ↓
     Fibonacci, Robber

          (4) Knapsack DP
      /        |         \
  Subset    Coin     Partition

          (5) Tree DP
        /      \
   subtree   rerooting

          (6) Digit DP

          (7) Bitmask DP
        /           \
   TSP           Assign Workers

          (8) Minimax DP (games)
            uses Interval DP
```

### 1. <span style="color:yellow">Subsequence DP (`1D`/`2D` DP on `i`/`j` indexes)</span>

<span style="color:orange">This includes:</span>
* LCS
* LIS
* Edit distance
* Palindromic subsequence
* String matching
* Sequence alignments

<span style="color:orange">Recognition Rule</span>

* If the problem compares two sequences OR decisions depend on `i` and `j` moving independently, it’s subsequence DP.

Keywords:
* `i`, `j`, “subsequence”, “transform”, “alignment”, “edit”.

<span style="color:orange">Core idea:</span>

> You compare characters at i and j → dp transition.

Formula
```powershell
dp[i][j] = best using s1[0..i], s2[0..j]
```

For LCS:
```cpp
if s1[i] == s2[j]:
    dp[i][j] = dp[i-1][j-1] + 1
else:
    dp[i][j] = max(dp[i-1][j], dp[j][j-1])
```

Template
```cpp
for(int i=1;i<=n;i++){
    for(int j=1;j<=m;j++){
        if(s1[i-1] == s2[j-1]) 
            dp[i][j] = dp[i-1][j-1] + 1;
        else 
            dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
    }
}
```

> Problem
>> * LC 1143: Longest Common Subsequence

### 2. <span style="color:yellow">Subarray / Interval DP (`dp[l][r]`)</span>

You pick from range `[l…r]`.

<span style="color:orange">Used for:</span>
* Burst Balloons
* Stone Game
* Minimum Cost to Cut Stick
* Palindromic substring DP
* Matrix Chain Multiplication

<span style="color:orange">Recognition Rule</span>

* If the problem asks for best answer on subarray `[l…r]` and requires splitting at various `k`→ INTERVAL DP.

Keywords:
* "choose k", "split", "ranges", "interval".

Formula
```cpp
dp[l][r] = best over k in [l..r] of:
    dp[l][k] + dp[k+1][r] + cost(l,k,r)
```

Template
```cpp
for(int len = 2; len <= n; len++){
    for(int l = 0; l+len-1 < n; l++){
        int r = l + len - 1;
        for(int k = l; k < r; k++){
            dp[l][r] = min(dp[l][r], dp[l][k] + dp[k+1][r] + cost);
        }
    }
}
```

> Problem
>> * LC 312: Burst Balloons

### 3. <span style="color:yellow">Kadane-style / Optimal Substructure on 1D (Prefix/Running DP)</span>

<span style="color:orange">Used for:</span>
* Fibonacci
* max subarray
* Climbing stairs
* house robber
* maximum sum subsequence
* 1D DP with recurrence based only on previous states

<span style="color:orange">Recognition Rule</span>

* If answer depends ONLY on previous few states (like `dp[i−1]`, `dp[i−2]`) → Linear DP.

Keywords:
* “max sum”, “non-adjacent”, “till index `i`”.

Formula
```cpp
dp[i] = max(include i, exclude i)
```

House Robber:
```cpp
dp[i] = max(dp[i-1], dp[i-2] + nums[i])
```

Template
```cpp
dp[0] = nums[0];
dp[1] = max(nums[0], nums[1]);

for(int i = 2; i < n; i++){
    dp[i] = max(dp[i-1], dp[i-2] + nums[i]);
}
```

> Problem
>> * LC 198: House Robber

### 4. <span style="color:yellow">KNAPSACK DP (Choice DP)

<span style="color:orange">Used for:</span>
* Subset sum
* Target sum
* Coin change
* Unbounded knapsack
* Partition equal subset
* DP over choices

<span style="color:orange">Recognition Rule</span>

* If you see “choose item or skip item” → KNAPSACK.

Keywords:
* “pick or not pick”, “capacity”, “sum = target”, “count ways”.

Formula

0/1:
```cpp
dp[i][w] = max(
    dp[i-1][w],            // skip
    dp[i-1][w - weight[i]] + value[i]  // pick
)
```

Coin change (unbounded):
```sql
dp[w] += dp[w - coin]
```

Template
```cpp
for(int i=1;i<=n;i++){
    for(int w=0; w<=W; w++){
        if(w >= wt[i]) 
            dp[i][w] = max(dp[i-1][w], dp[i-1][w-wt[i]] + val[i]);
        else 
            dp[i][w] = dp[i-1][w];
    }
}
```

> Problem
>> * LC 416: Partition Equal Subset Sum
>> * LC 322: Coin Change (unbounded form)

### 5. <span style="color:yellow">TREE DP (DFS + Combine children)</span>

<span style="color:orange">Used for:</span>
* House Robber III
* Diameter of tree
* Path sum
* Subtree DP
* Rerooting DP

<span style="color:orange">Recognition Rule</span>

* If the input is a tree and answer depends on subtrees, it's Tree DP.

Keywords:
* “children”, “subtree”, “rooted tree”, “combine child states”.

Formula
```cpp
dp[u] = merge( dp of each child )
```

Template
```cpp
int dfs(int u, int parent) {
    for (int v : adj[u]) {
        if (v == parent) continue;
        dfs(v, u);
        dp[u] = combine(dp[u], dp[v]);
    }
}
```

> Problem
>> * LC 337: House Robber III

### 6. <span style="color:yellow">DIGIT DP (DP on digits + tight constraint)</span>

<span style="color:orange">Used for:</span>
* count numbers in range
* sum of digits
* numbers without repeated digits
* modulo DP on large numbers

<span style="color:orange">Recognition Rule</span>

* If constraints involve digits of a number + “till 10^18”, you automatically use digit DP.

Keywords:
* “count numbers ≤ N”, “digits”, “tight/loose”, “leading zeros”.

Formula
```sql
dp[pos][tight][leading][state] = count
```
Template
```cpp
int dfs(int pos, bool tight, bool leading, int state){
    if(pos == len) return valid(state);

    int limit = tight ? digits[pos] : 9;

    for(int d=0; d<=limit; d++){
        ans += dfs(pos+1, tight && d==limit, leading && d==0, newState);
    }
    return ans;
}
```

> Problem
>> * LC 1012: Numbers With Repeated Digits
or
Count numbers <span N with digit sum divisible by K

### 7. <span style="color:yellow">BITMASK DP (Subset DP)</span>

<span style="color:orange">Used for:</span>
* TSP
* Assign workers → jobs
* Can I Win
* Choose subsets
* DP on small sets (n ≤ 20)

<span style="color:orange">Recognition Rule</span>

* If the state tracks “which items are used”, ← BITMASK DP.

Keywords:
* “subset”, “mask”, “used/un-used”, “all combinations”.

Formula
```sql
dp[mask] = best using subset = mask
```

TSP:
```sql
dp[mask][i] = min over j in mask:
    dp[mask ^ (1<<i)][j] + dist[j][i]
```

Template
```cpp
for(mask = 0; mask < (1<<n); mask++){
    for(each item i not in mask){
        dp[mask | (1<<i)] = min(dp[mask | (1<<i)], dp[mask] + cost);
    }
}
```

> Problem
>> * LC 464: Can I Win
>> * LC 698: Partition to K subsets

### 8. <span style="color:yellow">GAME THEORY DP (Minimax + DP + intervals)

<span style="color:orange">Used for:</span>
* Predict the winner
* Stone games
* Flip games
* All turn-based 2-player optimal games

<span style="color:orange">Recognition Rule</span>

* If two players alternate turns and try to maximize win → MINIMAX DP.

Keywords:
* “player1 vs player2”, “optimal play”, “maximize difference”.

Formula

Classic:
```cpp
dp[l][r] = max(
    nums[l] - dp[l+1][r],
    nums[r] - dp[l][r-1]
)
```

Template
```cpp
int solve(l,r):
    if(l==r) return nums[l];
    return max(nums[l] - solve(l+1,r),
               nums[r] - solve(l,r-1));
```

> Problem
>> * LC 486: Predict the Winner
>> * LC 877: Stone Game

