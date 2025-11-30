## LC - 1190 - [Reverse Substrings Between Each Pair of Parentheses](https://leetcode.com/problems/reverse-substrings-between-each-pair-of-parentheses/description/)

```cpp
class Solution {
public:
    string reverseParentheses(string s) {
        stack<int> st ;
        int n = s.length() ;
        for(int i = 0 ; i < n ; ++i){
            if(s[i] == '('){
                st.push(i) ;
            }
            else if(s[i] == ')'){
                int idx = st.top() ;
                st.pop() ;
                reverse(s.begin()+idx, s.begin()+i) ;
            }
        }
        int low = 0, high = 0 ;
        while(high < n){
            if(s[high] != '(' and s[high] != ')'){
                s[low] = s[high] ;
                low++ ;
            }
            high++ ;
        }
        return s.substr(0, low) ;
    }
};
```

> Time Complexity - O(N<sup>2</sup>)

> Space Complexity - O(N)

* The Optimization is a very elementry approach which is rarely used. [Pattern](https://leetcode.com/problems/reverse-substrings-between-each-pair-of-parentheses/editorial/) 🙃😬