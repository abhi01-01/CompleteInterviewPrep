### Leetcode - 643 - [Maximum Average Subarray I](https://leetcode.com/problems/maximum-average-subarray-i/description/)

```cpp
class Solution {
public:
    double findMaxAverage(vector<int>& nums, int k) {
        int size = nums.size() ;
        double average = 0, maxAverage = std::numeric_limits<double>::lowest();
        int start = 0, end = 0 ;
        while(start < size and end < size){
            average += (double)nums[end] ;
            if((end - start + 1) > k){
                average -= nums[start] ;
                start++ ;
            }
            if((end - start + 1) == k){
                maxAverage = max(maxAverage, average/(end-start+1)) ;
            }
            end++ ;
        }
        return maxAverage ;
    }
};
```

> Time Complexity - O(1*N)

> Space Complexity - O(1)