# String 

* String originally is not a DS, some patterns are always applied on strings, some common patterns applied on strings are listed below.

## 8 Patterns

### ✅ 1. $Sliding Window on Strings (Frequency Map)$

This is the GOAT pattern for string problems.

Used when problem includes:
* substring
* at most / at least
* repeating / distinct chars
* anagrams
* find window of size k

Template:

```cpp
unordered_map<char,int> mp;
int l = 0;

for (int r = 0; r < n; r++) {
    mp[s[r]]++;
    
    while (window invalid)
        mp[s[l]]--, l++;

    update answer
}
```

> Problems:
>> * LC 3: Longest substring w/o repeating
>> * LC 76: Minimum Window Substring
>> * LC 567: Permutation in String
>> * LC 438: Find All Anagrams
>> * LC 159: At Most 2 Distinct
>> * LC 340: At Most K Distinct

If substring + conditions → sliding window.

### ✅ 2. $Two Pointers on Strings$

Used for:
* palindrome checks
* comparing ends
* trimming
* merging two strings

Template:
```cpp
int l = 0, r = s.size()-1;
while(l < r) {
    if (!valid(s[l], s[r])) return false;
    l++, r--;
}
return true;
```

> Problems:
>> * LC 125: Valid Palindrome
>> * LC 680: Valid Palindrome II
>> * LC 344: Reverse String
>> * LC 392: Is Subsequence
>> * LC 28: StrStr (optimized tricks)

### ✅ 3. $Hashing + Maps (freq / set / scans)$

For checking:
* anagrams
* isomorphic strings
* character frequency
* grouping strings

Template:
```cpp
unordered_map<char,char> mp;
unordered_set<char> used;
for (int i=0;i<n;i++){
    // check mapping consistency
}
```

> Problems:
>> * LC 205: Isomorphic
>> * LC 290: Word Pattern
>> * LC 49: Group Anagrams
>> * LC 409: Longest Palindrome possible
>> * LC 451: Sort Characters By Frequency

### ✅ 4. $String Stack / Decode / Parsing$

Used when:
* parentheses
* encoding like "`2[a3[b]]`"
* removing adjacent duplicates
* evaluating expressions

Template:
```cpp
stack<string> stStr;
stack<int> stNum;
string cur = "";
int num = 0;
```

> Problems:
>> * LC 20: Valid Parentheses
>> * LC 394: Decode String
>> * LC 150: Reverse Polish Notation
>> * LC 227: Basic Calculator

### ✅ 5. $Prefix / Suffix Tricks$

Used for:
* KMP pattern matching
* Z-function
* rolling hash
* detect repeated substring
* prefix-suffix equality

Template (KMP prefix array):
```cpp
vector<int> lps(n);
for (int i=1;i<n;i++){
    while (j>0 && s[i] != s[j]) j = lps[j-1];
    if (s[i] == s[j]) j++;
    lps[i] = j;
}
```

> Problems:
>> * LC 28: Implement strStr
>> * LC 459: Repeated Substring Pattern
>> * LC 1392: Longest Happy Prefix
>> * String searching (KMP/Z)

### ✅ 6. $Trie (Prefix Tree)$

When problem needs:
* prefix matching
* autocomplete
* word dictionary
* wildcard searches

Template:
```cpp
struct Node {
    Node* next[26];
    bool end;
};
```

> Problems:
>> * LC 208: Trie
>> * LC 211: Word Dictionary
>> * LC 648: Replace Words
>> * LC 1268: Search Suggestions System
>> * LC 421: Max XOR using trie

### ✅ 7. $DP on Strings (Subsequence, Substring DP)$

Used for:
* edit distance
* LCS
* palindrome DP
* regex
* wildcard matching

Template:
```cpp
dp[i][j] = result for s1[0..i], s2[0..j]
```

> Problems:
>> * LC 72: Edit Distance
>> * LC 10: Regex Matching
>> * LC 44: Wildcard Matching
>> * LC 516: Longest Palindromic Subsequence
>> * LC 5: Longest Palindromic Substring

### ✅ 8. $Greedy on Strings$

Used for:
* remove smallest chars
* lexicographically smallest
* monotonic stack behavior

Template:
```cpp
while (!st.empty() && st.top() > c && canRemove) st.pop();
st.push(c);
```

> Problems:
>> * LC 316: Remove Duplicate Letters
>> * LC 402: Remove K Digits
>> * LC 1081: Smallest Subsequence of Distinct

---

➡️ Every single string problem on LeetCode is one of these:
* Sliding window
* Two pointers
* Frequency/hash maps
* Stack parsing
* Prefix/suffix arrays (KMP/Z)
* Trie
* String DP
* Greedy lexicographic


➡️ **STRING PATTERN RECOGNITION**

✔️ “substring” → sliding window <br>
✔️ “subsequence” → two pointers OR DP<br>
✔️ “pattern matching” → KMP/Z<br>
✔️ “anagrams / isomorphic” → hashmap<br>
✔️ “decode / parentheses” → stack<br>
✔️ “autocomplete / dictionary” → trie<br>
✔️ “edit / transform” → DP<br>
✔️ “lexicographically smallest” → greedy<br>

---

<span style="color:yellow">***PROBLEMS***</span>

🟢 Easy:

> LC 125: Valid Palindrome
> 
> LC 392: Is Subsequence
> 
> LC 383: Ransom Note

🟡 Medium:

> LC 3: Longest Substring
> 
> LC 5: Longest Palindromic Substring
> 
> LC 49: Group Anagrams
> 
> LC 151: Reverse Words

🔥 Hard:

> LC 10: Regex Matching
> 
> LC 44: Wildcard Matching
> 
> LC 72: Edit Distance
> 
> LC 76: Minimum Window Substring
> 
> LC 30: Substring with Concatenation

