### Leetcode - 503 - [Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/description/)

```cpp
class Solution {
public:
    vector<int> nextGreaterElements(vector<int>& nums) {
        int start = 0, end = nums.size()-1 ;
        int maxElementIdx = 0, maxElement = INT_MIN ;
        // maximum element wouldn't have any greater element, that's why we are finding max elememt
        while(start <= end){
            if(nums[start] > maxElement){
                maxElementIdx = start ;
                maxElement = nums[start] ;
            }
            if(nums[end] > maxElement){
                maxElementIdx = end ;
                maxElement = nums[end] ;
            }
            start++ ;
            end-- ;
        }
        
        stack<int> st ;
        int n;
        int size = n = nums.size() ;
        // assume maximum element is rightmost num, so start finding next greater element for its left side elements
        // n - finding next greater element for all numbers of nums, same as next greater element
        while(n > 0){
            if(maxElementIdx < 0){
                maxElementIdx = (size + maxElementIdx) ;
            }
            int currElement = nums[maxElementIdx] ;
            while(!st.empty() and currElement >= st.top()){
                st.pop() ;
            }
            nums[maxElementIdx] = (!st.empty()) ? st.top() : -1 ;
            st.push(currElement) ;
            maxElementIdx-- ;
            n-- ;
        }
        return nums ;
    }
};
```

> Time Complexity - O(2*N)

> Space Complexity - O(1*N)