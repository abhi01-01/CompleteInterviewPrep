### GFG - [Filling Bucket](https://www.geeksforgeeks.org/problems/filling-bucket0529/1)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
    public:

    int mod = 1e8 ;
    int solveWithoutMemo(int n){
      // Edge Case : if the bucket is overfilled, the it's not valid
      if(n<0){
          return 0 ;
      }
      // Edge case : if you have filled the whole bucket then you have 1 way 
      if(n==0){
          return 1 ;
      }
      
      int fill1litre = solveWithoutMemo(n-1)%mod ;
      int fill2litre = solveWithoutMemo(n-2)%mod ;
      
      return (fill1litre + fill2litre)%mod ;
    }
    int fillingBucket(int n) {
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
    int mod = 1e8 ;
    int solveWithMemo(int n, vector<int>& dp){
      // Edge Case : if the bucket is overfilled, the it's not valid
      if(n<0){
          return 0 ;
      }
      // Edge case : if you have filled the whole bucket then you have 1 way 
      if(n==0){
          return 1 ;
      }
      
      // if subproblem already solve, return it
      if(dp[n] != -1){
          return dp[n] ;
      }
      
      int fill1litre = solveWithMemo(n-1, dp)%mod ;
      int fill2litre = solveWithMemo(n-2, dp)%mod ;
      
      // store the subproblem result
      return dp[n] = (fill1litre%mod + fill2litre%mod)%mod ;
    }
    int fillingBucket(int n) {    
        vector<int> dp(n+1, -1) ;
        return solveWithMemo(n, dp) ;
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
    int MOD = 1e8 ;
    int solveWith1DTable(int n){
    vector<int> dp(n+1, -1) ;
    dp[0] = 1 ;  // Initializing the 1st edge case
      
    for(int i = 1 ; i <=n ; ++i){
        int fill1Litre = dp[i-1] ;
        int fill2Litre = (i-2) >= 0 ? dp[i-2] : 0 ;
        dp[i] = (fill1Litre + fill2Litre)%MOD ;
    }
    return dp[n] ;  
    }

    int fillingBucket(int n) {
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
  public:
  int MOD = 1e8 ;
  int solveWithoutTable(int n){
    int fill1Litre = 1 ;    // Init the 1st edge case
    int fill2Litre = 0 ;
    int numWays = 0 ;
      
    for(int i = 1 ; i <=n ; ++i){
        numWays = (fill1Litre%MOD + fill2Litre%MOD)%MOD ;
        fill2Litre = fill1Litre ;
        fill1Litre = numWays ;
    }
    return numWays ;  
  }
    int fillingBucket(int n) {
        return solveWithoutTable(n) ;
    }
}
```

> Time Complexity = O(N)

> Space Complexity = O(1)