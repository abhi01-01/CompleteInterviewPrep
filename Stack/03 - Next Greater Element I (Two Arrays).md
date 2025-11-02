### Leetcode - 496 - [Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/description/)

```cpp
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& nums1, vector<int>& nums2) {
        unordered_map<int, int> mp ;
        stack<int> st ;
        int back = nums2.size() ;
        while(--back >= 0){
            int currElement = nums2[back] ;
            while(!st.empty() and currElement >= st.top()){
                st.pop() ;
            }
            nums2[back] = (!st.empty()) ? st.top() : -1 ;
            mp[currElement] = nums2[back] ;
            st.push(currElement) ;
        }
        for(int i = 0 ; i < nums1.size() ; ++i){
            nums1[i] = mp[nums1[i]] ;
        }
        return nums1 ;
    }
};
```

> Time Complexity - O(N+M)

> Space Com plexity - O(2*N)