### Leetcode - 739 - [Daily Temperatures](https://leetcode.com/problems/daily-temperatures/description/) 

* This is similar to [Next Greater Element](https://www.geeksforgeeks.org/problems/next-larger-element-1587115620/1) but with one modification. We will find and store the index of next greater element instead element itself.

* 2 pass Solution

```cpp
class Solution{
public:
    vector<int> dailyTemperatures(vector<int>& temperatures) {
        int back = temperatures.size(), size = temperatures.size() ;
        using _pair = pair<int, int> ;
        stack<_pair> st ;
        while(--back >= 0){
            int currElement = temperatures[back] ;
            while((!st.empty()) and (st.top().first <= currElement)){
                st.pop() ;
            }
            temperatures[back] = (!st.empty()) ? st.top().second : -1 ;
            st.push(make_pair(currElement, back)) ;
        }

        for(int i = 0 ; i < size ; ++i){
            if(temperatures[i] == -1){
                temperatures[i] = 0 ;
            }
            else{
                temperatures[i] -= i ;
            }
        }
        return temperatures ;        
    }
};
```

> Time Complexity - O(2*N)

> Space Complexity - O(1)

---
* 1 pass Solution

```cpp
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& temperatures) {
        int back = temperatures.size(), size = temperatures.size() ;
        using _pair = pair<int, int> ;
        stack<_pair> st ;
        while(--back >= 0){
            int currElement = temperatures[back] ;
            while((!st.empty()) and (st.top().first <= currElement)){
                st.pop() ;
            }
            temperatures[back] = (!st.empty()) ? (st.top().second - back) : 0 ;
            st.push(make_pair(currElement, back)) ;
        }
        return temperatures ;        
    }
};
```

> Time Complexity - O(1*N)

> Space Complexity - O(1)