### Leetcode - 57 - [Insert Intervals](https://leetcode.com/problems/insert-interval/description/)


* Approach 1, the easiest way to push the new interval into intervals and then sort it, then call merge interval function.

```cpp
class Solution{
    public :
    vector<vector<int>> merge(vector<vector<int>>& intervals){
        sort(intervals.begin(), intervals.end()) ;
        vector<vector<int>> result ;

        for(int i = 0 ; i < intervals.size() ; ++i){
            if(result.empty() or intervals[i][0] > result.back()[1]){
                result.push_back(intervals[i]) ;
            }
            else{
                result.back()[1] = max(result.back()[1], intervals[i][1]) ;
             }
        }

        return result ;
    }

    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval){
        intervals.push_back(newInterval) ;
        return merge(intervals) ;
    }
};
```

> Time Complexity - O(NLogN)

> Space Complexity - O(N)

---

* Approach 2, Since given intervals is sorted so find the position of newInterval in the intervals arrayn insert the newInterval at that position and then call merge interval function. 

2 pass solution

```cpp
class Solution{
    public :
        vector<vector<int>> merge(vector<vector<int>>& intervals){
        vector<vector<int>> result ;

        for(int i = 0 ; i < intervals.size() ; ++i){
            if(result.empty() or intervals[i][0] > result.back()[1]){
                result.push_back(intervals[i]) ;
            }
            else{
                result.back()[1] = max(result.back()[1], intervals[i][1]) ;
             }
        }

        return result ;
    }

    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval){

        int n = intervals.size(), i = 0 ;

        while(i < n){
            if(intervals[i][0] < newInterval[0]) i++ ;
            else break ;
        }
        intervals.insert(intervals.begin()+i, newInterval) ;

        return merge(intervals) ;
    }
};
```
> Time Complexity - O(N)

> Space Complexity - O(N)

---


* Approach 3, start comparing and mereging simultaneously including newInterval

1 pass Solution

```cpp
class Solution{
    public :
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval){
       vector<vector<int>> result ;

       for(auto const& p : intervals){
        if(p[1] < newInterval[0]){
            result.push_back(p) ;
        }
        else if(newInterval[1] < p[0]){
            result.push_back(newInterval) ;
            newInterval = p ;
        }
        else{
            newInterval[0] = min(newInterval[0], p[0]) ;
            newInterval[1] = max(newInterval[1], p[1]) ;
        }
       }
        result.push_back(newInterval) ;
       return result ; 
    }
};
```

> Time Complexity - O(N)

> Space Complexity - O(N)