### GFG - [Maximize the Cut Segments](https://www.geeksforgeeks.org/problems/cutted-segments1642/1)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
  public:
    // Function to find the maximum number of cuts.
    int solveWithoutMemo(int n, int x, int y, int z){
        // Edge Case : if you have cut the whole line segment, return 0
        if(n == 0){
            return 0 ;
        }
        // Edge Case : if you can't cut whole line segment, return INT_MIN as indicator
        if(n < 0){
            return INT_MIN ;
        }
        
        int cutLengthX = solveWithoutMemo(n-x, x, y, z) ;
        int cutLengthY = solveWithoutMemo(n-y, x, y, z) ;
        int cutLengthZ = solveWithoutMemo(n-z, x, y, z) ;
        
        int maxCuts = max({cutLengthX, cutLengthY, cutLengthZ}) ;
        return (maxCuts == INT_MIN) ? 0 : (maxCuts+1) ;
    }
    int maximizeTheCuts(int n, int x, int y, int z) {
        // Your code here
        return solveWithoutMemo(n, x, y, z) ;
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
    // Function to find the maximum number of cuts.
    int solveWithMemo(int n, int x, int y, int z, vector<int>& dp){
        // Edge Case : if you have cut the whole line segment, return 0
        if(n == 0){
            return 0 ;
        }
        // Edge Case : if you can't cut whole line segment, return INT_MIN as indicator
        if(n < 0){
            return INT_MIN ;
        }
        
        if(dp[n] != -1){
            return dp[n] ;
        }
        
        int cutLengthX = solveWithMemo(n-x, x, y, z, dp) ;
        int cutLengthY = solveWithMemo(n-y, x, y, z, dp) ;
        int cutLengthZ = solveWithMemo(n-z, x, y, z, dp) ;
        
        int maxCuts = max({cutLengthX, cutLengthY, cutLengthZ}) ;
        dp[n] = (maxCuts == INT_MIN) ? INT_MIN : (maxCuts+1) ;
        return dp[n] ;
    }
    int maximizeTheCuts(int n, int x, int y, int z) {
        // Your code here
        vector<int> dp(n+1, -1) ;
        int ans = solveWithMemo(n, x, y, z, dp) ;
        return (ans == INT_MIN) ? 0 : ans ;
    }    
}
```

> Time Complexity = O(3*N)

> Space Complexity = O(4*N) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- With 1D table

```cpp
class BottomUp{
  public:
    // Function to find the maximum number of cuts.
    int solveWith1DTable(int n, int x, int y, int z){
        // Edge Case : if you have cut the whole line segment, return 0
        vector<int> dp(n+1, -1) ;
        dp[0] = 0 ;
        
        for(int i = 1 ; i <= n ; ++i){
            // Edge Case : if you can't cut whole line segment, return INT_MIN as indicator
            int cutLengthX = ((i-x) >= 0) ? dp[i-x] : INT_MIN ;
            int cutLengthY = ((i-y) >= 0) ? dp[i-y] : INT_MIN ;
            int cutLengthZ = ((i-z) >= 0) ? dp[i-z] : INT_MIN ;
            int maxCuts = max({cutLengthX, cutLengthY, cutLengthZ}) ;
            dp[i] = (maxCuts == INT_MIN) ? INT_MIN : (maxCuts+1) ;
        }
        return (dp[n] == INT_MIN) ? 0 : dp[n] ;
    }
    int maximizeTheCuts(int n, int x, int y, int z) {
        // Your code here
        return solveWith1DTable(n, x, y, z) ;
    }
}
```

> Time Complexity = O(1*N)

> Space Complexity = O(1*N)

---

* Bottom Up Approach -- Without 1D table

```cpp
class bottomUp{
// Can't be optimized further 
}
```

> Time Complexity = O()

> Space Complexity = O()