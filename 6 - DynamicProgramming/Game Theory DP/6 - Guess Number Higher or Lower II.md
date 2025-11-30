## LC - 375 - [Guess Number Higher or Lower II](https://leetcode.com/problems/guess-number-higher-or-lower-ii/description/?envType=problem-list-v2&envId=game-theory)

Example
```pgsql
Input: n = 10
Output: 16
Explanation:
Worst-case strategy guarantees you’ll never pay more than 16 coins.
```

This is not aiming to get lucky — it's planning for the worst case.

Key Insight:

For each guess `x`, if you're wrong:

* If the real number is lower than `x`, you guess in range `[low, x-1]`

* If it’s higher, you guess in `[x+1, high]`

And since you're prepping for the worst-case:
```sql
cost = x + max(cost[low to x-1], cost[x+1 to high])
```

Your job is to find the minimum of this cost over all possible `x` in the range.

Recursive Formula (Without DP)

Define:
```sql
f(l, r) = minimum money to guarantee a win in range [l, r].
```
Recurrence:
```sql
f(l, r) = min over x in [l, r]:  
        x + max(f(l, x-1), f(x+1, r))
```

Base case:
```sql
if l >= r: return 0
```

👉 No cost if there's only one number or none to guess.

__TL;DR Strategy__

>For every possible guess `x`, think:
>>“If I’m wrong, what’s the worst amount I’ll need to pay?”
>>
>>Choose the guess that minimizes that maximum loss.

> **Solutions**


* TopDown Approach - Without Memoization
```cpp
class TopDown{
    public:
    int solveWithoutMemo(int low, int high){
        if(high <= low){
            return 0 ;
        }

        int ans = INT_MAX ;

        for(int x = low ; x <= high ; ++x){
            int cost = x + (max(solveWithoutMemo(low, x-1), solveWithoutMemo(x+1, high))) ;

            ans = min(ans, cost) ; 
        }
        return ans ;
    }

    int getMoneyAmount(int n) {
        return solveWithoutMemo(1, n) ;
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
    int solveWithMemo(int low, int high, vector<vector<int>>& dp){
        if(high <= low){
            return 0 ;
        }

        if(dp[low][high] != -1){
            return dp[low][high] ;
        }

        int ans = INT_MAX ;

        for(int x = low ; x <= high ; ++x){
            int cost = x + (max(solveWithMemo(low, x-1, dp), solveWithMemo(x+1, high, dp))) ;

            ans = min(ans, cost) ; 
        }
        return dp[low][high] = ans ;
    }

    int getMoneyAmount(int n) {
        vector<vector<int>> dp(n+1, vector<int>(n+1, -1)) ;
        return solveWithMemo(1, n, dp) ;
    }
};
```

> Time Complexity = O(N<sup>3</sup>)

> Space Complexity = O(N<sup>2</sup>) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- Tabulation / Loop Method

<span style="color:yellow">**First, what the DP table means:**</span>

`dp[l][r]` = the minimum cost to guarantee a win if the secret number is in the range `[l, r]`.

* If `l == r` → only one number → no need to guess → `cost = 0`.

* If `l > r` → invalid → also `cost = 0`.

It’s all about computing small ranges first and using them to build larger ones

<span style="color:yellow">**Why Interval DP (len-based loop)?**</span>

<span style="color:red">What we’re trying to do is:</span>

1. Solve all ranges of size 1 (like `[1,1]`, `[2,2]`...) → `cost = 0`.

2. Use those to solve ranges of size 2 (like `[1,2]`, `[2,3]`...)

3. Then ranges of size `3`, `4`, ... up to size `n`.

That’s where len comes in.
We start with smallest range `(len = 1) `and go up to n.


```cpp
class BottomUp{
public:
    int tabulation(int n){
        vector<vector<int>> dp(n+2, vector<int>(n+2, 0)) ;

        for(int delta = 1 ; delta <= (n-1) ; ++delta){            
            for(int low = 1 ; (low + delta) <= n ; ++low){
                int high = low + delta ;
                dp[low][high] = INT_MAX ;
                for(int x = low ; x <= high ; ++x){
                    int cost = x + max(dp[low][x-1], dp[x+1][high]) ;
                    dp[low][high] = min(dp[low][high], cost) ; 
                }
            }
        }
        return dp[1][n] ;
    }

    int getMoneyAmount(int n) {
        return tabulation(n) ;
    }
};
```

> Time Complexity = O(N<sup>3</sup>)

> Space Complexity = O(N<sup>2</sup>)

---

* Bottom Up Approach -- Optimized

```cpp
class BottomUp{
// Can't be optimized
};
```

> Time Complexity = O()

> Space Complexity = O()
