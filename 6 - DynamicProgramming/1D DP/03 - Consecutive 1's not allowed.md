### GFG - [Consecutive 1's not allowed](https://www.geeksforgeeks.org/problems/consecutive-1s-not-allowed1912/1)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
  public:
    // #define ll long long
    int solveWithoutMemo(int n){
        if(n < 3){
            return n+1 ;
     }
     
     int prevNum1 = solveWithoutMemo(n-1) ;
     int prevNum2 = solveWithoutMemo(n-2) ;
     
     return (prevNum1 + prevNum2) ;
    }
    
    int countStrings(int n) {
        return solveWithoutMemo(n) ;
    }
```

> Time Complexity = O(2<sup>N</sup>)

> Space Complexity = O(N) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
  public:
    // #define ll long long
    int solveWithMemo(int n, vector<int>& dp){
        if(n < 3){
            return n+1 ;
        }
        
        if(dp[n] != -1){
            return dp[n] ;
        }
     
        int prevNum1 = solveWithMemo(n-1, dp) ;
        int prevNum2 = solveWithMemo(n-2, dp) ;
     
        return (prevNum1 + prevNum2) ;
    }
    
    int countStrings(int n) {
        vector<int> dp(n+1, -1) ;
        return solveWithMemo(n, dp) ;  // The main task is to find the n + 1th number of the fibonacci sequence
    }   
}
```

> Time Complexity = O(2*N)

> Space Complexity = O(2*N) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- With 1D table

```cpp
class BottomUp{
  public:
    // #define ll long long
    int solveWith1DTable(int n){
        vector<int> dp(n+1, -1) ;
        
        // init the bases cases, n<3 return n+1
        dp[0] = 0 ;
        dp[1] = 2 ;
        dp[2] = 3 ;
        
        for(int i = 3 ; i <=n ; ++i){
            dp[i] = dp[i-1] + dp[i-2] ;
        }
        
        return dp[n] ;
    }
    int countStrings(int n) {
        return solveWith1DTable(n) ;
    }
}
```

> Time Complexity = O(1*N)

> Space Complexity = O(1*N)

---

* Bottom Up Approach -- Without 1D table

```cpp
class bottomUp{
  public:
    // #define ll long long
    int solveWithoutTable(int n){
        vector<int> dp(n+1, -1) ;
        
        // init the bases cases, n<3 return n+1
        // dp[0] = 0 ;
        int prevNum2 = 2 ;
        int prevNum1 = 3 ;
        int currNum = (n==1) ? 2 : 3 ;
        
        for(int i = 3 ; i <=n ; ++i){
            currNum = prevNum1 + prevNum2 ;
            prevNum2 = prevNum1 ;
            prevNum1 = currNum ;
        }
        
        return currNum ;
    }
    int countStrings(int n) {
        return solveWithoutTable(n) ;
    }
}
```

> Time Complexity = O(1*N)

> Space Complexity = O(1*N)