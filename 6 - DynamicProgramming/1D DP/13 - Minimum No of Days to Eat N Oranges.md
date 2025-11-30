### Leetcode - 1553 - [Minimum No of Days to Eat N Oranges](https://leetcode.com/problems/minimum-number-of-days-to-eat-n-oranges/description/)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
public:
    int solveWithoutMemo(int n){
        if(n <= 1){
            return n ;
        }

        int minDaystoEat = solveWithoutMemo(n-1) ;

        if(n%3 == 0){
            minDaystoEat = min(minDaystoEat, solveWithoutMemo(n - (2*(n/3)))) ;
        }
        else if(n%2 == 0){
            minDaystoEat = min(minDaystoEat, solveWithoutMemo(n/2)) ;
        }
        
        return (minDaystoEat + 1) ;
    }

    int minDays(int n) {
        return solveWithoutMemo(n) ;
    }    
}
```

> Time Complexity = O(3<sup>N</sup>)

> Space Complexity = O(3*N) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
public:
    int solveWithMemo(int n, vector<int>& dp){
        if(n <= 1){
            return n ;
        }

        if(dp[n] != -1){
            return dp[n] ; 
        }

        int minDaystoEat = solveWithMemo(n-1, dp) ;

        if(n%3 == 0){
            minDaystoEat = min(minDaystoEat, solveWithMemo(n - (2*(n/3)), dp)) ;
        }
        else if(n%2 == 0){
            minDaystoEat = min(minDaystoEat, solveWithMemo(n/2, dp)) ;
        }

        return dp[n] = (minDaystoEat + 1) ;
    }

    int minDays(int n) {
        vector<int> dp(n+1, -1) ;
        return solveWithMemo(n, dp) ;
    }    
}
```

> Time Complexity = O(3*N)
>> This above memoization solution throws runtime error for `n` = `0`
>> #### Why Runtime Error Happens
>> 1. Stack Overflow (too deep recursion):
>> * The function `solveWithMemo(n - 1, dp)` is always called before the divisibility checks.
>> * So for large n (like 9 million), recursion stack goes millions of calls deep before any memoization can help.
>> * The system call stack can’t handle that → runtime error.
>> #### Example:
>> * For `n` = `9209408`, first call is `solveWithMemo(9209408)`
>> * Then `solveWithMemo(9209407)`, then `9209406`, … → huge recursion chain before any base case.
>> 2. Inefficient condition order:
>> * Check divisibility after `solveWithMemo(n-1, dp)`, so we’re not taking advantage of the faster divisibility paths early.
>> 3. Memory-heavy dp array:
>> * Although it fits, it’s not scalable for even slightly bigger values (say 10<sup>8</sup> would crash immediately).

> Space Complexity = O(4*N) -- Recursion Stack + Vector

#### Correct Approact - Memoization

```cpp
class TopDown{
public:
    int solveWithMemo(int n, unordered_map<int, int>& dp){
        if(n <= 1){
            return n ;
        }
        if(dp.count(n)){
            return dp[n] ; 
        }

        int by3 = n%3 + solveWithMemo(n/3, dp) ;  // eat remainder + 2/3

        int by2 = n%2 + solveWithMemo(n/2, dp) ;  // eat remainder + half

        return dp[n] = min(by2, by3) + 1 ;
    }

    int minDays(int n) {
        unordered_map<int, int> dp;
        return solveWithMemo(n, dp) ;
    }    
}
```
> Time Complexity = O(2*N)

> Space Complexity = O(3*N)
---

* Bottom Up Approach -- With 1D table

```cpp
class BottomUp{
public:
    int solveWith1DTable(int n){
        vector<int> dp(n+1, INT_MAX);
        dp[0] = 0 ;
        dp[1] = 1 ;
        for(int i  = 2 ; i <= n ; ++i){
            dp[i] = dp[i-1] + 1 ; // if eat 1 orange
            if(i%2 == 0){
                dp[i] = min(dp[i], dp[i/2] + 1) ;
            }
            if(i%3 == 0){
                dp[i] = min(dp[i], dp[i- 2*(i/3)] + 1) ;
            } 
        }
        return dp[n] ;
    }

    int minDays(int n) {
        return solveWith1DTable(n) ;
    }
}
```
> Time Complexity = O(1*N)
>> Throws `TLE` b/c of given contraints.<br>
>> `n` can be up to 10<sup>7</sup> or more, so you can’t fill an array up to n directly (too large).
That’s why this problem is usually solved top-down with memoization and pruning.

> Space Complexity = O(1*N)

---

* Bottom Up Approach -- Without 1D table

```cpp
class bottomUp{
// Can't be further optimized
}
```

> Time Complexity = O()

> Space Complexity = O()