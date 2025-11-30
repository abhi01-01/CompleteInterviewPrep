## GFG - [Aggressive Cows](https://www.geeksforgeeks.org/problems/aggressive-cows/1)

* This question is same as GFG - [Minimize Max Distance to Gas Station](https://www.geeksforgeeks.org/problems/minimize-max-distance-to-gas-station/1)


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
    
    int aggressiveCows(vector<int> &stalls, int k) {
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