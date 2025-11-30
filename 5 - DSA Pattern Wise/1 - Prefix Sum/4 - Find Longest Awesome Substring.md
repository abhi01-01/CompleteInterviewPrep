#### Leetcode - 1542 - [Find Longest Awesome Substring](https://leetcode.com/problems/find-longest-awesome-substring/)

😳 This problem is same as Leetcode - 1371 [Find the Longest Substring Containing Vowels in Even Counts](https://leetcode.com/problems/find-the-longest-substring-containing-vowels-in-even-counts/description/)


```cpp
class Solution {
public:
    int longestAwesome(string s) {
        unordered_map<char, int> positions = {{'0', 1}, {'1', 2}, {'2', 4}, {'3', 8}, {'4', 16}, {'5', 32}, {'6', 64}, {'7', 128}, {'8', 256}, {'9', 512}} ;
        
        unordered_map<int, int> lastOccurance ;
        int length = s.length(), prefixXor = 0, maxLenSubstr = 0 ;

        // Base case: before processing any character, prefix mask = 0 at index -1
        lastOccurance[prefixXor] = -1 ;
        
        for(int i = 0 ; i < length ; ++i){
            prefixXor ^= positions[s[i]] ;

            // Case 1: Exact same mask seen before → substring(palindromic) has all even counts
            if(lastOccurance.find(prefixXor) == lastOccurance.end()){
                lastOccurance[prefixXor] = i ;
            }
            else{
                maxLenSubstr = max(maxLenSubstr, (i-lastOccurance[prefixXor])) ;
            }
            // Case 2: Check masks that differ by one bit → one odd count allowed
            // if the palindrome length is odd, that is one of the character has odd count
            for(int j = 0 ; j < 10 ; ++j){
                int toggleMask = prefixXor ^ (1 << j) ;
                if(lastOccurance.count(toggleMask)){
                    maxLenSubstr = max(maxLenSubstr, (i-lastOccurance[toggleMask])) ;
                }
            }
        }
        return maxLenSubstr ;
    }
};
```

```cpp
class Solution {
public:
    int longestAwesome(string s) {        
        unordered_map<int, int> lastOccurance ;
        int length = s.length(), prefixXor = 0, maxLenSubstr = 0 ;

        // Base case: before processing any character, prefix mask = 0 at index -1
        lastOccurance[prefixXor] = -1 ;
        
        for(int i = 0 ; i < length ; ++i){
            prefixXor ^= (1 << (s[i] - '0')) ;

            // Case 1: Exact same mask seen before → substring(palindromic) has all even counts
            if(lastOccurance.find(prefixXor) == lastOccurance.end()){
                lastOccurance[prefixXor] = i ;
            }
            else{
                maxLenSubstr = max(maxLenSubstr, (i-lastOccurance[prefixXor])) ;
            }
            // Case 2: Check masks that differ by one bit → one odd count allowed
            // if the palindrome length is odd, that is one of the character has odd count
            for(int j = 0 ; j < 10 ; ++j){
                int toggleMask = prefixXor ^ (1 << j) ;
                if(lastOccurance.count(toggleMask)){
                    maxLenSubstr = max(maxLenSubstr, (i-lastOccurance[toggleMask])) ;
                }
            }
        }
        return maxLenSubstr ;
    }
};
```

> Time Complexity = O(1*N)

> Space Complexity = O(2<sup>10</sup>)

>Approach/Logic
>> #### 1. Initialize:
>>> * prefixMask = `0`(no odd counts yet)
>>> * lastOccurance[0] = `-1` (for handling substrings starting from index 0)
>>
>> #### 2. Iterate each char:
>>> * Toggle `(^=)` the bit representing the current character.
>>> * Now prefixMask tells you which digits have odd occurrences up to i.
>>
>> #### 3. Two cases make a valid palindrome substring:
>>> * If same mask seen before → substring between those indices has all even counts.
>>> * If mask differs by exactly one bit, that means only one digit is odd → still valid for palindrome.
>>
>> #### 4. Track max length across all valid substrings.