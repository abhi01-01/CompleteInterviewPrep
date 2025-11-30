### Leectcode - 746 - [Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs/description/)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
public:
    int solveWithoutMemo(vector<int>& cost, int n, int step){
        if(step >= n){
            return 0 ;
        }

        int climb1Step = solveWithoutMemo(cost, n, step+1) ;
        int climb2Step = solveWithoutMemo(cost, n, step+2) ;

        return cost[step] + min(climb1Step, climb2Step) ;
    }

    int minCostClimbingStairs(vector<int>& cost) {
        int n = cost.size() ;
        int startFrom0 = solveWithoutMemo(cost, n, 0) ;
        int startFrom1 = solveWithoutMemo(cost, n, 1) ;

        return min(startFrom0, startFrom1) ;
    }
}
```

> Time Complexity = O(2<sup>N</sup>)

> Space Complexity = O(2*N) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
public:
    int solveWithMemo(vector<int>& cost, int n, int step, vector<int>& dp){
        if(step >= n){
            return 0 ;
        }

        if(dp[step] != -1){
            return dp[step] ;
        }

        int climb1Step = solveWithMemo(cost, n, step+1, dp) ;
        int climb2Step = solveWithMemo(cost, n, step+2, dp) ;

        return dp[step] = cost[step] + min(climb1Step, climb2Step) ;
    }

    int minCostClimbingStairs(vector<int>& cost) {
        int n = cost.size() ;
        vector<int> dp1(n, -1), dp2(n, -1) ;
        int startFrom0 = solveWithMemo(cost, n, 0, dp1) ;
        int startFrom1 = solveWithMemo(cost, n, 1, dp2) ;

        return min(startFrom0, startFrom1) ;
    }    
}
```

> Time Complexity = O(2*N)

> Space Complexity = O(4*N) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- With 1D table

```cpp
class BottomUp{
public:
    int solveWith1DTable(vector<int>& cost){
        int n = cost.size() ;
        vector<int> dp(n, -1) ;
        dp[0] = cost[0], dp[1] = cost[1] ;

        if(n < 3){
            return min(cost[0], cost[1]) ;
        }

        for(int i = 2 ; i < n ; ++i){
            dp[i] = (min(dp[i-1], dp[i-2]) + cost[i]) ;
        }

        return min(dp[n-1], dp[n-2]) ;
    }

    int minCostClimbingStairs(vector<int>& cost) {
        return solveWith1DTable(cost) ;
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
    int solveWithoutTable(vector<int>& cost){
        int n = cost.size() ;
        int climb1Step = cost[1], climb2Step = cost[0] ;
        int currStep = 0 ;
        
        for(int i = 2 ; i < n ; ++i){
            currStep = (min(climb1Step, climb2Step) + cost[i]) ;
            climb2Step = climb1Step ;
            climb1Step = currStep ;
        }

        return min(climb1Step, climb2Step) ;
    }

    int minCostClimbingStairs(vector<int>& cost) {
        return solveWithoutTable(cost) ;
    }
}
```

> Time Complexity = O(1*N)

> Space Complexity = O(1*N)