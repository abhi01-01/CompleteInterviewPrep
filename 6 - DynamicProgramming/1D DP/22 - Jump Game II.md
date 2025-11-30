### Leetcode - 45 - [Jump Game II](https://leetcode.com/problems/jump-game-ii/)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
    public:
    int solveWithoutMemo(vector<int>& nums, int currIdx){
        int n = nums.size() ;
        if(currIdx == n-1){
            return 0 ;
        }

        int minJumps = INT_MAX ;

        for(int jump = 1 ; jump <= nums[currIdx] and ((currIdx + jump) < n) ; ++jump){
            int nextJump = solveWithoutMemo(nums, currIdx + jump) ;
            if(nextJump != INT_MAX){
                minJumps = min(minJumps, nextJump + 1) ;
            }
        }
        return minJumps ;
    }

    int jump(vector<int>& nums) {
        int start = 0 ;
        return solveWithoutMemo(nums, start) ;
    }
};
```

> Time Complexity = O(M<sup>N</sup>)

> Space Complexity = O(N) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
    public:
    int solveWithMemo(vector<int>& nums, int currIdx, vector<int>& dp){
        int n = nums.size() ;
        if(currIdx == n-1){
            return 0 ;
        }

        if(dp[currIdx] != -1){
            return dp[currIdx] ;
        }

        int minJumps = INT_MAX ;

        for(int jump = 1 ; jump <= nums[currIdx] and ((currIdx + jump) < n) ; ++jump){
            int nextJump = solveWithMemo(nums, currIdx + jump, dp) ;
            if(nextJump != INT_MAX){
                minJumps = min(minJumps, nextJump + 1) ;
            }
        }
        return dp[currIdx] = minJumps ;
    }

    int jump(vector<int>& nums) {
        int start = 0, n = nums.size() ;
        vector<int> dp(n, -1) ;
        return solveWithMemo(nums, start, dp) ;
    }
};
```

> Time Complexity = O(M*N)

> Space Complexity = O(2*N) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- With 1D table

```cpp
class BottomUp{
    public:
    int solveWith1DTable(vector<int>& nums){
        int n = nums.size() ;
        vector<int> dp(n, -1) ;
        dp[n-1] = 0 ;

        for(int currIdx = n-2 ; currIdx >= 0 ; --currIdx){
            int minJumps = INT_MAX ;
            for(int jump = 1 ; jump <= nums[currIdx] and ((currIdx + jump) < n) ; ++jump){
                int nextJump = dp[currIdx + jump] ;
                if(nextJump != INT_MAX){
                    minJumps = min(minJumps, nextJump + 1) ;
                }
            }
            dp[currIdx] = minJumps ;
        }

        return dp[0] ;
    }

    int jump(vector<int>& nums) {
        return solveWith1DTable(nums) ;
    }

};
```

> Time Complexity = O(M*N)

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