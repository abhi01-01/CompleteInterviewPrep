### GFG - [Frog Jump](https://www.geeksforgeeks.org/problems/geek-jump/1)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
  public:
    int solveWithoutMemo(vector<int>& height, int currStair){
        int n = height.size() ;
        if(currStair == (n-1)){
            return 0 ;
        }
        
        int jump1Stair = abs(height[currStair+1] - height[currStair]) + solveWithoutMemo(height, currStair+1) ;
        int jump2Stair = ((currStair+2) < n) ? abs(height[currStair+2] - height[currStair]) + solveWithoutMemo(height, currStair+2) : INT_MAX ;
        
        int minCost = min(jump1Stair, jump2Stair) ;
        
        return minCost ;
    }
    
    int minCost(vector<int>& height) {
        // Code here
        int start = 0 ;
        return solveWithoutMemo(height, start) ;
    } 
};
```

> Time Complexity = O(2<sup>N</sup>)

> Space Complexity = O(2*N) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
  public:
    int solveWithMemo(vector<int>& height, int currStair, vector<int>& dp){
        int n = height.size() ;
        if(currStair == (n-1)){
            return 0 ;
        }
        
        if(dp[currStair] != -1){
            return dp[currStair] ;
        }
        
        int jump1Stair = abs(height[currStair+1] - height[currStair]) + solveWithMemo(height, currStair+1, dp) ;
        int jump2Stair = ((currStair+2) < n) ? abs(height[currStair+2] - height[currStair]) + solveWithMemo(height, currStair+2, dp) : INT_MAX ;
        
        return dp[currStair] = min(jump1Stair, jump2Stair) ;
    }
    
    int minCost(vector<int>& height) {
        // Code here
        int start = 0, n = height.size() ;
        vector<int> dp(n+1, -1) ;
        return solveWithMemo(height, start, dp) ;
    }    
}
```

> Time Complexity = O(2*N)

> Space Complexity = O(3*N) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- With 1D table

```cpp
class BottomUp{
  public:
    int solveWith1DTable(vector<int>& height){
        int n = height.size() ;
        vector<int> dp(n, -1) ;
        dp[n-1] = 0 ;
        
        for(int currStair = (n-2) ; currStair >= 0 ; --currStair){
            int jump1Stair = abs(height[currStair+1] - height[currStair]) + dp[currStair+1] ;
            int jump2Stair = ((currStair+2) < n) ? abs(height[currStair+2] - height[currStair]) + dp[currStair+2] : INT_MAX ;
            dp[currStair] = min(jump1Stair, jump2Stair) ;
        }
        return dp[0] ;
    }
    
    int minCost(vector<int>& height) {
        // Code here
        return solveWith1DTable(height) ;
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
    int solveWithoutTable(vector<int>& height){
        int n = height.size() ;
        int currStairPlus1 = 0, currStairPlus2 = INT_MAX, minCost = 0 ;
        
        for(int currStair = (n-2) ; currStair >= 0 ; --currStair){
            int jump1Stair = abs(height[currStair+1] - height[currStair]) + currStairPlus1 ;
            int jump2Stair = ((currStair+2) < n) ? abs(height[currStair+2] - height[currStair]) + currStairPlus2 : INT_MAX ;
            minCost = min(jump1Stair, jump2Stair) ;
            currStairPlus2 = currStairPlus1 ;
            currStairPlus1 = minCost ;
        }
        return currStairPlus1 ;
    }
    
    int minCost(vector<int>& height) {
        // Code here
        return solveWithoutTable(height) ;
    }
}
```

> Time Complexity = O(1*N)

> Space Complexity = O(1)