### Leetcode - 1137 - [N-th Tribonacci Number](https://leetcode.com/problems/n-th-tribonacci-number/description/)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
public:
    int solveWithoutMemo(int n){
        if(n < 3){
            return (n==0) ? 0 : 1 ;
        }

        int prevNum1 = solveWithoutMemo(n-1) ;
        int prevNum2 = solveWithoutMemo(n-2) ;
        int prevNum3 = solveWithoutMemo(n-3) ;

        return prevNum1 + prevNum2 + prevNum3 ;
    }
    int tribonacci(int n) {
        return solveWithoutMemo(n) ;
    } 
}
```

> Time Complexity = O(3<sup>N</sup>)

> Space Complexity = O(1*N) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
    int solveWithMemo(int n, vector<int>& dp){
        if(n < 3){
            return (n==0) ? 0 : 1 ;
        }

        if(dp[n] != -1){
            return dp[n] ;
        }

        int prevNum1 = solveWithMemo(n-1, dp) ;
        int prevNum2 = solveWithMemo(n-2, dp) ;
        int prevNum3 = solveWithMemo(n-3, dp) ;

        return dp[n] = (prevNum1 + prevNum2 + prevNum3) ;
    }
    int tribonacci(int n) {
        vector<int> dp(n+1, -1) ;
        return solveWithMemo(n, dp) ;
    }   
}
```

> Time Complexity = O(3*N)

> Space Complexity = O(2*N) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- With 1D table

```cpp
class BottomUp{
public:
    int solveWith1Dtable(int n){
        vector<int> dp(n+1, -1) ;
        dp[0] = 0 ;
        dp[1] = 1 ;
        dp[2] = 1 ;

        for(int i = 3 ; i <= n ; ++i){
            dp[i] = dp[i-1] + dp[i-2] + dp[i-3] ;
        }

        return dp[n] ;
    }
    int tribonacci(int n) {
        return solveWith1Dtable(n) ;
    }
}
```

> Time Complexity = O(1*n)

> Space Complexity = O(1*N)

---

* Bottom Up Approach -- Without 1D table

```cpp
class bottomUp{
    public:
    int solveWithouttable(int n){
        int prevNum3 = 0 ;
        int prevNum2 = 1 ;
        int prevNum1 = 1 ;
        int currNum = (n == 0) ? 0 : 1 ;

        for(int i = 3 ; i <= n ; ++i){
            currNum = (prevNum1 + prevNum2 + prevNum3) ;
            prevNum3 = prevNum2 ;
            prevNum2 = prevNum1 ;
            prevNum1 = currNum ;
        }

        return currNum ;
    }
    int tribonacci(int n) {
        return solveWithouttable(n) ;
    }
}
```

> Time Complexity = O(1*N)

> Space Complexity = O(1)
