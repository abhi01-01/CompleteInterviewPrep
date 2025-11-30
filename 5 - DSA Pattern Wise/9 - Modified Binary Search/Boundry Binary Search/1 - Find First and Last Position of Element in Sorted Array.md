## Leetcode - 34 - [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/)

* 1 . Brute force way is to find the target linearly and return the answer.

* 2 . Other way is to do it by binary Search on Boundry Method. 
> Binary Search
>> * Use binary search to find the first occurance of target element
>> * Use binary search to find the last occurance of target element

```cpp
class Solution {
public:

    int findFirstOccuranceIndex(vector<int>&nums, int target){
        int low = 0, high = nums.size()-1, ans = -1 ;

        while(low <= high){

            int mid = low + (high-low)/2 ;

            if(nums[mid] == target){
                ans = mid ;
                high = mid - 1 ;
            }
            else if(nums[mid] > target){
                high = mid - 1 ;
            }
            else{
                low = mid + 1 ;
            }
        }
        return ans ;
    }

    int findLastOccuranceIndex(vector<int>&nums, int target){
        int low = 0, high = nums.size()-1, ans = -1 ;

        while(low <= high){

            int mid = low + (high-low)/2 ;

            if(nums[mid] == target){
                ans = mid ;
                low = mid + 1 ;
            }
            else if(nums[mid] > target){
                high = mid - 1 ;
            }
            else{
                low = mid + 1 ;
            }
        }
        return ans ;
    }        

    vector<int> searchRange(vector<int>& nums, int target) {
       int firstIdx = findFirstOccuranceIndex(nums, target) ;
       int lastIdx = findLastOccuranceIndex(nums, target) ;

       return {firstIdx, lastIdx} ;   
    }
};
```

> Time Complexity - O(2*LogN)

> Space Complexity - O(1)