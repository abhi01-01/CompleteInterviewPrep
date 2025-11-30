# 5 GAME THEORY DP PATTERNS

✅ **Pattern 1 — Minimax (Score Difference DP)**

THE MOST IMPORTANT PATTERN.
This is used in:
> * Predict The Winner
> * Stone Games
> * Removing stones from left/right
> * Turn-based picking from array

State:
```sql
dp[l][r] = max score difference the current player can get from nums[l..r]
```

Recurrence:

```sql
If take left:  diff = nums[l] - dp[l+1][r]
If take right: diff = nums[r] - dp[l][r-1]

dp[l][r] = max(diffLeft, diffRight)
```

Template:
```cpp
int solve(int l, int r) {
    if (l == r) return nums[l];
    if (dp[l][r] != -1) return dp[l][r];

    int left = nums[l] - solve(l+1, r);
    int right = nums[r] - solve(l, r-1);

    return dp[l][r] = max(left, right);
}
```

> Problems:
>> * LC 486: Predict the Winner
>> * LC 877: Stone Game
>> * LC 1690: Stone Game VII
>> * LC 1406: Stone Game III
>> * LC 1563: Stone Game V

✅ **Pattern 2 — Grundy Numbers (Nim Game Theory)**

Used when:
> * Multiple piles
> * You can split piles
> * You have moves like `+k`, `-k`, `xor`, etc
> * You combine independent games
> * This is known as Sprague–Grundy Theorem.

Grundy rule:

```perl
G(state) = mex( { G(all next states) } )
Result is losing position if xor of all pile Grundy values == 0
```

Template:
```cpp
int grundy(state):
    if memo[state] return memo[state]

    unordered_set<int> next;
    for each move:
        next.insert(grundy(nextState));

    return memo[state] = mex(next);
```

> Problems:
>> * LC 292: Nim Game
>> * LC 1025: Divisor Game
>> * LC 1908: Game of Nim
>> * LC 2029: Stone Game IX
>> * LC Hard: Wording Game

✅ **Pattern 3 — DFS + Memo (Boolean Win/Lose DP)**

Used when:
> * Finite choices
> * You check if ANY move leads opponent to losing state

State:

```perl
dp[state] = can the current player win?
```

Template:
```cpp
bool solve(state):
    if dp[state] known return dp[state]

    for each move m:
        if solve(state_after_m) == false:
            return dp[state] = true;

    return dp[state] = false;
```

> Problems:
>> * LC 464: Can I Win
>> * LC 294: Flip Game II
>> * LC 292: Nim (boolean version)
>> * LC 2038: Remove Colored Pieces Game

✅ **Pattern 4 — Interval DP + Game (2 players picking)**

When picking from an interval and scoring.

Idea:

The game becomes:

```sql
dp[l][r] = best difference or best score current player gets
```

Template:

(Same as Predict the Winner but generalized)
```cpp
dp[l][r] = max over all moves (
    value(move) - dp[new_l][new_r]
)
```

> Problems:
>> * Guess Number II
>> * Stone Game II
>> * Stone Game VII
>> * Stone Game V
>> * Stone Game III

✅ **Pattern 5 — Turn-based DP (dp[i][j][turn])**

Used when:

* Turn matters explicitly
* There are more than 2 types of moves
* Score affects player differently

Template:

```cpp
int solve(i, j, turn):
    if turn == 0:
        return max(for all moves solve(next_i, next_j, 1))
    else:
        return min(for all moves solve(next_i, next_j, 0))
```


> Problems:
>> * LC 375: Guess Number Higher or Lower II
>> * LC 486 (alternate style)
>> * Cat and Mouse I & II
>> * Chess-like DP problems

-----


### <span style="color:yellow">HOW TO RECOGNIZE GAME THEORY DP PROBLEMS</span>

Look for phrases like:
* “Player 1 and Player 2 take turns...”
* “Both players play optimally”
* “Determine if Player 1 can win”
* “Find maximum score difference”
* “Return true if first player wins”
* “Pick from left or right”
* “You may remove any pile and split it”

If any of these appear → it's game theory DP.

----

### <span style="color:yellow">MASTER TEMPLATES (memorizable)</span>

These two solve 80% of game problems:

Template A — Score Difference DP
```cpp
int f(l, r):
    if l == r: return nums[l]
    return max(nums[l] - f(l+1, r),
               nums[r] - f(l, r-1))
```

Template B — Boolean Win/Lose
```cpp
bool canWin(state):
    for each valid move:
        if (!canWin(nextState))
            return true;
    return false;
```

----

### <span style="color:yellow">MUST-SOLVE PROBLEMS (Ordered Guide)</span>

🟢 EASY:

> LC 292: Nim Game
> 
> LC 1025: Divisor Game

🟡 MED:

> LC 486: Predict the Winner
> 
> LC 294: Flip Game II
> 
> LC 877: Stone Game
> 
> LC 1908: Game of Nim
> 
> LC 1927: Sum Game
> 
> LC 2029: Stone Game IX
> 
> LC 2038: Remove Colored Pieces

🔥 ADVANCED:

> LC 375: Guess Number Higher or Lower II
> 
> LC 1140: Stone Game II
> 
> LC 1406: Stone Game III
> 
> LC 1563: Stone Game V
> 
> LC 1686: Stone Game VI
> 
> LC 1690: Stone Game VII
> 
> LC 1872: Stone Game VIII

💀 HARDCORE:

> LC 913: Cat and Mouse
> 
> LC 1728: Cat and Mouse II
> 
> LC 3283: Maximum Moves to Kill Pawns
> 
> LC 343: Integer Break Game variants

-----

### <span style="color:yellow">GAME THEORY DP MAP</span>

| Problem type                | Use                  |
| --------------------------- | -------------------- |
| Pick from left/right        | Score difference DP  |
| True/false if Player 1 wins | Minimax boolean DP   |
| Complex moves               | Turn-based DP        |
| Multiple piles              | Grundy (Nim)         |
| Independent subgames        | XOR of Grundy values |
| Interval scoring            | Interval DP          |
