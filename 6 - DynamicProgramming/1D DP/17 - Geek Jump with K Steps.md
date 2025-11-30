### GFG - [Geek Jump with K Steps](https://www.geeksforgeeks.org/problems/minimal-cost/1)

* TopDown Approach - Without Memoization

```cpp
class TopDown{
  public:
    int solveWithoutMemo(int k, vector<int>& arr, int start){
        int n = arr.size() ;
        if(start == n-1){
            return 0 ;
        }
        
        int minCost = INT_MAX ;
        
        for(int i = 1 ; i <= k and (start+i) < n ; ++i ){
            int jumpCost = abs(arr[start+i] - arr[start]) ;
            int nextCost = solveWithoutMemo(k, arr, start+i) ;
            minCost = min(minCost, jumpCost + nextCost) ;
        }
        return minCost ;
    }
    
    int minimizeCost(int k, vector<int>& arr) {
        // Code here
        int start = 0 ;
        return solveWithoutMemo(k, arr, start) ;
    }    
}
```

> Time Complexity = O(K<sup>N</sup>)

> Space Complexity = O(N*K) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
  public:
    int solveWithMemo(int k, vector<int>& arr, int currIdx, vector<int>& dp){
        int n = arr.size() ;
        if(currIdx == n-1){
            return 0 ;
        }
        int minCost = INT_MAX ;
        
        if(dp[currIdx] != -1){
            return dp[currIdx] ;
        }
        
        for(int i = 1 ; i <= k and (currIdx+i) < n ; ++i ){
            int jumpCost = abs(arr[currIdx+i] - arr[currIdx]) ;
            int nextCost = solveWithMemo(k, arr, currIdx+i, dp) ;
            minCost = min(minCost, jumpCost + nextCost) ;
        }
        return dp[currIdx] = minCost ;
    }
    
    int minimizeCost(int k, vector<int>& arr) {
        // Code here
        int start = 0, n = arr.size() ;
        vector<int> dp(n, -1) ;
        return solveWithMemo(k, arr, start, dp) ;
    }    
}
```

> Time Complexity = O(K*N)

> Space Complexity = O(K*N + N) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- With 1D table

```cpp
class BottomUp{
  public:
    int solveWith1DTable(int k, vector<int>& arr){
        int n = arr.size() ;
        vector<int> dp(n, -1) ;
        
        dp[n-1] = 0 ;
 
        for(int currIdx = (n-2) ; currIdx >= 0 ; --currIdx){
            int minCost = INT_MAX ;
            for(int i = 1 ; i <= k and (currIdx+i) < n ; ++i ){
                int jumpCost = abs(arr[currIdx+i] - arr[currIdx]) ;
                int nextCost = dp[currIdx+i] ;
                minCost = min(minCost, jumpCost + nextCost) ;
                dp[currIdx] = minCost ;
            }
        }
        return dp[0] ;
    }
    
    int minimizeCost(int k, vector<int>& arr) {
        // Code here
        return solveWith1DTable(k, arr) ;
    }
}
```

> Time Complexity = O(K*N)

> Space Complexity = O(N)

---

* Bottom Up Approach -- Without 1D table

```cpp
class bottomUp{
// Can't be optimized further
}
```

> Time Complexity = O()

> Space Complexity = O()