# SLIDINNG WINDOW

> Sliding Window is THE pattern for subarray problems.

## 4 TYPES OF SLIDING WINDOWS

### ✅ ***Pattern 1: Fixed-Size Window***

Used when window size k is FIXED.

Clues:
* “Find max sum of subarray of size k”
* “Length EXACTLY k”
* “Compare all windows of size k”

Template

```cpp
int sum = 0, ans = 0;

for (int i = 0; i < n; i++) {
    sum += nums[i];
    if (i >= k) sum -= nums[i - k];
    if (i >= k - 1) ans = max(ans, sum);
}
```

> Problems:
>> * LC 643: Maximum Average Subarray
>> * LC 1052: Grumpy Bookstore Owner
>> * LC 1456: Max Vowels in Substring
>> * LC 1876: Substrings of Size 3 with Distinct Characters


### ✅ ***Pattern 2: Variable-Size Window (Shrink until valid)***

This is the BIG ONE. The real sliding window.

Use WHEN:
* “Smallest subarray”
* “Longest subarray"
* “At most K distinct”
* “Sum ≤ target”

Template

```cpp
int l = 0;

for (int r = 0; r < n; r++) {
    add(nums[r]);

    while (window is invalid)
        remove(nums[l++]);

    update answer;
}
```

Logic:
* Expand right
* Shrink left until valid
* Track best window

> Problems:
>> * LC 3: Longest Substring Without Repeating
>> * LC 76: Minimum Window Substring
>> * LC 904: Fruits Into Baskets
>> * LC 209: Min Size Subarray Sum
>> * LC 713: Subarray Product < K
>> * LC 1658: Min operations to reduce X to zero

### ✅ ***Pattern 3: Sliding Window + Frequency Map***

Used for problems with characters, counts, and “distinct”.

Template

```cpp
unordered_map<char,int> freq;
int l = 0;

for (int r = 0; r < n; r++) {
    freq[s[r]]++;

    while (freq invalid)
        freq[s[l]]--, l++;

    ans = max(ans, r-l+1);
}
```

> Problems:
>> * LC 3: Longest substring w/o repeating chars
>> * LC 76: Minimum Window Substring
>> * LC 159: Longest substring with at MOST 2 distinct
>> * LC 340: At most K distinct
>> * LC 395: At least K repeats in substring

### ✅ ***Pattern 4: Monotonic Sliding Window (Deque Trick)***

Used when problem asks:

* “Maximum in each window”
* “Minimum in each window”
* “Sliding window max/min”

Template

```cpp
deque<int> dq;

for (int i = 0; i < n; i++) {

    while (!dq.empty() && dq.front() <= i-k)
        dq.pop_front();

    while (!dq.empty() && nums[dq.back()] < nums[i])
        dq.pop_back();

    dq.push_back(i);

    if (i >= k-1)
        ans.push_back(nums[dq.front()]);
}
```

> Problems:
>> * LC 239: Sliding Window Maximum
>> * LC 1438: Longest Subarray Absolute Diff ≤ Limit
>> * LC 862: Shortest Subarray With Sum ≥ K

This is the most OP sliding window trick.

---

### <span style="color:yellow">BONUS: Sliding Window + Binary Search</span>

Used when:

* “Longest subarray with constraint > ???”
* Condition is monotonic

Examples:

> * LC 1438: Longest Absolute Difference (with multiset)
> * LC 1004: Longest Ones with Flips

---

### <span style="color:yellow">HOW TO IDENTIFY SLIDING WINDOW PROBLEMS</span>

Look for keywords:

✔️ `“subarray”`<br>
✔️ `“substring”`<br>
✔️ `“continuous” / “contiguous”`<br>
✔️ `“longest” or “shortest”`<br>
✔️ `“at most K”`<br>
✔️ `“sum/product ≤ or ≥ target”`

If ANY of these appear → sliding window.

---

### <span style="color:yellow">CHEAT SHEET</span>

| Pattern         | When                      |
| --------------- | ------------------------- |
| Fixed window    | size is EXACTLY k         |
| Variable window | grow & shrink until valid |
| Freq map window | chars, distinct, repeats  |
| Monotonic deque | sliding min/max problems  |


---

### <span style="color:yellow">PROBLEMS TO MASTER</span>

🟢 Beginner:

> LC 643: Maximum Average Subarray
> 
> LC 1456: Maximum Vowels
> 
> LC 1876: Substring Size 3

🟡 Medium:> LC 3: Longest Substring Without Repeat


> 
> LC 209: Min Size Subarray Sum
> 
> LC 904: Fruits Into Baskets
> 
> LC 76: Minimum Window Substring
> 
> LC 713: Product < K
> 
> LC 1004: Max Consecutive Ones III

🔥 Hard:

> LC 239: Sliding Window Maximum
> 
> LC 862: Shortest Subarray Sum ≥ K
> 
> LC 1438: Longest Absolute Diff
> 
> LC 480: Sliding Window Median