### GFG - [Climbing Stairs II](https://leetcode.com/problems/climbing-stairs-ii/)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
public:
    int solveWithoutMemo(vector<int>& costs, int currIdx){
        int n = costs.size() ;
        if(currIdx == (n-1)){
            return 0 ;
        }

        int jump1Step = ((currIdx+1) < n) ? (1 + costs[currIdx+1] + solveWithoutMemo(costs, currIdx+1)) : INT_MAX ;
        int jump2Step = ((currIdx+2) < n) ? (4 + costs[currIdx+2] + solveWithoutMemo(costs, currIdx+2)) : INT_MAX ;
        int jump3Step = ((currIdx+3) < n) ? (9 + costs[currIdx+3] + solveWithoutMemo(costs, currIdx+3)) : INT_MAX ;

        int minCost = min({jump1Step, jump2Step, jump3Step}) ;

        return minCost ; 
    }

    int climbStairs(int n, vector<int>& costs) {
        int start = -1 ;
        return solveWithoutMemo(costs, start) ;
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
    int solveWithMemo(vector<int>& costs, int currIdx, vector<int>& dp){
        int n = costs.size() ;
        if(currIdx == (n-1)){
            return 0 ;
        }

        if(dp[currIdx+1] != -1){
            // since storing curridx as in dp[currIdx+1], that's why returning so
            return dp[currIdx+1] ;
        }

        int jump1Step = ((currIdx+1) < n) ? (1 + costs[currIdx+1] + solveWithMemo(costs, currIdx+1, dp)) : INT_MAX ;
        int jump2Step = ((currIdx+2) < n) ? (4 + costs[currIdx+2] + solveWithMemo(costs, currIdx+2, dp)) : INT_MAX ;
        int jump3Step = ((currIdx+3) < n) ? (9 + costs[currIdx+3] + solveWithMemo(costs, currIdx+3, dp)) : INT_MAX ;

        // Since starting from idx -1, so storing idx -1 value at idx 0 in dp arr
        return dp[currIdx+1] = min({jump1Step, jump2Step, jump3Step}) ; 
    }

    int climbStairs(int n, vector<int>& costs) {
        vector<int> dp(n+1, -1) ;
        int start = -1 ;
        return solveWithMemo(costs, start, dp) ;
    }    
}
```

> Time Complexity = O(3*N)

> Space Complexity = O(4*N) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- With 1D table

```cpp
class BottomUp{
    int solveWith1DTable(vector<int>& costs){
        int n = costs.size() ;
        // dp[i] represents: min cost to reach the end when currently at index (i-1)
        // dp[0] corresponds to currIdx = -1
        vector<int> dp(n+1, -1) ;
        dp[n] = 0 ;

        for(int currIdx = (n-2) ; currIdx >= -1 ; --currIdx){
            int i = currIdx + 1 ; 
            int jump1Step = ((currIdx+1) < n) ? (1 + costs[currIdx+1] + dp[i+1]) : INT_MAX ;
            int jump2Step = ((currIdx+2) < n) ? (4 + costs[currIdx+2] + dp[i+2]) : INT_MAX ;
            int jump3Step = ((currIdx+3) < n) ? (9 + costs[currIdx+3] + dp[i+3]) : INT_MAX ;
            int minCost = min({jump1Step, jump2Step, jump3Step}) ;
            // Since starting from idx -1, so storing idx -1 value at idx 0 in dp arr
            dp[currIdx+1] = minCost ; 
        }
        return dp[0] ;   // This is result for currIdx = -1
    }

    int climbStairs(int n, vector<int>& costs) {
        return solveWith1DTable(costs) ;
    }
}
```

> Time Complexity = O(1*N)

> Space Complexity = O(1*N)

---

* Bottom Up Approach -- Without 1D table

```cpp
class BottomUp{
public:
    int solveWithoutTable(vector<int>& costs){
        int n = costs.size() ;
        // dp[i] represents: min cost to reach the end when currently at index (i-1)
        // dp[0] corresponds to currIdx = -1
        int dpiPlus1 = 0, dpiPlus2 = 0, dpiPlus3 = 0, minCost = 0 ;

        for(int currIdx = (n-2) ; currIdx >= -1 ; --currIdx){
            int i = currIdx + 1 ; 
            int jump1Step = ((currIdx+1) < n) ? (1 + costs[currIdx+1] + dpiPlus1) : INT_MAX ;
            int jump2Step = ((currIdx+2) < n) ? (4 + costs[currIdx+2] + dpiPlus2) : INT_MAX ;
            int jump3Step = ((currIdx+3) < n) ? (9 + costs[currIdx+3] + dpiPlus3) : INT_MAX ;
            // Since starting from idx -1, so storing idx -1 value at idx 0 in dp arr
            minCost = min({jump1Step, jump2Step, jump3Step}) ;
            dpiPlus3 = dpiPlus2 ;
            dpiPlus2 = dpiPlus1 ;
            dpiPlus1 = minCost ;
        }
        return minCost ;   // This is result for currIdx = -1
    }

    int climbStairs(int n, vector<int>& costs) {
        return solveWithoutTable(costs) ;
    }
}
```

> Time Complexity = O(1*N)

> Space Complexity = O(1)