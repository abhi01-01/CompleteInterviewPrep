### Leetcode - 76 - [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/description/)

```cpp
class Solution{
    public :
    bool windowHasT(unordered_map<char, int>& storeWindow, unordered_map<char, int>& storeT){
        for(auto& it : storeT){
            if(storeWindow.find(it.first) == storeWindow.end()){
                return false ;
            }
            else if(storeWindow[it.first] < it.second){
                return false ;
            }
        }
        return true ;
    }

    string minWindow(string s, string t){
        int start = 0, end = 0, lengthS = s.length(), lengthT = t.length() ;
        unordered_map<char, int> storeT ;
        for(auto& ch : t){
            storeT[ch]++ ;
        }
        int minSubstrWindow = INT_MAX ;
        int minSubstrStartIdx = 0 ;
        unordered_map<char, int> storeWindow ;

        while(end < lengthS and start < lengthS){
            storeWindow[s[end]]++ ;
            int window = (end - start + 1) ;
            while((window >= lengthT) and start <= end and windowHasT(storeWindow, storeT)){
                if(window < minSubstrWindow){
                    minSubstrWindow = window ;
                    minSubstrStartIdx = start ;
                }
                storeWindow[s[start]]-- ;
                start++ ;
                window = (end - start + 1) ; 
            }
            end++ ;
        }
        return (minSubstrWindow == INT_MAX) ? "" : s.substr(minSubstrStartIdx, minSubstrWindow) ;
    }
};
```

> Time Complexity - O(M) + O(26*N)

> Space Complexity - O(26)

---

```cpp
class Solution {
    public:
    string minWindow(string& s, string &t){
        unordered_map<char, int> storage ;
        for(auto& ch : t){
            storage[ch]++ ;
        }

        int start = 0, end = 0, minSubstrLen = INT_MAX, minSubstrStartIdx = -1, lengthS = s.length(), window = 0, lengthT = t.length() ;

        while(end < lengthS){
            if(storage[s[end]] > 0){
                // ensuring that all chars of t appeared in the window
                window++ ;
            }
            storage[s[end]]-- ;
            // when all chars of t appeared in the window 
            if(window == lengthT){
                // start shrinking and from left until window has all chars of string t
                // map[char] == 0, represents, window has all the chars
                while((start < end) and storage[s[start]] < 0){
                    storage[s[start++]]++ ;
                }
                if((end-start+1) < minSubstrLen){
                    minSubstrLen = (end-(minSubstrStartIdx=start)+1) ;
                }
            }
            end++ ;
        }        
        return (minSubstrLen == INT_MAX) ? "" : s.substr(minSubstrStartIdx, minSubstrLen) ;
    }
};
```

> Time Complexity - O(1*N)

> Space Complexity - O(26)