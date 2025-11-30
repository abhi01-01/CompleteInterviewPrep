### Leetcode - 852 - [Peak Index In a Mountain Array](https://leetcode.com/problems/peak-index-in-a-mountain-array/description/)

```cpp
class Solution{
    public:
    int peakIndexMountainArray(vector<int>& arr){
        int low = 0, high = arr.size()-1 ;
        while(low < high){
            int mid = low + (high - low)/2 ;
            if(arr[mid+1] > arr[mid]){
                low = mid + 1 ;
            }
            else{
                high = mid ;
            }
        }
        return high ;
    }
};
```

> Time Complexity - O(LogN)

> Space Complexity - O(1)