# HashMap / HashSet (6 Patterns)

If you need to store relationships, counts, or check existence in O(1),
→ HashMap/HashSet is ALWAYS the correct move.

### ✅ $Pattern 1 — Frequency Counting (Counting Occurrences)$

The SINGLE most common use of HashMap.

Used for:
* character counts
* majority element
* anagrams
* duplicates
* comparing two strings/arrays

Template:
```cpp
unordered_map<int,int> freq;

for (auto &x : arr)
    freq[x]++;
```

> Problems:
>> * LC 242: Valid Anagram
>> * LC 383: Ransom Note
>> * LC 347: Top K Frequent
>> * LC 451: Sort Characters by Frequency
>> * LC 594: Longest Harmonious Subsequence

Frequency maps = free wins.

### ✅ $Pattern 2 — Sliding Window With HashMap$

Used when window conditions depend on:
* counts of chars
* number of distinct items
* duplicates
* atMost / atLeast constraints

This is the backbone of most string problems.

Template:

```cpp
unordered_map<char,int> mp;
int l = 0;

for (int r = 0; r < n; r++) {
    mp[s[r]]++;

    while (window invalid)
        mp[s[l]]--, l++;

    update ans;
}
```

> Problems:
>> * LC 3: Longest substring w/o repeat
>> * LC 76: Minimum Window Substring
>> * LC 159/340: At most K distinct
>> * LC 438: Find Anagrams
>> * LC 567: Permutation in String
>> * LC 904: Fruits Into Baskets

This pattern + two pointers = broken OP.

### ✅ $Pattern 3 — HashSet for Uniqueness / Existence Checks$

Used for:
* contains?
* detect cycles / visited states
* unique substrings
* longest consecutive sequence
* check if element seen before

Template:
```cpp
unordered_set<int> st;
if (st.count(x)) doSomething();
st.insert(x);
```

> Problems:
>> * LC 217: Contains Duplicate
>> * LC 128: Longest Consecutive Sequence
>> * LC 349: Intersection of Arrays
>> * LC 202: Happy Number
>> * Detect cycle in graph / recursion

HashSet is the FASTEST existence-check tool in all DS.

### ✅ $Pattern 4 — Grouping Using HashMap (Bucket by Key)$

Used for grouping by:
* anagram signature
* mod
* absolute difference
* sorted hash-key
* frequency patterns
* mapping words to patterns

Template:
```cpp
unordered_map<KeyType, vector<Item>> groups;

for (item : arr) {
    auto key = buildKey(item);
    groups[key].push_back(item);
}
```

> Problems:
>> * LC 49: Group Anagrams
>> * LC 347: Top K Frequent (buckets)
>> * LC 451: Characters by frequency
>> * LC 890: Word Pattern II
>> * LC 30: Substring with Concatenation

HashMap grouping = solve 50% of string problems.

### ✅ $Pattern 5 — Prefix Sum + HashMap (GOAT pattern)$
This pattern is legendary.
Used for any subarray sum / prefix constraint.

Template:
```cpp
unordered_map<int,int> mp;
mp[0] = 1;

int prefix = 0, ans = 0;

for (int x : nums) {
    prefix += x;

    if (mp.count(prefix - k))
        ans += mp[prefix - k];

    mp[prefix]++;
}
```

> Problems:
>> * LC 1: Two Sum (prefix special case)
>> * LC 560: Subarray Sum Equals K
>> * LC 525: Contiguous Array (0/1 trick)
>> * LC 1590: Make Sum Divisible
>> * LC 930: Binary Subarrays With Sum

This is one of the most repeated patterns.

### ✅ $Pattern 6 — Key-Value Mapping (Real world mapping)$

Used for:
* mapping char → char
* mapping original → clone
* tree → parent
* number → next number
* node → metadata
* graph mapping

Template:
```cpp
unordered_map<char,char> mp;
mp[s[i]] = t[i];
```

> Problems:
>> * LC 205: Isomorphic Strings
>> * LC 138: Copy List With Random Pointer
>> * LC 890: Find and Replace Pattern
>> * LC 166: Fraction to Recurring Decimal
>> * LC 359: Logger Rate Limiter

HashMap = flexible relational mapping.

### $BONUS: HashMap as Memo For DP / DFS$

Used for:
* memoizing recursion states
* caching DP states
* caching DFS results

Template:
```cpp
unordered_map<StateType, int> dp;

if(dp.count(state)) return dp[state];

return dp[state] = solve(next);
```
Problems:
> * LC 464: Can I Win
> * LC 139: Word Break
> * LC 377: Combination Sum IV

----

### <span style="color:yellow">HOW TO KNOW IT’S A HASH PROBLEM?</span>

Look for keywords:

✔️ “count”<br>
✔️ “frequency”<br>
✔️ “group items by…”<br>
✔️ “distinct”<br>
✔️ “find subarray with sum…”<br>
✔️ “find any duplicate”<br>
✔️ “mapping from X to Y”<br>
✔️ “check existence fast”<br>
✔️ “O(1) lookup required”<br>
✔️ “sliding window with chars/numbers”

If ANY appear → hash map / hash set is the weapon.

<span style="color:yellow">***HASHMAP SUMMARY***</span>

<span style="color:orange">Use HashMap for:</span>
* frequencies
* prefix sums
* sliding windows
* mapping relationships

<span style="color:orange">Use HashSet for:</span>
* existence check
* visited set
* duplicates
* uniqueness constraints

----

<span style="color:yellow">**PROBLEMS**</span>

🟢 Easy/Medium:

> LC 1: Two Sum
> 
> LC 242: Valid Anagram
> 
> LC 349: Intersection of Arrays
> 
> LC 202: Happy Number
> 
> LC 217: Contains Duplicate

🔥 Medium:

> LC 3: Longest Substring
> 
> LC 49: Group Anagrams
> 
> LC 560: Subarray Sum Equals K
> 
> LC 290: Word Pattern
> 
> LC 451: Sort Characters by Frequency
> 
> LC 904: Fruits Into Baskets

💀 Hard:

> LC 76: Minimum Window Substring
> 
> LC 30: Substring with Concatenation
> 
> LC 138: Copy List Random Pointer
> 
> LC 460: LFU Cache