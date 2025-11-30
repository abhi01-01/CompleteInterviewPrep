### Leetcode - 279 - [Perfect Squares](https://leetcode.com/problems/perfect-squares/description/)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
public:
    int solveWithoutMemo(int n){
        if(n == 0){
            return 0 ;
        }

        int minSquares = INT_MAX ;

        for(int i = 1 ; i*i <= n ; ++i){
            int nextSquare = solveWithoutMemo(n-i*i) ;
            if(nextSquare != INT_MAX){
                minSquares = min(minSquares, nextSquare + 1) ;
            }
        }
        return minSquares ;
    }

    int numSquares(int n) {
        return solveWithoutMemo(n) ;
    }    
};
```

> Time Complexity = O(√N<sup>N</sup>)

> Space Complexity = O(N) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
public:
    int solveWithMemo(int n, vector<int>& dp){
        if(n == 0){
            return 0 ;
        }

        if(dp[n] != -1){
            return dp[n] ;
        }

        int minSquares = INT_MAX ;

        for(int i = 1 ; i*i <= n ; ++i){
            int nextSquare = solveWithMemo(n-i*i, dp) ;
            if(nextSquare != INT_MAX){
                minSquares = min(minSquares, nextSquare + 1) ;
            }
        }
        return dp[n] = minSquares ;
    }

    int numSquares(int n) {
        vector<int> dp(n+1, -1) ;
        return solveWithMemo(n, dp) ;
    }    
};
```

> Time Complexity = O(√N*N)

> Space Complexity = O(2*N) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- With 1D table

```cpp
class BottomUp{
public:
    int solveWith1Dtable(int n){
        vector<int> dp(n+1, -1) ;
        dp[0] = 0 ;

        for(int j = 1 ; j <= n ; ++j){
            int minSquares = INT_MAX ;
            for(int i = 1 ; i*i <= j ; ++i){
                int nextSquare = ((j-i*i) >= 0) ? dp[j-i*i] : INT_MAX ;
                if(nextSquare != INT_MAX){
                    minSquares = min(minSquares, nextSquare + 1) ;
                }
            }
            dp[j] = minSquares ;
        }
        return dp[n] ;
    }

    int numSquares(int n) {
        return solveWith1Dtable(n) ;
    }
};
```

> Time Complexity = O(√N*N)

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