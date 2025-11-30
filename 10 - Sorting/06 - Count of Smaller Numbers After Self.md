### Leetcode - 315 - [Count of Smaller Numbers After Self](https://leetcode.com/problems/count-of-smaller-numbers-after-self/description/)

* Brute Force Approach

```cpp
class Solution{
    public :
    vector<int> countSmaller(vector<int>& nums) {
        int size = nums.size() ;
        for(int i = 0 ; i < size ; ++i){
            int count = 0 ;
            for(int j = i+1 ; j < size ; ++j){
                if(nums[j] < nums[i]){
                    count++ ;
                }
            }
            nums[i] = count ;
        }
        return nums ;
    }
};
```

> Time Complexity - O(N<sup>2</sup>)

> Space Complexity - O(1)

---

```cpp
class Solution{
    public :
    
};