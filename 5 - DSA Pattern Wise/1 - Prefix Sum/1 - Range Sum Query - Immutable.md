### Leetcode - 303 - [Range Sum Query - Immutable](https://leetcode.com/problems/range-sum-query-immutable/description/)

```cpp
class NumArray {
public:
    vector<int> prefix_sum ;
    NumArray(vector<int>& nums) {
        int sum = 0, size = nums.size() ;
        prefix_sum.resize(size, 0) ;
        prefix_sum[0] = nums[0] ;
        for(int i = 1 ; i < size ; ++i){
            prefix_sum[i] = (prefix_sum[i-1] +nums[i]) ;
        }
    }
    
    int sumRange(int left, int right) {
        return ((left-1) >= 0) ? (prefix_sum[right]-prefix_sum[left-1]) : prefix_sum[right] ;
    }
};

/**
 * Your NumArray object will be instantiated and called as such:
 * NumArray* obj = new NumArray(nums);
 * int param_1 = obj->sumRange(left,right);
 */
 ```