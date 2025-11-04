### Leetcode - 55 - [Jump Game](https://leetcode.com/problems/jump-game/)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
    public :
    bool solveWithoutMemo(vector<int>& nums, int currIdx){
        if(currIdx == nums.size()-1){
            return true ;
        }

        for(int jump = 1 ; (jump <= nums[currIdx]) and ((currIdx + jump) < nums.size()) ; ++jump){
            if(solveWithoutMemo(nums, currIdx+jump)){
                return true ;
            }
        }
        return false ;
    }

    bool canJump(vector<int>& nums){
        int start = 0 ;
        return solveWithoutMemo(nums, start) ;
    }
};
```

> Time Complexity = O(M<sup>N</sup>), where M is maximum element of array and N is the size of the array

> Space Complexity = O(N) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
    public :
        bool solveWithMemo(vector<int>& nums, int currIdx, vector<int>& dp){
        if(currIdx == nums.size()-1){
            return true ;
        }

        if(dp[currIdx] != -1){
            return dp[currIdx] ;
        }

        for(int jump = 1 ; (jump <= nums[currIdx]) and ((currIdx + jump) < nums.size()) ; ++jump){
            if(solveWithMemo(nums, currIdx+jump, dp)){
                return dp[currIdx] = true ;
            }
        }
        return dp[currIdx] = false ;
    }

    bool canJump(vector<int>& nums){
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
    public :
    bool solveWith1DTable(vector<int>& nums){
        int n = nums.size() ;
        vector<int> dp(n, false) ;
        dp[n-1] = true ;

        for(int currIdx = n-2 ; currIdx >= 0 ; --currIdx){
            for(int jump = 1 ; (jump <= nums[currIdx]) and ((currIdx + jump) < nums.size()) ; ++jump){
                if(dp[currIdx+jump]){
                    dp[currIdx] = true ;
                    break ;
                }
            }
        }
        return dp[0] ;
    }

    bool canJump(vector<int>& nums){
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