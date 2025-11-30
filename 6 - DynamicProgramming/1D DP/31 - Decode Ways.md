### Leetcode - 91 - [Decode Ways](https://leetcode.com/problems/decode-ways/description/)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
public:
    int solveWithoutMemo(string& s, int currIdx){
        int n = s.length() ;
        // Edge case: If all the characters are exhausted then you've decoded the whole string hence you've one valid way
        if(currIdx >= n){
            return 1 ;
        }

        // Edge case: If the character is '0' then you've can't decode it in the valid way
        if(s[currIdx] == '0'){
            return 0 ;
        }

        // If you're here then it's guaranteed that the character lies within '1' to '9' which can be decoded hence consider it and move to the next character
        int decodeWays = solveWithoutMemo(s, currIdx + 1) ;

        // If you're here then there are two possible ways of decoding: When the current character is '1' then it's guaranteed that the next character will be within '0' to '9'. If the current character is '2' then you can only decode when the next character lies within '0' to '6'
        if(((currIdx+1) < n) and (s[currIdx] == '1' or (s[currIdx] == '2' and s[currIdx+1] <= '6'))){
            decodeWays += solveWithoutMemo(s, currIdx + 2) ;
        }

        return decodeWays ;
    }

    int numDecodings(string s) {
        int start = 0 ;
        return solveWithoutMemo(s, start) ;
    }    
};
```

> Time Complexity = O(2<sup>N</sup>)

> Space Complexity = O(N) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
public:
    int solveWithMemo(string& s, int currIdx, vector<int>& dp){
        int n = s.length() ;
        if(currIdx >= n){
            return 1 ;
        }
        if(s[currIdx] == '0'){
            return 0 ;
        }

        if(dp[currIdx] != -1){
            return dp[currIdx] ;
        }

        int decodeWays = solveWithMemo(s, currIdx + 1, dp) ;

        if(((currIdx+1) < n) and (s[currIdx] == '1' or (s[currIdx] == '2' and s[currIdx+1] <= '6'))){
            decodeWays += solveWithMemo(s, currIdx + 2, dp) ;
        }

        return dp[currIdx] = decodeWays ;
    }

    int numDecodings(string s) {
        int start = 0, n = s.length() ;
        vector<int> dp(n, -1) ;
        return solveWithMemo(s, start, dp) ;
    }    
};
```

> Time Complexity = O(2*N)

> Space Complexity = O(2*N) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- With 1D table

```cpp
class BottomUp{
public:
    int solveWith1Dtable(string& s){
        int n = s.length() ;
        vector<int> dp(n+1, -1) ;
        dp[n] = 1 ;
        for(int currIdx = n-1 ; currIdx >= 0 ; --currIdx){
            if(s[currIdx] == '0'){
                dp[currIdx] = 0 ;
            }
            else{
                int decodeWays = dp[currIdx + 1] ;
                if(((currIdx+1) < n) and (s[currIdx] == '1' or (s[currIdx] == '2' and s[currIdx+1] <= '6'))){
                    decodeWays += ((currIdx + 2) <= n)   ? dp[currIdx + 2] : 0 ;
                }
                dp[currIdx] = decodeWays ;
            }
        }
        return dp[0] ;
    }

    int numDecodings(string s) {
        return solveWith1Dtable(s) ;
    }
};
```

> Time Complexity = O(N)

> Space Complexity = O(N)

---

* Bottom Up Approach -- Without 1D table

```cpp
class BottomUp{
public:
    int solveWithouttable(string& s){
        int n = s.length() ;
        int dpAtCurrIdx = 0, dpAtCurrIdxPlus1 = 1, dpAtCurrIdxPlus2 = 0 ;

        for(int currIdx = n-1 ; currIdx >= 0 ; --currIdx){
            if(s[currIdx] == '0'){
                dpAtCurrIdx = 0 ;
            }
            else{
                int decodeWays = dpAtCurrIdxPlus1 ;
                if(((currIdx+1) < n) and (s[currIdx] == '1' or (s[currIdx] == '2' and s[currIdx+1] <= '6'))){
                    decodeWays += ((currIdx + 2) <= n)   ? dpAtCurrIdxPlus2 : 0 ;
                }
                dpAtCurrIdx = decodeWays ;
            }
            dpAtCurrIdxPlus2 = dpAtCurrIdxPlus1 ;
            dpAtCurrIdxPlus1 = dpAtCurrIdx ;
        }
        return dpAtCurrIdx ;
    }

    int numDecodings(string s) {
        return solveWithouttable(s) ;
    }
};
```

> Time Complexity = O(N)

> Space Complexity = O(1)