### Leetcode - 2140 - [Solving Questions With Brainpower](https://leetcode.com/problems/solving-questions-with-brainpower/description/)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
public:
    typedef long long ll ;
    int n ;
    ll solveWithoutMemo(vector<vector<int>>& questions, int currIdx, int end){
        // Edge case : we consumed all questions
        if(currIdx >= end){
            return 0 ;
        }

        ll solveQuestion = questions[currIdx][0] + solveWithoutMemo(questions, (currIdx + questions[currIdx][1] + 1), end) ;
        ll skipQuestion = solveWithoutMemo(questions, currIdx+1, end) ;

        return max(solveQuestion, skipQuestion) ;
    } 
    long long mostPoints(vector<vector<int>>& questions) {
        n = questions.size() ;
        return solveWithoutMemo(questions, 0, n) ;
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
    typedef long long ll ;
    int n ;
    ll solveWithMemo(vector<vector<int>>& questions, int currIdx, int end, vector<ll>& dp){
        // Edge case : we consumed all questions
        if(currIdx >= end){
            return 0 ;
        }

        if(dp[currIdx] != -1){
            dp[currIdx] ;
        }

        ll solveQuestion = questions[currIdx][0] + solveWithMemo(questions, (currIdx + questions[currIdx][1] + 1), end, dp) ;
        ll skipQuestion = solveWithMemo(questions, (currIdx+1), end, dp) ;

        return dp[currIdx] = max(solveQuestion, skipQuestion) ;
    } 
    long long mostPoints(vector<vector<int>>& questions) {
        n = questions.size() ;
        vector<ll> dp(n, -1) ;
        return solveWithMemo(questions, 0, n, dp) ;
    }    
}
```
> Memoization throws TLE in this problem.

> Time Complexity = O(2*N)

> Space Complexity = O(3*N) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- With 1D table

```cpp
class BottomUp{
public:
    typedef long long ll ;
    int n ;
    ll solveWith1Dtable(vector<vector<int>>& questions){
        n = questions.size() ;
        vector<ll> dp(n+1, -1) ;
        // Edge case : we consumed all questions
        dp[n] = 0 ;

        for(int i = n-1 ; i >=0 ; --i){
            int nextQuestion = (i + questions[i][1] + 1) ;
            ll solveQuestion = (questions[i][0] + ((nextQuestion <= n) ? dp[nextQuestion] : 0)) ;
            ll skipQuestion = dp[i+1] ;
            dp[i] = max(solveQuestion, skipQuestion) ;
        }
        return dp[0] ;
    }

    long long mostPoints(vector<vector<int>>& questions) {
        n = questions.size() ;
        vector<ll> dp(n, -1) ;
        return solveWith1Dtable(questions) ;
    }
}
```

> Time Complexity = O(1*N)

> Space Complexity = O(1*N)

---

* Bottom Up Approach -- Without 1D table

```cpp
class bottomUp{
// Can't be further optimized, b/c distribution is random in dp table i.e. no pattern found
}
```

> Time Complexity = O()

> Space Complexity = O()