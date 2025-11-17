### Leetcode 56 - [Merge Intervals](https://leetcode.com/problems/merge-intervals/description/)

* Solution 1

```cpp
class Solution{
    public :
    vector<vector<int>> merge(vector<vector<int>>& intervals){
        sort(intervals.begin(), intervals.end()) ;
        vector<vector<int>> result ;
        int i = 0, n = intervals.size() ;
        while(i < n){
            int a1 = intervals[i][0] ;
            bool flag = true ;
            int a2 = intervals[i][1] ;
            while(flag and (i+1) < n){
                if(a2 >= intervals[i+1][0]){
                    i++ ;
                    a2 = max(a2, intervals[i][1]) ;
                }
                else{
                    flag = false ;
                }
            }
            result.push_back({a1, a2}) ;
            i++ ;
        }
        return result ;
    }
};
```

* Solution 2

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        sort(intervals.begin(), intervals.end()) ;
        vector<vector<int>> ans ;
        for(auto& ele : intervals){
            if(ans.empty() or ele[0] > ans.back()[1] ){
                ans.push_back(ele) ;
            }
            else{
                ans.back()[1] = max(ans.back()[1], ele[1]) ;
            }
        }
        return ans ;
    }
};
```

> Time Complexity - O(NLogN)

> Space Complexity - O(N)
