## GFG - [The Painter's Partition Problem](https://www.geeksforgeeks.org/dsa/painters-partition-problem/)

* This qus is as same as GFG - [Allocate Minimum Pages](https://www.geeksforgeeks.org/problems/allocate-minimum-number-of-pages0937/1) just the wordings changed. So using the same code.

```cpp
class Solution {
  public:
      bool check(vector<int>& arr, int k, int pageLimit){
        int students = 1 ;
        int pageSum = 0 ;
        
        for(int i = 0 ; i < arr.size() ; ++i){
            if((pageSum + arr[i]) > pageLimit ){
                students++ ;
                pageSum = arr[i] ;
            }
            else{
                pageSum += arr[i] ;
            }
        }
        return (students <= k) ;
    }
    
    int minTime(vector<int>& arr, int k) {
        // code here
                
        if(k > arr.size()) return -1 ;
        
        int minPageLimit = *max_element(arr.begin(), arr.end()) ;   // which is low
        int maxPageLimit = accumulate(arr.begin(), arr.end(), 0) ;  // which is high
        
        int ans = -1 ;          // to handle -1 condition wla case otherwise we can return high as we used to do
        
        while(minPageLimit <= maxPageLimit){
            
            int mid = minPageLimit + (maxPageLimit - minPageLimit)/2 ;
            
            if(check(arr, k, mid)){
                ans = mid ;
                maxPageLimit = mid - 1  ;
            }
            else{
                minPageLimit = mid + 1 ;
            }
            
        }
        
        return ans ;
    }
};
```

> Time Complexity - O(n × Log(sum(arr) - max(arr)))

> Space Complexity - O(1)