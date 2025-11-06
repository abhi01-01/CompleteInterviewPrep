### Leetcode - 790 - [Domino and Tromino Tiling](https://leetcode.com/problems/domino-and-tromino-tiling/description/)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
public:
    int mod = 1e9+7 ; 
    int solveWithoutMemo(int n){
        if(n == 1) return 1 ;
        else if(n == 2) return 2 ;
        else if(n == 3) return 5 ;

        int totWays = 0 ;

        totWays += (2*solveWithoutMemo(n-1)%mod + solveWithoutMemo(n-3)%mod)%mod ;

        return totWays ;
    }

    int numTilings(int n) {
        return solveWithoutMemo(n) ;
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
    int mod = 1e9+7 ; 
    int solveWithMemo(int n, vector<int>& dp){
        if(n == 1) return 1 ;
        else if(n == 2) return 2 ;
        else if(n == 3) return 5 ;

        if(dp[n] != -1){
            return dp[n] ;
        }

        int totWays = 0 ;

        totWays = (2*solveWithMemo(n-1, dp)%mod + solveWithMemo(n-3, dp)%mod)%mod ;

        return dp[n] = totWays ;
    }

    int numTilings(int n) {
        vector<int> dp(n+1, -1) ;
        return solveWithMemo(n, dp) ;
    }    
};
```

> Time Complexity = O(2*N)

> Space Complexity = O(2*N) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- With 1D table

```cpp
class BottomUp{
public:
    int mod = 1e9+7 ; 
    int solveWith1Dtable(int n){
        vector<int> dp(n+1, -1) ;
        dp[0] = 0, dp[1] = 1, dp[2] = 2, dp[3] = 5 ;

        for(int idx = 4 ; idx <= n ; ++idx){
            dp[idx] = (2*dp[idx-1]%mod + dp[idx-3]%mod)%mod ;
        }
        return dp[n] ;
    }

    int numTilings(int n) {
        if(n == 1) return 1 ;
        else if(n == 2) return 2 ;
        return solveWith1Dtable(n) ;
    }
};
```

> Time Complexity = O(1*N)

> Space Complexity = O(N)

---

* Bottom Up Approach -- Without 1D table

```cpp
class BottomUp{
public:
    int mod = 1e9+7 ; 
    int solveWithoutTable(int n){
        int dpAt1 = 1, dpAt2 = 2, dpAt3 = 5 ;

        int totWaysAtn = 0 ;
        for(int idx = 4 ; idx <= n ; ++idx){
            totWaysAtn = (2*dpAt3 % mod + dpAt1 % mod)%mod ;
            dpAt1 = dpAt2 ;
            dpAt2 = dpAt3 ;
            dpAt3 = totWaysAtn ;
        }
        return totWaysAtn ;
    }

    int numTilings(int n) {
        if(n == 1) return 1 ;
        else if(n == 2) return 2 ;
        else if(n == 3) return 5 ;
        return solveWithoutTable(n) ;
    }
};
```

> Time Complexity = O(N)

> Space Complexity = O(1)