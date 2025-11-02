### Leetcode - 70 - [Climbing Stairs](https://leetcode.com/problems/climbing-stairs/description/)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
public:
    int solveWihoutMemo(int n){
        // stepped at nth step, it's way
        if(n == 0){
            return 1 ;
        }
        // overreached
        if(n < 0){
            return 0 ;
        }

        int climb1Step = solveWihoutMemo(n-1) ;
        int climb2Step = solveWihoutMemo(n-2) ;

        return (climb1Step + climb2Step) ;
    }
    
    int climbStairs(int n) {
        return solveWihoutMemo(n) ; 
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
    int solveWithMemo(int n, vector<int>& dp){
        // stepped at nth step, it's way
        if(n == 0){
            return 1 ;
        }
        // overreached
        if(n < 0){
            return 0 ;
        }

        if(dp[n] != -1){
            return dp[n] ;
        }

        int climb1Step = solveWithMemo(n-1, dp) ;
        int climb2Step = solveWithMemo(n-2, dp) ;

        return dp[n] = (climb1Step + climb2Step) ;
    }

    int climbStairs(int n) {
        vector<int> dp(n+1, -1) ;
        return solveWithMemo(n, dp) ; 
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
    int solveWith1DTable(int n){
        vector<int> dp(n+1, -1) ;
        // stepped at nth step, it's way
        dp[0] = 1 ; 
        
        for(int i = 1 ; i <= n ; ++i){
            int climb1Step = dp[i-1] ;
            int climb2Step = ((i-2) >= 0) ? dp[i-2] : 0 ;
            dp[i] = (climb1Step + climb2Step) ;

        }

        return dp[n] ;
    }

    int climbStairs(int n) {
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
    int solveWithoutable(int n){
        int climb1Step = 1 ; 
        int climb2Step = 0 ;
        int numWays = 0 ; 
        
        for(int i = 1 ; i <= n ; ++i){
            numWays = (climb1Step + climb2Step) ;
            climb2Step = climb1Step ;
            climb1Step = numWays ;

        }

        return numWays;
    }

    int climbStairs(int n) {
        return solveWithoutable(n) ; 
    }
}
```

> Time Complexity = O(1*N)

> Space Complexity = O(1)