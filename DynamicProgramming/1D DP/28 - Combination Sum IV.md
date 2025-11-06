### Leetcode - 377 - [Combination Sum IV](https://leetcode.com/problems/combination-sum-iv/)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
public:
    int solveWithoutMemo(vector<int>& nums, int target){
        if(target == 0){
            return 1 ;
        }

        int count = 0 ;

        for(int i = 0 ; i < nums.size() ; ++i){
            if(nums[i] <= target)
                count = count + solveWithoutMemo(nums, target - nums[i]) ;
        }
        return count ;
    }

    int combinationSum4(vector<int>& nums, int target) {
        return solveWithoutMemo(nums, target) ;
    }    
};
```
**Recurrence Relation**
> Each recursive call to solveWithoutMemo(nums, target):
>>
>> * Iterates over all n numbers.
>>
>> * For each number nums[i] that’s ≤ target, it makes a recursive call with target - nums[i].
>
> So the recurrence roughly looks like:
>
```math
T(target)=i=1∑n​T(target−nums[i])
```

> Time Complexity = O(N<sup>target</sup>)

> Space Complexity = O(target) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
public:
    int solveWithMemo(vector<int>& nums, int target, vector<int>& dp){
        if(target == 0){
            return 1 ;
        }

        if(dp[target] != -1){
            return dp[target] ;
        }

        int count = 0 ;

        for(int i = 0 ; i < nums.size() ; ++i){
            if(nums[i] <= target)
                count = count + solveWithMemo(nums, target - nums[i], dp) ;
        }
        return dp[target] = count ;
    }

    int combinationSum4(vector<int>& nums, int target) {
        vector<int> dp(target+1, -1) ;
        return solveWithMemo(nums, target, dp) ;
    }    
};
```

> Time Complexity = O(N*target)

> Space Complexity = O(2*target) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- With 1D table
> 2 Ways
>> * Without Sorting
>> 
>> ```cpp
>> class BottomUp{
>> public:
>>     int solveWith1Dtable(vector<int>& nums, int target){
>>         vector<int> dp(target+1, -1) ;
>>         dp[0] = 1 ;
>> 
>>         for(int idx = 1 ; idx <= target ; ++idx){
>>             unsigned int count = 0 ;
>>             for(int i = 0 ; i < nums.size() ; ++i){
>>                 if(nums[i] <= idx)
>>                     count = count + dp[idx - nums[i]] ;
>>             }
>>             dp[idx] = count ;
>>         }
>>         return dp[target] ;
>>     }
>> 
>>     int combinationSum4(vector<int>& nums, int target) {
>>         return solveWith1Dtable(nums, target) ;
>>     }
>> };
>> ```
>> 
>> Time Complexity = O(N*target)
>>
>> Space Complexity = O(N)
>>
>> * With Sorting
>>
>> ```cpp
>> class BottomUp{
>> public:
>>     int solveWith1Dtable(vector<int>& nums, int target){
>>         vector<int> dp(target+1, -1) ;
>>         dp[0] = 1 ;
>> 
>>         for(int idx = 1 ; idx <= target ; ++idx){
>>             unsigned int count = 0 ;
>>             for(int i = 0 ; (i < nums.size()) and (nums[i] <= idx) ; ++i){
>>                  count = count + dp[idx - nums[i]] ;
>>             }
>>             dp[idx] = count ;
>>         }
>>         return dp[target] ;
>>     }
>> 
>>     int combinationSum4(vector<int>& nums, int target) {
>>         sort(nums.begin(), nums.end()) ;
>>         return solveWith1Dtable(nums, target) ;
>>     }
>> };
>> ```

---

* Bottom Up Approach -- Without 1D table

```cpp
class BottomUp{
// Can't be optimized further
};
```

> Time Complexity = O()

> Space Complexity = O()