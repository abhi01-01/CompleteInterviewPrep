### Leetcode - 2770 - [Maximum Number of Jumps to Reach the Last Index](https://leetcode.com/problems/maximum-number-of-jumps-to-reach-the-last-index/description/)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
    public:
    int solveWithoutMemo(vector<int>& nums, int target, int currIdx){
        int n = nums.size() ;
        if(currIdx == n-1){
            return 0 ;
        }

        int maxJumps = INT_MIN ;

        for(int jump = 1 ; (jump < n) and ((currIdx+jump) < n) ; ++jump){
            int nextIdx = currIdx + jump ;
            int delta = (nums[nextIdx] - nums[currIdx]) ;
            if((delta >= -1*target) and (delta <= target)){
                int nextJump = solveWithoutMemo(nums, target, nextIdx) ;
                if(nextJump != INT_MIN){
                    maxJumps = max(maxJumps, nextJump+1) ;
                }
            }
        }

        return maxJumps ;
    } 

    int maximumJumps(vector<int>& nums, int target) {
        int start = 0 ;
        int maxJumps = solveWithoutMemo(nums, target, start) ;
        return (maxJumps == INT_MIN) ? -1 : maxJumps ;
    }
};
```

> Time Complexity = O(N<sup>N</sup>)

> Space Complexity = O(N) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
    public:
    int solveWithMemo(vector<int>& nums, int target, int currIdx, vector<int>& dp){
        int n = nums.size() ;
        if(currIdx == n-1){
            return 0 ;
        }
        if(dp[currIdx] != -1){
            return dp[currIdx] ;
        }
        int maxJumps = INT_MIN ;

        for(int jump = 1 ; (jump < n) and ((currIdx+jump) < n) ; ++jump){
            int nextIdx = currIdx + jump ;
            int delta = (nums[nextIdx] - nums[currIdx]) ;
            if((delta >= -1*target) and (delta <= target)){
                int nextJump = solveWithMemo(nums, target, nextIdx, dp) ;
                if(nextJump != INT_MIN){
                    maxJumps = max(maxJumps, nextJump+1) ;
                }
            }
        }

        return dp[currIdx] = maxJumps ;
    } 

    int maximumJumps(vector<int>& nums, int target) {
        int start = 0, n = nums.size() ;
        vector<int> dp(n, -1) ;
        int maxJumps = solveWithMemo(nums, target, start, dp) ;
        return (maxJumps == INT_MIN) ? -1 : maxJumps ;
    }
};
```

> Time Complexity = O(N<sup>2</sup>)

> Space Complexity = O(N) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- With 1D table

```cpp
class BottomUp{
    public:
    int solveWith1Dtable(vector<int>& nums, int target){
        int n = nums.size() ;
        vector<int> dp(n, -1) ;
        dp[n-1] = 0 ;


        for(int currIdx = n-2 ; currIdx >= 0 ; --currIdx){
            int maxJumps = INT_MIN ;
            for(int jump = 1 ; (jump < n) and ((currIdx+jump) < n) ; ++jump){
                int nextIdx = currIdx + jump ;
                int delta = (nums[nextIdx] - nums[currIdx]) ;
                if((delta >= -1*target) and (delta <= target)){
                    int nextJump = dp[nextIdx] ;
                    if(nextJump != INT_MIN){
                        maxJumps = max(maxJumps, nextJump+1) ;
                    }
                }
            }
            dp[currIdx] = maxJumps ;
        }
        return dp[0] ;
    } 

    int maximumJumps(vector<int>& nums, int target) {
        int maxJumps = solveWith1Dtable(nums, target) ;
        return (maxJumps == INT_MIN) ? -1 : maxJumps ;
    }
};
```

> Time Complexity = O(N<sup>2</sup>)

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