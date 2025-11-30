### GFG - [Next Greater Element](https://www.geeksforgeeks.org/problems/next-larger-element-1587115620/1)

```cpp
class Solution {
  public:
    vector<int> nextLargerElement(vector<int>& arr) {
        // code here
        int size = arr.size() ;
        
        for(int i = 0 ; i < size ; ++i){
            int j = i+1 ;
            for( ; j < size ; ++j){
                if(arr[j] > arr[i]){
                    arr[i] = arr[j] ;
                    break ;
                }
            }
            if(j == size){
                arr[i] = -1 ;
            }
        }
        return arr ;
    }
};
```

> Time Complexity - O(N*N)

> Space Complexity - O(1)

---

```cpp
class Solution {
  public:
    vector<int> nextLargerElement(vector<int>& arr) {
        // code here
        stack<int> st ;
        int back = arr.size() ;
        
        while(--back >= 0){
            int currElement = arr[back] ;
            
            while(!st.empty() and currElement >= st.top() ){
                st.pop() ;
            }
            arr[back] = (!st.empty()) ? st.top() : -1 ;
            st.push(currElement) ;
        }
        return arr ;
    }
};
```
__Next Larger Element is as same as Next Smaller Element except this `currElement >= st.top()` case `<=` turns to `>=` int Next Larger Element__

> Time Complexity - O(1*N)

> Space Complexity - O(1*N)