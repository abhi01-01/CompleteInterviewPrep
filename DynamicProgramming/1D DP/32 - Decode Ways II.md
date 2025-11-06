### Leetcode - 639 - [Decode Ways II](https://leetcode.com/problems/decode-ways-ii/description/)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
public:
    const int MOD = 1e9 + 7;
    long long solveWithoutMemo(string &s, int i) {
        if (i == s.size()) return 1; // reached end
        if (s[i] == '0') return 0;   // invalid start
        
        long long ways = 0;

        // 🔹 Case 1: Single character
        if (s[i] == '*') {
            ways = (ways + 9 * solveWithoutMemo(s, i + 1)) % MOD;
        } else {
            ways = (ways + solveWithoutMemo(s, i + 1)) % MOD;
        }

        // 🔹 Case 2: Two characters (i and i+1)
        if (i + 1 < s.size()) {
            char c1 = s[i] ;
            char c2 = s[i+1] ;
            if (c1 == '*' && c2 == '*') {
                // '**' → "11–19" and "21–26" → 15 combinations
                ways = (ways + 15 * solveWithoutMemo(s, i + 2)) % MOD;
            } else if (c1 == '*' and c2 != '*') {
                // first char is '*'
                if (c2 >= '0' && c2 <= '6')
                    ways = (ways + 2 * solveWithoutMemo(s, i + 2)) % MOD; // "1x" or "2x"
                else
                    ways = (ways + solveWithoutMemo(s, i + 2)) % MOD; // only "1x"
            } else if (c2 == '*' and c1 != '*') {
                // second char is '*'
                if (c1 == '1')
                    ways = (ways + 9 * solveWithoutMemo(s, i + 2)) % MOD; // "1*" → 11–19
                else if (c1 == '2')
                    ways = (ways + 6 * solveWithoutMemo(s, i + 2)) % MOD; // "2*" → 21–26
            } else {
                // both digits fixed
                int val = (c1 - '0') * 10 + (c2 - '0');
                if (val >= 10 && val <= 26)
                    ways = (ways + solveWithoutMemo(s, i + 2)) % MOD;
            }
        }

        return ways;
    }
    int numDecodings(string s) {
        return solveWithoutMemo(s, 0);
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
    int M = 1e9+7 ;
    int solveWithMemo(string& s, int i, vector<int>& dp){
        if(i >= s.size()) return 1 ;
        if(s[i] == '0') return 0 ;

        if(dp[i] != -1){
            return dp[i] ;
        }

        long long ways = 0 ;

        // Case 1 : single character
        if(s[i] == '*'){
            ways = (ways + ((9LL % M) * (solveWithMemo(s, i + 1, dp) % M)) % M) % M;
        }
        else{
            ways = (ways%M + (solveWithMemo(s, i+1, dp))%M)%M ;
        }

        // case 2 : 2 character , * and D, 2 places 4 ways to set

        if((i+1) < s.size()){
            char c1 = s[i] ;
            char c2 = s[i+1] ;

            if(c1 == '*' and c2 == '*'){
                ways = (ways + ((15LL % M) * (solveWithMemo(s, i + 2, dp) % M)) % M) % M;
            }
            else if(c1 == '*' and c2 != '*'){
                if(c2 >= '0' and c2 <= '6'){
                    ways = (ways + ((2LL % M) * (solveWithMemo(s, i + 2, dp) % M)) % M) % M;
                }
                else{
                    ways = (ways + (solveWithMemo(s, i + 2, dp) % M)) % M;
                }
            }
            else if(c1 != '*' and c2 == '*'){
                if(c1 == '1'){
                    ways = (ways + ((9LL % M) * (solveWithMemo(s, i + 2, dp) % M)) % M) % M;
                }
                else if(c1 == '2'){
                    ways = (ways + ((6LL % M) * (solveWithMemo(s, i + 2, dp) % M)) % M) % M;
                }
            }
            else{
                int val = (c1-'0')*10 + (c2-'0') ;
                if(val >= 10 and val <= 26){
                     ways = (ways + (solveWithMemo(s, i + 2, dp) % M)) % M;
                }
            }
        }
        return dp[i] = ways ;
    }

    int numDecodings(string s) {
        int start = 0, n = s.size() ; 
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
    int M = 1e9+7 ;
    int solveWith1Dtable(string& s){
        int n = s.size() ; 
        vector<int> dp(n+1, -1) ;
        dp[n] = 1 ;       // increased dp size by 1 just to avoid writing ternary operator cases for dp[i+2] <- func(s, i+2)

        for(int i = n-1 ; i >= 0 ; --i){

            if(s[i] == '0') dp[i] = 0 ;

            else{
                long long ways = 0 ;

                // Case 1 : single character
                if(s[i] == '*'){
                    ways = (ways + ((9LL % M) * (dp[i + 1] % M)) % M) % M;
                }
                else{
                    ways = (ways%M + dp[i+1]%M)%M ;
                }

                // case 2 : 2 character , * and D, 2 places 4 ways to set

                if((i+1) < s.size()){
                    char c1 = s[i] ;
                    char c2 = s[i+1] ;

                    if(c1 == '*' and c2 == '*'){
                        ways = (ways + ((15LL % M) * (dp[i + 2] % M)) % M) % M;
                    }
                    else if(c1 == '*' and c2 != '*'){
                        if(c2 >= '0' and c2 <= '6'){
                            ways = (ways + ((2LL % M) * (dp[i + 2] % M)) % M) % M;
                        }
                        else{
                            ways = (ways + (dp[i + 2] % M)) % M;
                        }
                    }
                    else if(c1 != '*' and c2 == '*'){
                        if(c1 == '1'){
                            ways = (ways + ((9LL % M) * (dp[i + 2] % M)) % M) % M;
                        }
                        else if(c1 == '2'){
                            ways = (ways + ((6LL % M) * (dp[i + 2] % M)) % M) % M;
                        }
                    }
                    else{
                        int val = (c1-'0')*10 + (c2-'0') ;
                        if(val >= 10 and val <= 26){
                            ways = (ways + (dp[i + 2] % M)) % M;
                        }
                    }
                }
                dp[i] = ways ;
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
    int M = 1e9+7 ;
    int solveWithouttable(string& s){
        int n = s.size() ; 
        int dpAti = 0, dpAtiPlus1 = 1, dpAtiPlus2 = 0 ;   
        for(int i = n-1 ; i >= 0 ; --i){

            if(s[i] == '0') dpAti = 0 ;

            else{
                long long ways = 0 ;

                // Case 1 : single character
                if(s[i] == '*'){
                    ways = (ways + ((9LL % M) * (dpAtiPlus1 % M)) % M) % M;
                }
                else{
                    ways = (ways%M + dpAtiPlus1 % M) % M ;
                }

                // case 2 : 2 character , * and D, 2 places 4 ways to set

                if((i+1) < s.size()){
                    char c1 = s[i] ;
                    char c2 = s[i+1] ;

                    if(c1 == '*' and c2 == '*'){
                        ways = (ways + ((15LL % M) * (dpAtiPlus2 % M)) % M) % M;
                    }
                    else if(c1 == '*' and c2 != '*'){
                        if(c2 >= '0' and c2 <= '6'){
                            ways = (ways + ((2LL % M) * (dpAtiPlus2 % M)) % M) % M;
                        }
                        else{
                            ways = (ways + (dpAtiPlus2 % M)) % M;
                        }
                    }
                    else if(c1 != '*' and c2 == '*'){
                        if(c1 == '1'){
                            ways = (ways + ((9LL % M) * (dpAtiPlus2 % M)) % M) % M;
                        }
                        else if(c1 == '2'){
                            ways = (ways + ((6LL % M) * (dpAtiPlus2 % M)) % M) % M;
                        }
                    }
                    else{
                        int val = (c1-'0')*10 + (c2-'0') ;
                        if(val >= 10 and val <= 26){
                            ways = (ways + (dpAtiPlus2 % M)) % M;
                        }
                    }
                }
                dpAti = ways ;
            }
            dpAtiPlus2 = dpAtiPlus1 ;
            dpAtiPlus1 = dpAti ;
        }

        return dpAti ;
    }

    int numDecodings(string s) {
        return solveWithouttable(s) ;
    }
};
```

> Time Complexity = O(N)

> Space Complexity = O(1)



### Follow Up - 01 -> What if, `*` represent any digit from `1 - 9`

That changes the rules a lot, because:

* `0` by itself is not a valid decoding (it can’t start a letter).

* But if `*` becomes `0`, it can only pair with a `1` or `2` before it to make `"10"` or `"20"`.<br>
So basically, we need to treat `'*'` as possibly `'0'`, but ignore those branches where it forms invalid standalone digits.

```cpp
class Solution {
public:
    const int MOD = 1e9 + 7;

    long long solve(string &s, int i) {
        if (i == s.size()) return 1; // reached end
        if (s[i] == '0') return 0;   // can't start with 0

        long long ways = 0;

        // 🔹 Case 1: Single character
        if (s[i] == '*') {
            // '*' can be 0–9, but '0' isn't valid alone, so 1–9 only
            ways = (ways + 9 * solve(s, i + 1)) % MOD;
        } else {
            // fixed digit, only valid if not '0'
            ways = (ways + solve(s, i + 1)) % MOD;
        }

        // 🔹 Case 2: Two characters (i and i+1)
        if (i + 1 < s.size()) {
            char c1 = s[i];
            char c2 = s[i + 1];

            if (c1 == '*' && c2 == '*') {
                // '**' can represent "00"–"99", but valid 2-digit codes are 10–26
                // So possibilities: 10–19 (10), 20–26 (7) → total 17
                ways = (ways + 17 * solve(s, i + 2)) % MOD;
            }
            else if (c1 == '*') {
                // First char '*', second fixed
                if (c2 >= '0' && c2 <= '6')
                    ways = (ways + 2 * solve(s, i + 2)) % MOD; // "1x" or "2x"
                else if (c2 >= '7' && c2 <= '9')
                    ways = (ways + solve(s, i + 2)) % MOD; // only "1x"
            }
            else if (c2 == '*') {
                // First fixed, second '*'
                if (c1 == '1')
                    ways = (ways + 10 * solve(s, i + 2)) % MOD; // "10"–"19"
                else if (c1 == '2')
                    ways = (ways + 7 * solve(s, i + 2)) % MOD;  // "20"–"26"
            }
            else {
                // both fixed
                int val = (c1 - '0') * 10 + (c2 - '0');
                if (val >= 10 && val <= 26)
                    ways = (ways + solve(s, i + 2)) % MOD;
            }
        }

        return ways;
    }

    int numDecodings(string s) {
        return solve(s, 0);
    }
};
```

### Follow Up - 02 -> if mappings extended to 99 (like a custom variant)?

* Every number from `1` to `99` is a valid code → `"1" → A`, `"2" → B`, … `"99" → CV` or whatever.

* That means now any two-digit number between `10–99` is valid, not just `10–26`.<br>
So when we see `'3'–'9'` followed by `'*'`, those pairs are totally valid.


```cpp
class Solution {
public:
    const int MOD = 1e9 + 7;

    long long solve(string &s, int i) {
        if (i == s.size()) return 1; // reached end
        if (s[i] == '0') return 0;   // can't start with 0 alone

        long long ways = 0;

        // 🔹 Case 1: Single character
        if (s[i] == '*') {
            // '*' can represent 1–9 (0 invalid as a single digit)
            ways = (ways + 9 * solve(s, i + 1)) % MOD;
        } else {
            ways = (ways + solve(s, i + 1)) % MOD;
        }

        // 🔹 Case 2: Two characters
        if (i + 1 < s.size()) {
            char c1 = s[i], c2 = s[i + 1];

            if (c1 == '*' && c2 == '*') {
                // "**" → can form 10–99 → 90 valid pairs (10 through 99)
                ways = (ways + 90 * solve(s, i + 2)) % MOD;
            }
            else if (c1 == '*') {
                // First '*' can be 1–9, form pairs 10–19, 20–29, ... 90–99
                // But if c2 == '0', we skip "00"
                int second = c2 - '0';
                if (second >= 0 && second <= 9) {
                    ways = (ways + 9 * solve(s, i + 2)) % MOD;
                }
            }
            else if (c2 == '*') {
                // Fixed first digit 1–9, second '*' can be 0–9
                // Forms 10,11,...19 for '1', 20–29 for '2', etc.
                if (c1 != '0')
                    ways = (ways + 10 * solve(s, i + 2)) % MOD;
            }
            else {
                // Both fixed digits
                int val = (c1 - '0') * 10 + (c2 - '0');
                if (val >= 10 && val <= 99)
                    ways = (ways + solve(s, i + 2)) % MOD;
            }
        }

        return ways;
    }

    int numDecodings(string s) {
        return solve(s, 0);
    }
};
```