## Template for modified binary search problems - Modified Binary Search Decision Tree

**🧠 Core Idea**

Modified binary search = binary search applied on something that’s not perfectly sorted, but has structure.

The moment you see a problem that’s not just "find target in sorted array" but still has some patterned monotonic behavior, your brain should yell:

> “Wait — I can probably use binary search with some tweaks.”

<br>
⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️⬇️

<br>

```pgsql
Can define monotonic can() ?
│
├── YES → Binary Search on Answer
│
└── NO
     │
     └── Is data sorted (or partially sorted/ has ordered structure)?
          │
          ├── YES
          │    │
          │    └── problem ask for boundaries / duplicates / first / last occurrence?
          |         |
          │         ├── YES → Boundary Search
          |         |
          │         └── NO  → Is array rotated or mountain-like?
          |             |
          |             ├── If rotated/sorted → Rotated-array / Pivot Search
          |             |
          |             └── If mountain/bitonic → Peak/Valley Search
          └── NO
              |
              └── Continuous/real values?
                    |
                    ├── YES → Binary Search on Real Numbers
                    |
                    └── NO
                        |
                        └── Array/data have monotone-like local structure (bitonic / unimodal)?
                             |
                             ├── YES → Peak/Valley / Bitonic Search (use slope-based logic)
                             |
                             └── NO → binary search likely not appropriate; use other algorithms
```             


### 🧩 STEP 1: Can you define a monotonic property?

> Meaning: as you increase or decrease something, the answer flips from “false → true” (or vice versa)?

✅ Yes → Binary Search on Answer (BSOA)<br>
## ❌ No → Go to Step 2


### CASE 1: Binary Search on Answer

> Typical phrasing:
>>
>> * “Find the minimum X that satisfies ___”<br>
>> * “Find the maximum speed/time/weight that still works”

> Examples:
>>
>> * Koko Eating Bananas 🍌 (canEat(mid) → true/false)
>>
>> * Allocate books / painters (can(mid) → true/false)
>>
>> * Minimize max distance, minimize time, maximize value under limit

💡 Key pattern: Search over numeric range, not array indices.

✅ Template:

```cpp
int l = low, r = high, ans;
while (l <= r) {
    int mid = l + (r - l) / 2;
    if (condition(mid)) {
        ans = mid;  // candidate
        r = mid - 1; // minimize
    } else l = mid + 1;
}
return ans;
```
---

### 🧩 STEP 2: Is the data sorted or partially sorted?

✅ Yes → Rotated / Modified Sorted Array
## ❌ No → Step 3


### CASE 2: Rotated or Partially Sorted Array

>Typical phrasing:
>>
>> * “Array is sorted but rotated”,
>> * “Search in a mountain array”,
>> * “Find pivot / smallest element”.

> Examples:
>> 
>> * Search in rotated sorted array
>> 
>>  * Find min in rotated sorted array
>> 
>> * Peak element in mountain array


💡 Key concept: One half is always monotonic → you can safely discard one side.

✅ Template:

```cpp
int l = 0, r = n - 1;
while (l < r) {
    int mid = (l + r) / 2;
    if (nums[mid] > nums[r]) l = mid + 1; // right unsorted
    else r = mid; // left unsorted
}
return nums[l]; // min element
```
---

### 🧩 STEP 3: Is the data sorted with duplicates or boundaries?

✅ Yes → Boundary Binary Search
## ❌ No → Step 4

### CASE 3: Boundary Search

>Typical phrasing:
>> 
>> * “Find first/last occurrence”,
>> * “Find lower/upper bound”,
>> * “Find smallest element ≥ target”.

> Examples:
>> 
>> * Lower bound / upper bound
>> 
>> * First and last position of target
>> 
>> * Insert position problems

✅ Template:

```cpp
int l = 0, r = n - 1, ans = -1;
while (l <= r) {
    int mid = (l + r) / 2;
    if (nums[mid] >= target) {
        ans = mid;
        r = mid - 1; // move left
    } else l = mid + 1;
}
return ans;
```

💡 Key concept: You store the result and keep exploring left/right.

---

### 🧩 STEP 4: Is the function monotonic but continuous (real values)?

✅ Yes → Binary Search on Real Numbers
## ❌ No → Step 5

### CASE 4: Continuous / Real Binary Search

>Typical phrasing / how to recognize these magically:
>>
>> * Find square root
>> * Find minimal error point
>> * Find time when two functions meet
>> * minimum radius
>> * minimum distance
>> * minimum max gap
>> * minimum precision
>> * find smallest t such that something is possible
>> * minimize the maximum …
>> * max average with floating conditions

> Examples:
>>
>> * Square Root / Nth Root of a Number
>> * Divide two numbers without using division
>> * Find peak of a polynomial / continuous function
>> * Minimize function value
>> * <mark>LeetCode 644 — Maximum Average Subarray II</mark> 
>> * <mark>LeetCode 774 — Minimize Max Distance to Gas Station</mark>
>> * Find minimal radius so all points are covered
>> * Find minimum time for machine to finish tasks (continuous time)
>> * <mark>Minimum radius heaters (real-valued)</mark>
>> * Minimize the maximum pairwise distance to form K clusters
>> * Place K centers such that max distance of any point to nearest center is minimized
>> * Find the smallest radius R to fully enclose polygon points around a circle
>> * Find the smallest radius R to fully enclose polygon points around a circle
>> * Frog jump across stones with minimum max jump
>> * Meeting point in 2D that minimizes max distance to all points
>> * Minimum speed / minimum radius with obstacles (advanced computational geometry)
>> * Find intersection in physics/time problems

✅ Template:

```cpp
double l = 0, r = target, eps = 1e-6;
while (r - l > eps) {
    double mid = (l + r) / 2;
    if (mid * mid < target) l = mid;
    else r = mid;
}
return l;
```

Key concept: Stop when range < ε (tolerance).

---

### 🧩 STEP 5: Is there a bitonic or peak structure?

✅ Yes → Peak / Valley Search

> Examples:
>>
>> * Peak element (LeetCode 162)
>> 
>> * Mountain array (LeetCode 1095)

✅ Template:

```cpp
int l = 0, r = n - 1;
while (l < r) {
    int mid = (l + r) / 2;
    if (nums[mid] < nums[mid + 1]) l = mid + 1;
    else r = mid;
}
return l; // index of peak
```

💡 Key concept: You always move towards the higher slope.


