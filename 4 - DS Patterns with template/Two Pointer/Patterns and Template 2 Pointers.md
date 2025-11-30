# Two Pointers (5 Patterns)

<span style="color:green">If something depends on two ends, continuous range, or linear merging,
→ two pointers is the GOAT.</span>

### ✅ ***Pattern 1 — Opposite Ends (l on left, r on right)***
Use when:
* Array is sorted
* You need to find pairs/quadruples
* You need to minimize/maximize something with two ends

Template:

```cpp
int l = 0, r = n-1;

while (l < r) {
    if (condition) l++;
    else r--;
}
```

> Problems:
>> * LC 167: Two Sum (sorted)
>> * LC 15: 3Sum
>> * LC 16: 3Sum Closest
>> * LC 11: Container With Most Water
>> * LC 42: Trapping Rain Water (variant)

Why it works:<br>
→ Opposite ends give max range → shrink smartly.

### ✅ ***Pattern 2 — Sliding Window Two Pointers (grow + shrink)***

This is two pointers + sliding window fusion.

Used for:
* “smallest window”
* “longest window”
* “at most k”
* “sum/product ≤ target”

Template:
```cpp
int l = 0;

for (int r = 0; r < n; r++) {
    add(nums[r]);

    while (invalid)
        remove(nums[l++]);

    update_answer();
}
```

> Problems:
>> * LC 3: Longest substring without repeating
>> * LC 209: Min Size Subarray Sum
>> * LC 713: Subarray Product < K
>> * LC 1004: Max Consecutive Ones
>> * LC 904: Fruits Into Baskets

This is the most OP pattern in interviews.


### ✅ ***Pattern 3 — Same Direction Two Pointers (Slow + Fast)***

When one pointer chases the other.

Use for:
* grouping
* skipping duplicates
* compressing strings
* cycle detection
* removing elements

Template:
```cpp
int slow = 0;

for (int fast = 0; fast < n; fast++) {
    if (keep(nums[fast]))
        nums[slow++] = nums[fast];
}
```

> Problems:
>> * LC 26: Remove Duplicates from Sorted Array
>> * LC 80: Remove Duplicates II
>> * LC 283: Move Zeroes
>> * Floyd’s cycle detection

Merge two sorted arrays (pointer per array)

### ✅ ***Pattern 4 — K-Sum with Two Pointers (multi-layer)***

Use two pointers inside loops to solve k-sum.

Template:
```cpp
for (i)
    for (j)
        two pointers on remaining range
```

>Problems:
>> * LC 3Sum
>> * LC 4Sum
>> * LC 16: 3Sum Closest
>> * LC 18: 4Sum

This uses sorted array + two pointers to reduce O(n^k) → O(n^(k−1)).


### ✅ ***Pattern 5 — Two Pointers on Two Arrays***

Used for:
* merging
* comparing
* intersecting intervals
* matching smallest pairs

Template:

```cpp
int i = 0, j = 0;

while (i < n && j < m) {
    if (condition) move i++;
    else move j++;
}
```

> Problems:
>> * LC 88: Merge Sorted Array
>> * LC 986: Interval List Intersections
>> * LC 1229: Meeting Scheduler
>> * LC Easy: Intersection of two sorted arrays
>> * LC 455: Assign Cookies

### ***EXTRA — Pattern 6: Pointer Walk on String (parsing)***

Used for substring parsing, comparing string runs.

Template:
```cpp
while (i < n) {
    j = i;
    while (j < n && s[j] == s[i]) j++;

    process s[i..j-1]

    i = j;
}
```

> Problems:
>> * LC 443: String Compression
>> * LC 1592: Rearrange Spaces

----

### <span style="color:yellow">HOW TO KNOW IT’S A TWO POINTERS PROBLEM?</span>

Look for:

✔️ `“sorted array”`<br>
✔️ `“find pair”`<br>
✔️ `“find triplet”`<br>
✔️ `“subarray / substring”`<br>
✔️ `“continuous / contiguous”`<br>
✔️ `“longest / shortest”`<br>
✔️ `“remove in-place”`<br>
✔️ `“merge / intersect”`

If any of these appear → two pointers

----

### <span style="color:yellow">POINTERS PROBLEMS TO MASTER</span>

(ordered from ez → pro)

🟢 Easy:

> LC 26: Remove Duplicates
> 
> LC 283: Move Zeroes
> 
> LC 344: Reverse String
> 
> LC 125: Valid Palindrome

🟡 Medium:

> LC 3: Longest substring without repeating
> 
> LC 167: Two Sum II
> 
> LC 209: Min Size Subarray Sum
> 
> LC 713: Subarray Product
> 
> LC 881: Boats to Save People
> 
> LC 904: Fruits into Baskets
> 
> LC 986: Interval Intersections
> 
> LC 18: 4Sum

🔥 Hard:

> LC 76: Minimum Window Substring (window + map)
> 
> LC 239: Sliding Window Max (deque but mental model = two pointers)
> 
> LC 632: Smallest Range from K Lists



