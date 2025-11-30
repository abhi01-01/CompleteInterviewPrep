### Leetcode - 5 - [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/description/)

* __Brute Force__

```cpp
class Solution {
public:
    
    bool ispalindrome( string str ){
        
        int start = 0 , end = str.length()-1 ;
        
        while( start <= end ){
            
            if( str[start] != str[end] ){
                return false ;
            }
            start++ ;
            end-- ;
        }
        
        return true ;
        
    }
    
    
    string longestPalindrome(string s) {
        
        ios_base::sync_with_stdio(false) ;
        cin.tie(NULL) ; 
        
        // create an empty string ans 
        string ans = "" ;
        
        // create all substring
        for( int i = 0 ; i < s.length() ; ++i ){
            
            for( int j = 1 ; j <= (s.length()-i) ; ++j ){
                
                string str = s.substr(i,j) ;
                
                // calc length of substring
                int len = str.length() ;
                
                // if substring is palindromic and length is graeater than ans string, new ans string would be current substring 
                if( ispalindrome(str) and len > ans.length() ){
                    
                    ans = str ;
                    
                }
            }  
        }
        
       return ans ; 
        
    }
};
```

>Time Complexity - O(N<sup>3</sup>)

>Sapce Complexity - O(1)

---

* __Using 2 Pointer Method__

```cpp
class Solution {
public:
    
    string longestPalindrome(string s) {
        
        int max_len = 0 , start = 0 , end = 0 , len = s.length() , startidx = 0 ;
        
        // Base condition
        if( len < 2 ) return s ;
         
        // Seraching substring, if substring is of odd length, considering ith char as middle character of substring, spread substr to both side decrementing start and incrementing end if start'th and end'th char matches
        for( int i = 0 ; i < len-1 ; ++i ){
             start = i , end = i ;
            
            while(start >= 0 and end < len ) {
                if( s[start] == s[end] ){
                    
                    // Taking maximun length's substring
                    if((end-start + 1) > max_len){
                        startidx = start ;
                        max_len = (end-start+1) ;
                    }
                    start-- ;
                    end++ ;
                }else{
                    break ;
                }
                
            }
        }
        
        //// Seraching substring, if substring is of even length, considering ith char as left char of middle char and (i+1)th char as right char of middle element of substring, spread substr to both side decrementing start and incrementing end if start'th and end'th char matches
        
        // i < (len-1), because if i < len, then (i+1) will len, and string's last index is len-1, so len is out of bound index 
        for( int i = 0 ; i < len-1 ; ++i ){
             start = i , end = i+1 ;
            
            while(start >= 0 and end < len ) {
                if( s[start] == s[end] ){
                    
                    // Taking maximun length's substring 
                    if((end-start + 1) > max_len){
                        startidx = start ;
                        max_len = (end-start+1) ;
                    }
                    start-- ;
                    end++ ;
                }else{
                    break ;
                }
                
            }
        }

        return s.substr(startidx, max_len) ;
        
    }
};
```

>Time Complexity - O(N<sup>2</sup>)

>Sapce Complexity - O(1)

---

* __Using 2 Pointer Method Easy and efficient__

```cpp
class Solution {
public:
    void expandLeftAndRight(string& s, int left, int right, int& substrStartIdx, int& longestPalindromeLength){
        while(left >= 0 and right < s.size() and s[left] == s[right]){
            if((right-left+1) > longestPalindromeLength){
                longestPalindromeLength = right - left + 1 ;
                substrStartIdx = left ;
            }
            left-- ;
            right++ ;
        }
    }

    string longestPalindrome(string s) {
        int substrStartIdx = 0, longestPalindromeLength = 0, strLen = s.length() ;
        for(int i = 0 ; i < strLen ; ++i){
            expandLeftAndRight(s, i, i, substrStartIdx, longestPalindromeLength) ; // considering palindromic string of even length
            expandLeftAndRight(s, i, i+1, substrStartIdx, longestPalindromeLength) ; // considering palindromic string of odd length
        }
        return s.substr(substrStartIdx, longestPalindromeLength) ;
    }
};
```

>Time Complexity - O(N<sup>2</sup>)

>Sapce Complexity - O(1)

---

* __Using Dynamic Programming (2D DP)__ 


```cpp
class Solution {
public:
    bool solve(vector<vector<bool>>& dp, int start, int end, string& s){
        if(start == end){
            return dp[start][end] = true ;
        }

        if((end-start) == 1){
            if(s[end] == s[start]){
                return dp[start][end] = true ;
            }
            else{
                return dp[start][end] = false ;
            }
        }

        // s.substr[start.......end] is a palindrome if end chars match and 
        // s.substr[start,start+1.........end-1,end] -> s.substr[start+1..........end-1] is a palindrome, which can be known by dp[start+1][end-1] 
        if(s[start] == s[end] and dp[start+1][end-1] == true){
            return dp[start][end] = true ;
        }
        else{
            return dp[start][end] = false ;
        }
    }

    string longestPalindrome(string s) {
        int n = s.length(), maxLen = 0, subStrStartIdx = 0 ;
        // dp[i][j] denotes s.substr[start, end] (both inclusive) is a palindrome
        vector<vector<bool>> dp(n, vector<bool>(n, false)) ;

        for(int window = 0 ; window < n ; ++window){
            for(int start = 0, end = window ; end < n ; ++start, ++end){
                if(solve(dp, start, end, s)){
                    if((end-start+1) > maxLen){
                        maxLen = end-start+1 ;
                        subStrStartIdx = start ;
                    }
                }
            }
        }

        return s.substr(subStrStartIdx, maxLen) ;
    }
};
```

>Time Complexity - O(N<sup>2</sup>)

>Sapce Complexity - O(N<sup>2</sup>)