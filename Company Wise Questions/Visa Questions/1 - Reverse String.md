>## Problem 
>>### you're given a string word, you can reverse the order of some characters from the begining or from the end of the word to get new strings. Your task is to iterate all possible new strings that can be formed this way, answer return the alphabetically smallest one.
<br>

>## Solution
>> 🧠 Key Insight<br>
>>Reversing a prefix or a suffix any number of times means:
>>> * You can rearrange characters to a limited extent, but not arbitrarily.
>>> * The best way to reason is:<br>
Try all possible prefix reversals and all possible suffix reversals once — because multiple reversals beyond that can be simulated by some single prefix/suffix reversal.
>>
>> So, for a given string s, possible strings come from:
>>> 1. Reversing prefix [0..i] → reverse(s.begin(), s.begin()+i)
>>> 2. Reversing suffix [i..n-1] → reverse(s.begin()+i, s.end())
>>
>> Then choose the alphabetically smallest among them.<br>

#### Example
```cpp
s = "dbca"

Possible reversals:
- reverse prefix(1): "dbca"
- reverse prefix(2): "bdca"
- reverse prefix(3): "cbda"
- reverse prefix(4): "acbd"

- reverse suffix(1): "dbca"
- reverse suffix(2): "dbac"
- reverse suffix(3): "dacb"
- reverse suffix(4): "acbd"

Smallest = "acbd"
```
### Code
#### This approach is O(n²) in naive form but can be optimized to O(n) space and O(n log n) time easily, since each reversal and comparison is O(n).

```cpp
class Solution{
    public :
    string SmallestReversalString(string s){
        string best = s ;
        int n = s.size() ;

        // try reversing each prefix
        for(int i = 1 ; i <= n ; ++i){
            string temp = s ;
            reverse(temp.begin(), temp.begin()+i) ;
            best = min(best, temp) ;
        }

        // try revrsing each suffix

        for(int i = 0 ; i < n ; ++i){
            string temp = s ;
            reverse(temp.begin() + i, temp.end()) ;
            best = min(best, temp) ;
        }

        return best ;
    }
};
```

>Time Complexity - O(N<sup>2</sup>)

>Space Complexity - O(1)

---

```cpp
class Solution{
    public :

    bool isBetter(const string& s, int n, bool isPrefix, int k, const string& best){
        // compare lexicographically for each index
        for(int i = 0 ; i < n ; ++i){
            char c1 ;
            if(isPrefix){
                // prefix reversed [0....k] rest same
                c1 = (i <= ) ? s[k-i] : s[i] ;
            }
            else{
                // suffix reversed [k....n-1]
                c1 = (i < k) ? s[i] : s[n-1-(i-k)] ;
            }
            char c2 = best[i] ;
            if(c1 < c2) return true ;
            if(c1 > c2) return false ;
        }
        return false ; // equal 
    }

    string SmallestReversalString(string s){
        int n = s.size() ;
        string best = s ;

        // try all prefix reversal 
        for(int k = 1 ; k <= n ; ++k){
            if(isBetter(s, n, true, k, best)){
                string temp = s ;
                reverse(temp.begin(), temp.begin()+k) ;
                best = temp ;
            }
        }

        // try all suffix reversal

        for(int k = 0 ; k < n ; ++k){
            if(isBetter(s, n, false, k, best)){
                string temp = s ;
                reverse(temp.begin()+k, temp.end()) ;
                best = temp ;
            }
        }
        return best ;
    }
};
```

>Time Complexity - O(NlogN)

>Space Complexity - O(1)

---

```cpp
class Solution{
    public :

    string buildPrefix(const string& s, int i){
        string t = s ;
        reverse(t.begin(), t.begin()+i+1) ;
        return t ;
    }

    string buildSuffix(cosnt string& s, int i){
        string t = s ;
        reverse(t.begin()+i, t.end()) ;
        return t ;
    }

    string smallestReversalString(string s){
        int n = s.size() ;
        char mn = *min_element(s.begin(), s.end()) ;

        string best = s ;   // Initial Candidate

        for(int i = 0 ; i < n ; ++i){
            if(s[i] == mn){
                // Case 1: reverse prefix to bring s[i] front
                best = min(best, buildPrefix(s, i)) ;
                // Case 2: reverse suffix to bring s[i] front
                best = min(best, buildSuffix(s, i)) ;
            }
        }
        return best ;
    }
};

>Time Complexity - O(N)

>Space Complexity - O(1)
