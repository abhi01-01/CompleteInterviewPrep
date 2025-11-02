### Leetcode - 3 - [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/description/)

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        vector<int> hash(257, 0);
        int start = 0, end = 0, longest_len_substr = 0, str_len = s.length() ;

        while(end < str_len ){
            hash[s[end]]++ ;
            while(start < end and hash[s[end]] > 1){
                hash[s[start++]]-- ;
            }
            longest_len_substr = max(end-start+1, longest_len_substr) ;
            end++ ;
        }
        return longest_len_substr ;
    }
};
```

>Time Complexity - O(1*N)

>Space Complexity - O(1)