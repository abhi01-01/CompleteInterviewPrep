## LC - 1475 - [Final Prices With a Special Discount in a Shop](https://leetcode.com/problems/final-prices-with-a-special-discount-in-a-shop/description/)

```cpp
class Solution {
public:
    vector<int> finalPrices(vector<int>& prices) {
        stack<int> st ;
        int n = prices.size() ;
        for(int i = n-1 ; i >= 0 ; --i){
            while(!st.empty() and st.top() > prices[i]) st.pop() ;

            int curr = prices[i] ;
            if(!st.empty()){
                prices[i] = curr-st.top() ;
            }else{
                prices[i] = curr ;
            }

            st.push(curr) ; 
        }
        return prices ;
    }
};
```

> Time Complexity - O(N)

> Space Complexity - O(1)
