### Leetcode - 347 - [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/description/)


```cpp
class Solution{
public :
    int topKFrequentElements(vector<int>& nums, int k){
        unordered_map<int, int> count ;
        for(auto const& num : nums){
            count[num]++ ;
        }
        // <frequency, num>
        using _pair = pair<int, int> ;
        priority_queue<_pair, vector<_pair>, greater<_pair>> minHeap ;

        for(auto const& p : count){
            minHeap.push({p.second, p.first}) ;
            if(minHeap.size() > k){
                minHeap.pop() ;
            }
        }
        vector<int> result ;
        
        while(!minHeap.empty()){
            int ele = minHeap.top().second ;
            result.push_back(ele) ;
            minHeap.pop() ;
        }
        return result ;
    }
};
```

> Time Complexity - O(NLogK) 

> Space Complexity - O(N)