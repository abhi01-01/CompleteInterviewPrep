### Leetcode - 153 - [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/description/)


```cpp
class Solution {
public:
    int findMin(vector<int>& nums) {
        int low = 0, high = nums.size()-1 ;
        while(low < high){
            int mid = low + (high-low)/2 ;
            if(nums[mid] > nums[high]){
                low = mid + 1 ;
            }
            else{
                high = mid ;
            }
        }
        return nums[high] ;
    }
};
```