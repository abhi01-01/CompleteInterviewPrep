## Leetcode - 509 - [Fibonacci Number](https://leetcode.com/problems/fibonacci-number/)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
    public:
    int solveWithoutMemo(int n){
        if(n<2){
            return n ;
        }
        int prevNum1 = solveWithoutMemo(n-1) ;
        int prevNum2 = solveWithoutMemo(n-2) ;

        return prevNum1 + prevNum2 ;
    }
    int nthFibonacci(int n){
        return solveWithoutMemo(n) ;
    }
}
```

> Time Complexity = O(2<sup>N</sup>)

> Space Complexity = O(N) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
    public :
    int solveWithMemo(int n, vector<int>& dp){
        if(n < 2){
            return n ;
        }

        if(dp[n] != -1){
            return dp[n] ;
        }

        int prevNum1 = solveWithMemo(n-1, dp) ;
        int prevNum2 = solveWithMemo(n-2, dp) ;

        return dp[n] = prevNum1 + prevNum2 ;
    }

    int nthFibonacci(int n){
        vector<int> dp(n+1, -1) ;
        return solveWithMemo(n,  dp) ;
    }
}
```

> Time Complexity = O(2*N)

> Space Complexity = O(2*N) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- With 1D table

```cpp
class BottomUp{
    public :

    int solveWith1DTable(int n){
        vector<int> dp(n+1, -1) ;

        // Initializing the base case

        dp[0] = 0 ;  // n = 0 then return 0
        dp[1] = 1 ;  // n = 1 then return 1

        for(int i = 2 ; i <= n ; ++i){
            int prevNum1 = dp[i-1] ;
            int prevNum2 = dp[i-2] ;
            dp[i] = prevNum1 + prevNum2 ;
        }
        return dp[n] ;
    }
    int nthFibomacci(int n){
        return solveWith1DTable(n) ;
    }
}
```

> Time Complexity = O(N)

> Space Complexity = O(N)

---

* Bottom Up Approach -- Without 1D table

```cpp
class bottomUp{
    public :

    int solveWithoutTable(int n){

        // initializing base casees
        int prevNum2 = 0 ;   // n = 0, return 0
        int prevNum1 = 1 ;   // n = 1, return 1
        int currNum = 0 ;

        for(int i = 2 ; i <= n ; ++i){
            currNum = prevNum1 + prevNum2 ;
            prevNum2 = prevNum1 ;
            prevNum1 = currNum ;
        }
        return currNum ;
    }

    int nthFibonacci(int n){
        if(n < 2){
            return n ;
        }

        return solveWithoutTable(n) ;
    }

}
```

> Time Complexity = O(N)

> Space Complexity = O(1)