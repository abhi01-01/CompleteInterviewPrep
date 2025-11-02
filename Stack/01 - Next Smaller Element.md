### GFG - [Next Smaller Element](https://www.geeksforgeeks.org/problems/immediate-smaller-element1142/1)


```cpp
    vector<int> nextSmallerEle(vector<int>& arr) {
        //  code here
        for(int i = 0 ; i < arr.size() ; ++i){
            int j = i+1 ;
            for( ; j < arr.size() ; ++j){
                if(arr[j] < arr[i]){
                    arr[i] = arr[j] ;
                    break ;
                }
            }
            if(j == arr.size()){
                arr[i] = -1 ;
            }
        }
        return arr ;
    }
```
> Time Complexity - O(N*N)

> Space Complexity - O(1)

---

```cpp
    vector<int> nextSmallerEle(vector<int>& arr) {
        //  code here
        stack<int> st ;
        int back = arr.size() - 1 ;
        
        while(back >= 0){
            int currElement = arr[back] ;
            while(!st.empty() and currElement <= st.top()){
                st.pop() ;
            }
            
            if(!st.empty() and currElement > st.top()){
                arr[back] = st.top() ;
            }
            else{
                arr[back] = -1 ;
            }
            st.push(currElement) ;
            --back ;
        }
        return arr ;
    }
```

> Time Complexity - O(1*N)

> Space Complexity - O(1*N)

---

```cpp
class Solution {
  public:
    vector<int> nextSmallerEle(vector<int>& arr) {
        //  code here
        stack<int> st ;
        int back = arr.size() ;
        
        while(--back >= 0){
            int currElement = arr[back] ;
            while(!st.empty() and currElement <= st.top()){
                st.pop() ;
            }
            arr[back] = (!st.empty()) ? st.top() : -1 ;
            st.push(currElement) ;
        }
        return arr ;
    }
};
```

> Time Complexity - O(1*N)

> Space Complexity - O(1*N)