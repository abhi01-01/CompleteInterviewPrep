### Leetcode - 215 - [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/description/)

* Using Sorting

```cpp
class Solution{
public :
    int findKthLargest(vector<int>& nums, int k) {
     sort(nums.begin(), nums.end()) ;
     return nums[nums.size()-k] ;   
    }
};
```

> Time Complexity - O(NLogN)

> Space Complexity - O(N)

* Using Min heap

```cpp
class Solution{
public :
    int findKthLargest(vector<int>& nums, int k) {
        priority_queue<int, vector<int>, greater<int>> minHeap ;
        for(auto const& num : nums){
            minHeap.push(num) ;
            if(minHeap.size() > k)
                minHeap.pop() ; 
        }
        return minHeap.top() ;
    }
};
```

> Time Complexity - O(NLogk)

> Space Complexity - O(N)