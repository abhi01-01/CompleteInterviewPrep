### L - 33 - [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/description/)

```cpp
class Solution{
    public :
    int search(vector<int>& nums, int target){
        int low = 0, high = nums.size()-1 ;
        while(low <= high){
            int mid = low + (high-low)/2 ;

            double pivot = ((nums[mid] < nums[0]) == (target < nums[0])) ?
                        nums[mid] :
                        (target < nums[0]) ? -INFINITY : INFINITY ;
            if(pivot < target){
                low = mid+1 ;
            }
            else if(pivot > target){
                high = mid ;
            }            
            else{
                return mid ;
            }
        }
        return -1 ;
    }
};
```

> Time Complexity - O(LogN)

> Space Complexity - O(1)

🔍 The problem

Normal binary search assumes the array is fully sorted.<br>
But rotation breaks that assumption — so when we pick a mid,
we need to figure out whether `nums[mid]` and `target` are in the same half.

That’s exactly what this line is doing:

```cpp
double num = (nums[mid] < nums[0]) == (target < nums[0])
                   ? nums[mid]
                   : target < nums[0] ? -INFINITY : INFINITY;
```

### breakdown
1️⃣ nums[mid] < nums[0]

* This is true if nums[mid] is in the right rotated half (smaller side).

* This is false if nums[mid] is in the left rotated half (bigger side).

2️⃣ (nums[mid] < nums[0]) == (target < nums[0])

* This checks if nums[mid] and target belong to the same half.

* If true, we can compare them normally.

* If false, we’ll simulate that nums[mid] is "infinity" or "−infinity"
to push the binary search toward the correct half.