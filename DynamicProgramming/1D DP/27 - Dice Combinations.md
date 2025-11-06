### CSES - [Dice Combinations](https://cses.fi/problemset/task/1633/)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
    public :
    int mod = 1e9+7 ;
    int solveWithoutMemo(int n){
        if(n == 0){
            return 1 ;
        }
        int count = 0 ;

        for(int dice = 1 ; dice <= 6 and dice <= n >; ++dice ){
            count = (count%mod + solveWithoutMemo(n-dice)%mod)%mod ;
        }

        return count ;
    }

    int constructSumN(int n){
        return solveWithoutMemo(n) ;
    }
};
```

> Time Complexity =O(6<sup>N</sup>)

> Space Complexity = O(N) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
    public :
    int mod = 1e9+7 ;
    int solveWithMemo(int n, vector<int>& dp){
        if(n == 0){
            return 1 ;
        }
        if(dp[n] != -1){
            return dp[n] ;
        }
        int count = 0 ;
        
        for(int dice = 1 ; dice <= 6 and dice <= n ; ++dice ){
            count = (count%mod + solveWithMemo(n-dice, dp)%mod)%mod ;
        }

        return dp[n] = count ;
    }

    int constructSumN(int n){
        vector<int> dp(n+1, -1) ;
        return solveWithMemo(n, dp) ;
    }
};
```

> Time Complexity = O(6*N)

> Space Complexity = O(2*N) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- With 1D table

```cpp
class BottomUp{
    public :
    int mod = 1e9+7 ;
    int solveWith1Dtable(int n){
        vector<int> dp(n+1, -1) ;
        dp[0] = 1 ;
        for(int idx = 1 ; idx <= n ; ++idx){
            int count = 0 ;
            
            for(int dice = 1 ; (dice <= 6) and (dice <= idx) ; ++dice ){
                count = (count%mod + dp[idx-dice]%mod)%mod ;
            }
            dp[idx] = count ;
        }

        return dp[n] ;
    }

    int constructSumN(int n){
        return solveWith1Dtable(n) ;
    }
};
```

> Time Complexity = O(6*N)

> Space Complexity = O(N)

---

* Bottom Up Approach -- Without 1D table

```cpp
class BottomUp{
// Can't be optimized further
};
```

> Time Complexity = O()

> Space Complexity = O()