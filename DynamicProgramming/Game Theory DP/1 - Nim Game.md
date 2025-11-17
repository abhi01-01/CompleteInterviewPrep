## Leetcode - 292 - [Nim game](https://leetcode.com/problems/nim-game/description/?envType=problem-list-v2&envId=game-theory)

Example 1:
```sql
Input: n = 4
Output: false
Explanation:
If there are 4 stones, no matter what you remove:
- remove 1 → 3 left → opponent removes all 3 → you lose
- remove 2 → 2 left → opponent removes both → you lose
- remove 3 → 1 left → opponent removes 1 → you lose
```
Example 2:
```vbnet
Input: n = 5
Output: true
Explanation: remove 1 → 4 left → opponent loses.
```

**Step 1: Define the recursive thinking**

Let’s define a function:

> `canWin(n)` → returns `true` if the player with `n` stones can force a win.

Recurrence logic:

If you can make a move that forces your opponent into a losing position,
then your current position is winning.

So:
```pgsql
canWin(n) = false, if all next moves lead to win for opponent.
canWin(n) = true, if there exists a move that leads to loss for opponent.
```

Mathematically:
```yaml
canWin(n) = !(canWin(n-1) && canWin(n-2) && canWin(n-3))
```

→ If all next 3 states are winning for the opponent, then you lose.
→ Else, you win.

**Step 2: Base Cases**

When n <= 3 → you can take all stones → you win.
```csharp
canWin(1) = true
canWin(2) = true
canWin(3) = true
```

When n = 4 → all next states (1, 2, 3) are winning for the opponent → you lose.

---

* TopDown Approach - Without Memoization
```cpp
class TopDown{
    public:
    bool solveWithoutMemo(int n) {
        if (n <= 3) return true;
        // if all moves make opponent win, you lose
        return !(solveWithoutMemo(n-1) && solveWithoutMemo(n-2) && solveWithoutMemo(n-3));
    }

    bool canWinNim(int n) {
        return solveWithoutMemo(n);
    }
};
```

> Time Complexity = O(3<sup>N</sup>)

> Space Complexity = O(3*N) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
    public:
    bool solveMemo(int n, vector<int>& dp) {
        if (n <= 3) return true;
        if (dp[n] != -1) return dp[n];
        return dp[n] = !(solveMemo(n-1, dp) && solveMemo(n-2, dp) && solveMemo(n-3, dp));
    }

    bool canWinNim(int n) {
        vector<int> dp(n+1, -1);
        return solveMemo(n, dp);
    }
};
```

> Time Complexity = O(3*N)

> Space Complexity = O(4*N) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- Tabulation / Loop Method

```cpp
class BottomUp{
public:
    bool solveWithTabulation(int n){
        vector<bool> dp(n+1, false) ;
        dp[0] = dp[1] = dp[2] = dp[3] = true ;

        for(int i = 4 ; i <=n ; ++i){
            dp[i] = !(dp[i-1] and dp[i-2] and dp[i-3]) ;
        }
        return dp[n] ;
    }
    bool canWinNim(int n) {
        return solveWithTabulation(n) ; 
    }
};
```

> Time Complexity = O(N)

> Space Complexity = O(N)

---

* Bottom Up Approach -- Optimized

```cpp
class BottomUp{
public:
    bool solveWithTabulation(int n){
        // dp[1] = dp[2] = dp[3] = true ;
        bool a = true, b = true, c = true ;

        for(int i = 4 ; i <=n ; ++i){
            bool d = !(c and b and a) ;
            a = b ;
            b = c ;
            c = d ; 
        }
        return c ;
    }
    bool canWinNim(int n) {
        return solveWithTabulation(n) ; 
    }
};
```

> Time Complexity = O(N)

> Space Complexity = O(1)

---

* Brainteaser

Mathematical Observation (1-line insight)

If you observe pattern:
```sql
n	Result
1	Win
2	Win
3	Win
4	Lose
5	Win
6	Win
7	Win
8	Lose

So it repeats every 4.
👉 You lose when n % 4 == 0.
```
**Solution Code**

```cpp
class Solution {
public:
    bool canWinNim(int n) {
        return (n%4 != 0) ;
    }
};
```

> Time Complexity = O(1)

> Space Complexity = O(1)