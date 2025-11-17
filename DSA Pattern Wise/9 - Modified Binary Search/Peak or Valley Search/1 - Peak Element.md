## Leetcode - 162 - [Peak Element](https://leetcode.com/problems/find-peak-element/description/) 


* 1 - Brute Force

```cpp
class Solution {
public:
    int findPeakElement(vector<int>& nums) {
        int n = nums.size() ;

        for(int i = 0 ; (i+1) < n ; ++i){
            if(nums[i+1] < nums[i]){
                return i ;
            }
        }
        return nums.size()-1 ;
    }
};
```

> Time Complexity - O(N)

> Space Complexity - O(1)

---
 

* 2 - Binary Search if there is a bitonic or peak structure?

Peak / Valley Search

Core idea:

If `nums[mid] < nums[mid + 1]`
```
→ we are on the slope going upward,
so the peak must exist on the right.
```
Else
```
→ we are on a downward slope or at a peak,
so the peak must exist on the left or at mid.
```
Why?

Because in a “mountain” shape, as long as the next number is higher, you’re still climbing — keep going right.

Once you start going down, the top is behind or at your current point.

<br>

```cpp
class Solution {
public:
    int findPeakElement(vector<int>& nums) {
        int low = 0, high = nums.size()-1 ;

        while(low < high){

            int mid = low + (high-low)/2 ;

            if(nums[mid+1] > nums[mid]){
                low = mid+1 ;
            }
            else{
                high = mid ;
            }
        }
        return high ;
    }
};
```

> Time Complexity - O(logN)

> Space Complexity - O(1)