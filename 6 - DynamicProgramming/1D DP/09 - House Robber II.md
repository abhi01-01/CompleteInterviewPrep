### Leetcode - 213 - [House Robber II](https://leetcode.com/problems/house-robber-ii/description/)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
public:
    int solveWithoutMemo(vector<int>& nums, int currRob, int lastHouse){
        // Edge Case : Edge case: If no houses left then you can't get money 
        if(currRob >= lastHouse){
            return 0 ;
        }

        int robHouse = (nums[currRob] + solveWithoutMemo(nums, currRob+2, lastHouse)) ;
        int skipRob = solveWithoutMemo(nums, currRob+1, lastHouse) ;

        return max(robHouse, skipRob) ;
    }
    int rob(vector<int>& nums) {
        int n = nums.size() ;
        if(n==1){
            return nums[0] ;
        }
        int startWith0 = solveWithoutMemo(nums, 0, n-1) ;
        int startWith1 = solveWithoutMemo(nums, 1, n) ;

        return max(startWith0, startWith1) ;
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
    int solveWithMemo(vector<int>& nums, int currRob, int lastHouse, vector<int>& dp){
        // Edge Case : Edge case: If no houses left then you can't get money 
        if(currRob >= lastHouse){
            return 0 ;
        }

        if(dp[currRob] != -1){
            return dp[currRob] ;
        }

        int robHouse = (nums[currRob] + solveWithMemo(nums, currRob+2, lastHouse, dp)) ;
        int skipRob = solveWithMemo(nums, currRob+1, lastHouse, dp) ;

        return dp[currRob] = max(robHouse, skipRob) ;
    }
    int rob(vector<int>& nums) {
        int n = nums.size() ;
        if(n==1){
            return nums[0] ;
        }
        // memoize 2 diff recursion calls in 2 diff memory
        vector<int> dp1(n, -1), dp2(n, -1) ;
        int startWith0 = solveWithMemo(nums, 0, n-1, dp1) ;
        int startWith1 = solveWithMemo(nums, 1, n,  dp2) ;

        return max(startWith0, startWith1) ;
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
    int solveWith1DTable(vector<int>& nums, int start, int end){
        int size = (end-start+2) ;
        vector<int> dp(size, -1) ;
        // Edge case: If no houses then you can't get money
        dp[0] = 0 ; 
        // Edge case: if there is only one house, rob it
        dp[1] = nums[start] ;
        // traversing nums by 'j' and dp by 'i'
        for(int i = 2, j = (start+1) ; i < size and j <= end ; ++i, ++j){
            int robHouse = (nums[j] + dp[i-2]) ;
            int skipRob = dp[i-1] ;
            dp[i] = max(robHouse, skipRob) ;
        }

        return dp[size-1] ;
    } 
    int rob(vector<int>& nums) {
        int n = nums.size() ;
        if(n==1){
            return nums[0] ;
        }
        int startWith0 = solveWith1DTable(nums, 0, n-2) ;
        int startWith1 = solveWith1DTable(nums, 1, n-1) ;

        return max(startWith0, startWith1) ;
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
    int solveWith1DTable(vector<int>& nums, int start, int end){
        int size = (end-start+2) ;
        // Edge case: If no houses then you can't get money
        int dp_0 = 0 ; 
        // Edge case: if there is only one house, rob it
        int dp_1 = nums[start] ;

        int dp_i = max(dp_0, dp_1) ;
        // traversing nums by 'j' and dp by 'i'
        for(int i = 2, j = (start+1) ; i < size and j <= end ; ++i, ++j){
            int robHouse = (nums[j] + dp_0) ;
            int skipRob = dp_1 ;
            dp_i = max(robHouse, skipRob) ;
            dp_0 = dp_1 ;
            dp_1 = dp_i ;
        }

        return dp_i ;
    } 
    int rob(vector<int>& nums) {
        int n = nums.size() ;
        if(n==1){
            return nums[0] ;
        }
        int startWith0 = solveWith1DTable(nums, 0, n-2) ;
        int startWith1 = solveWith1DTable(nums, 1, n-1) ;

        return max(startWith0, startWith1) ;
    }
}
```

> Time Complexity = O(1*N)

> Space Complexity = O(1*N)