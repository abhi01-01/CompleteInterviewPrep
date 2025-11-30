### Leetcode - 2466 - [Count Ways To Build Good Strings](https://leetcode.com/problems/count-ways-to-build-good-strings/description/)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
public:
    int lw, hi, ze, on ;
    int MOD = 1e9+7 ;
    int solveWithoutMemo(int strLen){
        if(strLen >hi){
            return 0 ;
        }
        int appendZero = solveWithoutMemo(strLen + ze) ;
        int appendOne = solveWithoutMemo(strLen + on) ;

        return (strLen >= lw) + (((appendZero % MOD) + (appendOne % MOD)) % MOD) ;
    }
    int countGoodStrings(int low, int high, int zero, int one) {
        lw = low, hi = high, ze = zero, on = one ;
        return solveWithoutMemo(0) ;
    }    
}
```

> Time Complexity = O(2<sup>strLen</sup>)

> Space Complexity = O(High) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
public:
    int lw, hi, ze, on ;
    int MOD = 1e9+7 ;
    int solveWithMemo(int strLen, vector<int>& dp){
        if(strLen > hi){
            return 0 ;
        }
        if(dp[strLen] != -1){
            return dp[strLen] ;
        }
        int appendZero = solveWithMemo(strLen + ze, dp) ;
        int appendOne = solveWithMemo(strLen + on, dp) ;

        return dp[strLen] = (strLen >= lw) + (((appendZero % MOD) + (appendOne % MOD)) % MOD) ;
    }
    int countGoodStrings(int low, int high, int zero, int one) {
        lw = low, hi = high, ze = zero, on = one ;
        vector<int> dp(high+1, -1) ;
        return solveWithMemo(0, dp) ;
    }    
}
```

> Time Complexity = O(2*High)

> Space Complexity = O(2*High) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- With 1D table

```cpp
class BottomUp{
public:
    int lw, hi, ze, on ;
    int MOD = 1e9+7 ;

    int solveWithMemo(){
        vector<int> dp(hi+2, -1) ;
        dp[hi+1] = 0 ;

        for(int strLen = hi ; strLen >= 0 ; --strLen){
            int appendZero = ((strLen + ze) <= (hi+1)) ? dp[strLen + ze] : 0 ;
            int appendOne = ((strLen + on) <= (hi+1)) ? dp[strLen + on] : 0 ;
            dp[strLen] = (strLen >= lw) + (((appendZero % MOD) + (appendOne % MOD)) % MOD) ;
        }
        return dp[0] ;
    }

    int countGoodStrings(int low, int high, int zero, int one) {
        lw = low, hi = high, ze = zero, on = one ;
        return solveWithMemo() ;
    }
}
```

> Time Complexity = O(1*N)

> Space Complexity = O(1*N)

---

* Bottom Up Approach -- Without 1D table

```cpp
class bottomUp{
// Can't be further optimized, no pattern found in above dp table
}
```

> Time Complexity = O()

> Space Complexity = O()