## LC - 1025 - [Divisor Game](https://leetcode.com/problems/divisor-game/?envType=problem-list-v2&envId=game-theory)

Example 1:
```yaml
Input: n = 2
Output: true
Explanation: Alice chooses x = 1 → n = 1. 
Now Bob has no moves → Alice wins.
```
Example 2:
```yaml
Input: n = 3
Output: false
Explanation:
Alice can only choose x = 1 → n = 2.
Then Bob chooses x = 1 → n = 1.
Alice has no moves → Bob wins.
```
Step 1: Define the state

Let’s define:

> `dp[n]` = `true` if the player starting with `n` stones can force a win.

Just like Nim, if you can move to any losing state, you win.

Step 2: Base Case

If `n = 1`:

* Alice has no valid moves (since `1` has no divisors `< 1`)
→ she loses.

So:
```yaml
dp[1] = false
```
Step 3: Recurrence Relation

For any `n > 1`:

Alice can choose any divisor `x` where `1 ≤ x < n` and `n % x == 0`.

If there exists an `x` such that after making that move,
the opponent loses, then current n is a winning position.

Formally:
```yaml
dp[n] = exists x (n % x == 0 and dp[n - x] == false)
```

---
### Solutions


* TopDown Approach - Without Memoization
```cpp
class TopDown{
public:
    bool solveWithoutMem(int n){
        if(n <= 1){
            return false ;
        }
        for(int i = 1 ; i < n ; ++i){
            if((n%i) == 0){
                return !solveWithoutMem(n-i) ;
            }
        }
        return false ;
    }

    bool divisorGame(int n) {
        return solveWithoutMem(n) ;
    }    
};
```

> Time Complexity = O(2<sup>N</sup>)

> Space Complexity = O(N) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
    public:
    bool solveWithMem(int n, vector<int>& dp){
        if(n <= 1){
            return false ;
        }
        if(dp[n] != -1){
            return dp[n] ;
        }

        for(int i = 1 ; i < n ; ++i){
            if((n%i) == 0){
                return dp[n] = !solveWithMem(n-i, dp) ;
            }
        }
        return dp[n] = false ;
    }

    bool divisorGame(int n) {
        vector<int> dp(n+1, -1) ;
        return solveWithMem(n, dp) ;
    }
};
```

> Time Complexity = O(N<sup>2</sup>)

> Space Complexity = O(2*N) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- Tabulation / Loop Method

```cpp
class BottomUp{
public:
    bool tabulation(int n){
        vector<bool> dp(n+1, false) ;

        for(int cur = 2 ; cur <= n ; ++cur){
            for(int i = 1 ; i < n ; ++i){
                if((cur%i) == 0){
                    dp[cur] = !dp[cur-i] ;
                    break ;
                }
            }
        }
        return dp[n] ;
    }

    bool divisorGame(int n) {
        return tabulation(n) ;
    }
};
```

> Time Complexity = O(N<sup>2</sup>)

> Space Complexity = O(N)

---

* Bottom Up Approach -- Optimized(Sapce or time)

```cpp
class BottomUp{
// can't be optimized
};
```

> Time Complexity = O()

> Space Complexity = O()

---

* Brainteaser

Mathematical Observation (1-line insight)

If you print dp for small n:
```sql
n	dp[n]
1	F
2	T
3	F
4	T
5	F
6	T

🎯 Pattern → Alice wins when n is even.
```
* If n is even, Alice wins.
* If n is odd, Alice loses.

```cpp
class Solution {
public:
    bool divisorGame(int n) {
        return (n%2 == 0) ; 
    }
};
```

> Time Complexity = O(1)

> Space Complexity = O(1)