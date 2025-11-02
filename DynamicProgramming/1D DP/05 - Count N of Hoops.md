### GFG - [Count No of Hoops](https://www.geeksforgeeks.org/problems/count-number-of-hops-1587115620/1)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
    public:
    // Function to count the number of ways in which frog can reach the top.
    int solveWithoutMemo(int n){
        if(n == 0){
            return 1 ;
        }
        if(n < 0){
            return 0 ;
        }
        
        int jump1Step = solveWithoutMemo(n-1) ;
        int jump2Step = solveWithoutMemo(n-2) ;
        int jump3Step = solveWithoutMemo(n-3) ;
        
        return (jump1Step + jump2Step + jump3Step) ;
    }
    
    int countWays(int n) {
        return solveWithoutMemo(n) ;
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
    // Function to count the number of ways in which frog can reach the top.
    int solveWithMemo(int n, vector<int>& dp){
        if(n == 0){
            return 1 ;
        }
        if(n < 0){
            return 0 ;
        }
        
        if(dp[n] != -1){
            return dp[n] ;
        }
        
        int jump1Step = solveWithMemo(n-1, dp) ;
        int jump2Step = solveWithMemo(n-2, dp) ;
        int jump3Step = solveWithMemo(n-3, dp) ;
        
        return dp[n] = (jump1Step + jump2Step + jump3Step) ;
    }
    
    int countWays(int n) {
        vector<int> dp(n+1, -1) ;
        return solveWithMemo(n, dp) ;
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
    // Function to count the number of ways in which frog can reach the top.
    int solveWith1DTable(int n){
        vector<int> dp(n+1, -1) ;
        dp[0] = 1 ;
        
        for(int i = 1 ; i <= n ; ++i){
            int jump1Step = dp[i-1] ;
            int jump2Step = ((i-2) >= 0) ? dp[i-2] : 0 ;
            int jump3Step = ((i-3) >= 0) ? dp[i-3] : 0 ;
            dp[i] = jump1Step + jump2Step + jump3Step ;
        }
        
        return dp[n] ;
    }
    
    int countWays(int n) {
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
    // Function to count the number of ways in which frog can reach the top.
    int solveWithoutTable(int n){
        int jump1Step = 1 ;
        int jump2Step = 0 ;
        int jump3Step = 0 ;
        int numWays = 0 ;
        
        for(int i = 1 ; i <= n ; ++i){
            numWays = (jump1Step + jump2Step + jump3Step) ;
            jump3Step = jump2Step ;
            jump2Step = jump1Step ;
            jump1Step = numWays ;
        }
        
        return numWays ;
    }
    
    int countWays(int n) {
        return solveWithoutTable(n) ;
    }
}
```

> Time Complexity = O(1*N)

> Space Complexity = O(1)