## Leetcode - 1552 - [Magnectic Force Between Two Balls](https://leetcode.com/problems/magnetic-force-between-two-balls/description/)

* This question is copy of [Aggressive Cows](https://www.geeksforgeeks.org/problems/aggressive-cows/1) and the wording changed. So pasting the same code here.

```cpp
class Solution {
public:
    bool canAssign(vector<int> &stalls, int k, int dist){
        int cows = 1 ;
        int prevStall = stalls[0] ;
        
        for(int i = 1 ; i < stalls.size() ; ++i){
            if((prevStall+dist) <= stalls[i]){
                cows++ ;
                prevStall = stalls[i] ;
            }
        }
        return (cows >= k) ;
    }
    int maxDistance(vector<int>& stalls, int k) {
        sort(begin(stalls), end(stalls)) ;
        int low = 1, high = stalls.back() - stalls.front() ;
        int ans = 1 ;
        
        while(low <= high){
            int mid = low + (high - low)/ 2 ;
            
            if(canAssign(stalls, k, mid)){
                ans = mid ;
                low = mid + 1 ;
            }
            else{
                high = mid - 1 ;
            }
        }
        return ans ;
    }
}; 
```


> Time Complexity - O(NLogN)

> Space Complexity - O(1)