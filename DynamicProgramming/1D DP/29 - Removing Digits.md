### CSES - [Removing Digits](https://cses.fi/problemset/task/1637)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
    public :
    int solveWithoutMemo(int n){
       if(n == 0){
        return 0 ;
       }    
       int minSteps = INT_MAX ;
       int nCopy = n ;

       int maxDigit = 0 ;
       while(nCopy){
            maxDigit = max(maxDigit, nCopy%10) ;
            nCopy /= 10 ;
       } 

       int nextStep = solveWithoutMemo(n - maxDigit) ;
       minSteps = min(minSteps, nextStep+1) ;
       return minSteps ;
    }    

    int removeDigits(int n){
        return solveWithoutMemo(n) ;
    }
};
```

> Time Complexity = O(logN<sup>N</sup>)

> Space Complexity = O(N) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
public :
    int solveWithMemo(int n, vector<int>& dp){
       if(n == 0){
        return 0 ;
       }   
       if(dp[n] != -1){
        return dn[n] ;
       } 
       int minSteps = INT_MAX ;
       int nCopy = n ;

       int maxDigit = 0 ;
       while(nCopy){
            maxDigit = max(maxDigit, nCopy%10) ;
            nCopy /= 10 ;
       } 

       int nextStep = solveWithMemo(n - maxDigit, dp) ;
       minSteps = min(minSteps, nextStep+1) ;

       return dp[n] = minSteps ;
    }    

    int removeDigits(int n){
        vector<int> dp(n+1, -1) ;
        return solveWithMemo(n, dp) ;
    }    
};
```

> Time Complexity = O(N*logN)

> Space Complexity = O(2*N) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- With 1D table

```cpp
class BottomUp{
    public :
    int solveWith1Dtable(int n){
        vector<int> dp(n+1, -1) ;
        dp[0] = 0 ;

        for(int idx = 1 ; idx <= n ; ++idx){
            int minSteps = INT_MAX ;
            int nCopy = n ;
            int maxDigit = 0 ;
            while(nCopy){
                maxDigit = max(maxDigit, nCopy%10) ;
                nCopy /= 10 ;
            }
            int nextStep = dp[idx - maxDigit] ;
            minSteps = min(minSteps, nextStep + 1) ;
            dp[idx] = minSteps ;
        }
        return dp[n] ;
    }

    int removeDigits(int n){
        return solveWith1Dtable(n) ;
    }
};
```

> Time Complexity = O(N*logN)

> Space Complexity = O(N)

---

* Bottom Up Approach -- Without 1D table

```cpp
class BottomUp{
// Can't be optimized further
};
```

> Time Complexity = O()

> Space Complexity = O()