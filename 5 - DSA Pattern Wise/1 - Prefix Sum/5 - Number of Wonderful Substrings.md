## LC - 1915 - [Number of Wonderful Substrings](https://leetcode.com/problems/number-of-wonderful-substrings/description/)

* This question is exact same as Leetcode - 1542 - [Find Longest Awesome Substring](https://leetcode.com/problems/find-longest-awesome-substring/). 


```cpp
class Solution {
public:
    long long wonderfulSubstrings(string& word) {
        unordered_map<int, int> freq ;
        long long count = 0, mask = 0, n = word.size() ;
        freq[0] = 1 ;

        for(int i = 0 ; i < n ; ++i){
            mask ^= (1 << (word[i] - 'a')) ;

            count += freq[mask] ;

            for(int j = 0 ; j < 10 ; ++j){
                int toogleBit = mask ^ (1 << j) ;
                if(freq.count(toogleBit)){
                    count += freq[toogleBit] ;
                }
            }
            freq[mask]++ ;
        }
        return count ; 
    }
};
```


> Time Complexity = O(1*N)

> Space Complexity = O(2<sup>10</sup>)