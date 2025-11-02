### Leetcode - 198 - [House Robber](https://leetcode.com/problems/house-robber/description/?envType=daily-question&envId=2024-01-21) - [CodingNinja](https://www.naukri.com/code360/problems/loot-houses_630510?leftPanelTabValue=SUBMISSION) - [Stickler Thief](https://www.geeksforgeeks.org/problems/stickler-theif-1587115621/1?itm_source=geeksforgeeks&itm_medium=article&itm_campaign=bottom_sticky_on_article)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
public:
    int solveWithoutMemo(vector<int>& nums, int n, int currRob){
        // Edge case: If no houses left then you can't get money
        if(currRob >= n){
            return 0 ;
        }
        int RobHouse = (nums[currRob] + solveWithoutMemo(nums, n, currRob+2)) ;
        int skipRob = solveWithoutMemo(nums, n, currRob+1) ;
        return max(RobHouse, skipRob) ;
    }
    
    int rob(vector<int>& nums) {
        int n = nums.size() ;
        return solveWithoutMemo(nums, n, 0) ;
    }    
}
```

> Time Complexity = O(2<sup>N</sup>)

> Space Complexity = O(2*N) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
    public :
    int solveWithMemo(vector<int>& nums, int n, int currRob, vector<int>& dp){
        // Edge case: If no houses left then you can't get money
        if(currRob >= n){
            return 0 ;
        }
        if(dp[currRob] != -1){
            return dp[currRob] ;
        }

        int RobHouse = (nums[currRob] + solveWithMemo(nums, n, currRob+2, dp)) ;
        int skipRob = solveWithMemo(nums, n, currRob+1, dp) ;
        return dp[currRob] = max(RobHouse, skipRob) ;
    }

    int rob(vector<int>& nums) {
        int n = nums.size() ;
        vector<int> dp(n, -1) ;
        return solveWithMemo(nums, n, 0, dp) ;
    }    
}
```

> Time Complexity = O(2*N)

> Space Complexity = O(3*N) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- With 1D table

```cpp
class BottomUp{
public:
    int solveWith1DTable(vector<int>& nums){
        int n = nums.size() ;
        vector<int> dp(n+1, -1) ;
        // Edge case: If no houses then you can't get money
        // Edge case: if there is only one house, rob it
        dp[0] = 0, dp[1] = nums[0] ;

        for(int i = 2 ; i <= n ; ++i){
            int RobHouse = (nums[i-1] + dp[i-2]) ;
            int skipRob = dp[i-1] ;
            dp[i] = max(RobHouse, skipRob) ;
        }
        return dp[n] ;
    }

    int rob(vector<int>& nums) {
        return solveWith1DTable(nums) ;
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
    int solveWithoutTable(vector<int>& nums){
        int n = nums.size() ;
        // Edge case: If no houses then you can't get money
        // Edge case: if there is only one house, rob it
        int dp0 = 0, dp1 = nums[0] ;
        int currRob = dp1 ;

        for(int i = 2 ; i <= n ; ++i){
            int RobHouse = (nums[i-1] + dp0) ;
            int skipRob = dp1 ;
            currRob = max(RobHouse, skipRob) ;
            dp0 = dp1 ;
            dp1 = currRob ;
        }
        return currRob ;
    }

    int rob(vector<int>& nums) {
        return solveWithoutTable(nums) ;
    }
}
```

> Time Complexity = O(1*N)

> Space Complexity = O(1)