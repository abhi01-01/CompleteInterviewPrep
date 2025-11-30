## Leetcode - 1095 - [Find in Mountain Array](https://leetcode.com/problems/find-in-mountain-array/description/)

* This question is a combination of 2 questions, `Peak element in the Mountain Array` and find `target` in sorted array.

As per question, since target can be at any or both the slopes of mountain, so search on both slopes and return answer as per question asked.


```cpp
/**
 * // This is the MountainArray's API interface.
 * // You should not implement it, or speculate about its implementation
 * class MountainArray {
 *   public:
 *     int get(int index);
 *     int length();
 * };
 */

class Solution {
public:
    int peakIndexMountainArray(MountainArray &mountainArr, int n){
        int low = 0, high = n-1 ;

        while(low < high){
            int mid = low +(high-low)/2 ;

            if(mountainArr.get(mid+1) > mountainArr.get(mid)){
                low = mid + 1 ;
            }
            else{
                high = mid ;
            }
        }
        return high ;
    }

    int binarySearchForTargetOnIncreasingSolpe(int target, int low, int high, MountainArray &mountainArr){

        while(low <= high){

            int mid = low + (high - low)/2 ;

            if(mountainArr.get(mid) == target){
                return mid ;
            }
            else if(mountainArr.get(mid) < target){
                low = mid + 1 ;
            }
            else{
                high = mid - 1 ;
            }
        }
        return -1 ;
    }

    int binarySearchForTargetOnDecreasingSolpe(int target, int low, int high, MountainArray &mountainArr){

        while(low <= high){

            int mid = low + (high - low)/2 ;

            if(mountainArr.get(mid) == target){
                return mid ;
            }
            else if(mountainArr.get(mid) > target){
                low = mid + 1 ;
            }
            else{
                high = mid - 1 ;
            }
        }
        return -1 ;
    }

    int findInMountainArray(int target, MountainArray &mountainArr) {
        int n = mountainArr.length() ;

        int peakIndex = peakIndexMountainArray(mountainArr, n) ;

        int targetIndexAtIncreasingSolpe = binarySearchForTargetOnIncreasingSolpe(target, 0, peakIndex, mountainArr) ;

        int targetIndexAtDecreasingSolpe = binarySearchForTargetOnDecreasingSolpe(target, peakIndex+1, n-1, mountainArr) ;

        if(targetIndexAtIncreasingSolpe == -1 and targetIndexAtDecreasingSolpe == -1){
            return -1 ;
        }
        else if(targetIndexAtIncreasingSolpe == -1 and targetIndexAtDecreasingSolpe != -1){
            return targetIndexAtDecreasingSolpe ;
        }
        else if(targetIndexAtIncreasingSolpe != -1 and targetIndexAtDecreasingSolpe == -1){
            return targetIndexAtIncreasingSolpe ;
        }
        return min(targetIndexAtIncreasingSolpe, targetIndexAtDecreasingSolpe) ;
    }
};
```

> Time Complexity - O(3*LogN)

> Space Complexity - O(1)