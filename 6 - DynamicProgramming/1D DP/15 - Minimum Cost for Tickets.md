### Leetcode - 983 - [Minimum Cost for Tickets](https://leetcode.com/problems/minimum-cost-for-tickets/description/)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
public:
    int getNextStartDayIdx(vector<int>& days, int minNextStartDay, int start){
        int n = days.size() ;

        for(int idx = start ; idx < n ; ++idx){
            if(days[idx] >=  minNextStartDay){
                return idx ;
            }
        }
        return n ;
    }

    int solveWithoutMemo(vector<int>& days, vector<int>& costs, int currIdx){
        if(currIdx == days.size()){
            return 0 ;
        }

        int oneDayPass = costs[0] + solveWithoutMemo(days, costs, getNextStartDayIdx(days, days[currIdx] + 1,  currIdx+1)) ;
        int sevenDaysPass = costs[1] + solveWithoutMemo(days, costs, getNextStartDayIdx(days, days[currIdx] + 7,  currIdx+1)) ;
        int thirtyDaysPass = costs[2] + solveWithoutMemo(days, costs, getNextStartDayIdx(days, days[currIdx] + 30,  currIdx+1)) ;

        return min({oneDayPass, sevenDaysPass, thirtyDaysPass}) ;
    }

    int mincostTickets(vector<int>& days, vector<int>& costs) {
        return solveWithoutMemo(days, costs, 0) ;
    }    
}
```

> Time Complexity = O(N*3<sup>N</sup>)

> Space Complexity = O(3*N) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
public:
    int getNextStartDayIdx(vector<int>& days, int minNextStartDay, int start){
        int n = days.size() ;

        for(int idx = start ; idx < n ; ++idx){
            if(days[idx] >=  minNextStartDay){
                return idx ;
            }
        }
        return n ;
    }

    int solveWithoutMemo(vector<int>& days, vector<int>& costs, int currIdx, vector<int>& dp){
        if(currIdx == days.size()){
            return 0 ;
        }

        if(dp[currIdx] != -1){
            return dp[currIdx] ;
        }

        int oneDayPass = costs[0] + solveWithoutMemo(days, costs, getNextStartDayIdx(days, days[currIdx] + 1,  currIdx+1), dp) ;
        int sevenDaysPass = costs[1] + solveWithoutMemo(days, costs, getNextStartDayIdx(days, days[currIdx] + 7,  currIdx+1), dp) ;
        int thirtyDaysPass = costs[2] + solveWithoutMemo(days, costs, getNextStartDayIdx(days, days[currIdx] + 30,  currIdx+1), dp) ;

        return dp[currIdx] = min({oneDayPass, sevenDaysPass, thirtyDaysPass}) ;
    }

    int mincostTickets(vector<int>& days, vector<int>& costs) {
        int n = days.size() ;
        vector<int> dp(n+1, -1) ;
        return solveWithoutMemo(days, costs, 0, dp) ;
    }    
}
```

> Time Complexity = O(3*N<sup>2</sup>)

> Space Complexity = O(3*N) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- With 1D table

__`minNextStartDay` with linear Search__

```cpp
class BottomUp{
public:
    int getNextStartDayIdx(vector<int>& days, int minNextStartDay, int start){
        int n = days.size() ;

        for(int idx = start ; idx < n ; ++idx){
            if(days[idx] >=  minNextStartDay){
                return idx ;
            }
        }
        return n ;
    }

    int solveWith1DTable(vector<int>& days, vector<int>& costs){
        int n = days.size() ;
        vector<int> dp(n+1, -1) ;
        dp[n] = 0 ;

        for(int i = (n-1) ; i >= 0 ; --i){
            int oneDayPass = costs[0] + dp[getNextStartDayIdx(days, days[i] + 1,  i+1)] ;
            int sevenDaysPass = costs[1] + dp[getNextStartDayIdx(days, days[i] + 7,  i+1)] ;
            int thirtyDaysPass = costs[2] + dp[getNextStartDayIdx(days, days[i] + 30,  i+1)] ;
            dp[i] = min({oneDayPass, sevenDaysPass, thirtyDaysPass}) ;
        }
        return dp[0] ;
    }

    int mincostTickets(vector<int>& days, vector<int>& costs) {
        int n = days.size() ;
        vector<int> dp(n+1, -1) ;
        return solveWith1DTable(days, costs) ;
    }
}
```

> Time Complexity = O(N<sup>2</sup>)

> Space Complexity = O(1*N)

__`minNextStartDay` with Binary Search__

```cpp
class Solution {
public:
    int getNextStartDayIdx(vector<int>& days, int minNextStartDay, int start){
        int end = days.size() - 1 ;

        while(start <= end){
            int mid = start + (end - start)/2 ;
            if(days[mid] == minNextStartDay){
                return mid ;
            }
            else if(days[mid] > minNextStartDay){
                end = mid - 1 ;
            }
            else{
                start = mid + 1 ;
            }
        }
        return start ;
    }

    int solveWith1DTable(vector<int>& days, vector<int>& costs){
        int n = days.size() ;
        vector<int> dp(n+1, -1) ;
        dp[n] = 0 ;

        for(int i = (n-1) ; i >= 0 ; --i){
            int oneDayPass = costs[0] + dp[getNextStartDayIdx(days, days[i] + 1,  i+1)] ;
            int sevenDaysPass = costs[1] + dp[getNextStartDayIdx(days, days[i] + 7,  i+1)] ;
            int thirtyDaysPass = costs[2] + dp[getNextStartDayIdx(days, days[i] + 30,  i+1)] ;
            dp[i] = min({oneDayPass, sevenDaysPass, thirtyDaysPass}) ;
        }
        return dp[0] ;
    }

    int mincostTickets(vector<int>& days, vector<int>& costs) {
        int n = days.size() ;
        vector<int> dp(n+1, -1) ;
        return solveWith1DTable(days, costs) ;
    }
};
```

> Time Complexity = O(NlogN)

> Space Complexity = O(1*N)

---

* Bottom Up Approach -- Without 1D table

```cpp
class bottomUp{
// Can't be further optimized, no fixed pattern found
}
```

> Time Complexity = O()

> Space Complexity = O()