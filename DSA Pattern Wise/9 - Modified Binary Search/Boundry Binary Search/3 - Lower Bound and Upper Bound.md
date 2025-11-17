## GFG - [Lower Bound](https://www.geeksforgeeks.org/problems/implement-lower-bound/1)


```cpp
class Solution {
  public:
    int lowerBound(vector<int>& nums, int target) {
        // code here
        int low = 0, high = nums.size() -1 ; 
        
        while(low <= high){
            
            int mid = low + (high - low)/2 ;
            
            if(nums[mid] >= target){
                high = mid - 1 ;
            }
            else {
                low = mid + 1 ;
            }
        }
        return low ;
    }
};
```

> Time Complexity - O(LogN)

> Space Complexity - O(1)

---

## GFG - [Upper Bound](https://www.geeksforgeeks.org/problems/implement-upper-bound/1)

```cpp
class Solution {
  public:
    int upperBound(vector<int>& arr, int target) {
        // code here
        int low = 0, high = arr.size()-1 ;
        
        while(low <= high){
            
            int mid = low + (high - low)/2 ;
            
            if(arr[mid] <= target){
                low = mid + 1 ;
            }
            else{
                high = mid - 1 ;
            }
        }
        return low ;
    }
};
```

> Time Complexity - O(LogN)

> Space Complexity - O(1)