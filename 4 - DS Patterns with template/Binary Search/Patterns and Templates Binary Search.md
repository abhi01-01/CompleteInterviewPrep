# Binary Search (6 Patterns)

If answer lives on a monotonic line (sorted array or sorted feasibility),<br>
→ binary search

### ✅ $Pattern 1 — Classic Binary Search (Exact Value)$

The OG pattern.

Used when:

* array is sorted
* find element / index

Template:
```cpp
int l = 0, r = n-1;

while (l <= r) {
    int mid = l + (r-l)/2;

    if (a[mid] == target) return mid;
    else if (a[mid] < target) l = mid + 1;
    else r = mid - 1;
}
return -1;
```

> Problems
>> * LC 704: Binary Search
>> * LC 35: Search Insert Position
>> * LC 744: Next Greatest Letter

This is the “tutorial” pattern.

### ✅ $Pattern 2 — Binary Search on Answer (BS on feasible region)$

This is the REAL interview pattern.

Used when:
* answers lie in a numeric range
* you must check feasibility
* monotonic yes/no function exists

Template:
```cpp
int l = low, r = high;

while (l < r) {
    int mid = l + (r-l)/2;

    if (can(mid)) r = mid;   // search left
    else l = mid + 1;        // search right
}
return l;
```

Clues:
* “minimum time”
* “minimum speed”
* “max distance <= X?”
* “can finish with K workers?”
* “can we split into <= m subarrays?”

> Problems:
>> * LC 875: Koko Eating Bananas
>> * LC 1011: Ship Packages
>> * LC 410: Split Array Largest Sum
>> * LC 1482: Bouquet flowers
>> * LC 1552: Magnetic force
>> * LC 774: Minimize Max Distance
>> * GFG: Allocate minimum pages

This is the KING pattern.

### ✅ $Pattern 3 — Binary Search on Leftmost/Rightmost Bound (Lower/Upper Bound)$

Used to find:
* first occurrence
* last occurrence
* boundary where condition changes

Template (lower bound)
```cpp
int l = 0, r = n; // r = n to allow return n
while (l < r) {
    int mid = (l+r)/2;
    if (a[mid] >= target) r = mid;
    else l = mid + 1;
}
return l; // first index >= target
```

Template (upper bound)
```cpp
while (l < r) {
    int mid = (l+r)/2;
    if (a[mid] > target) r = mid;
    else l = mid + 1;
}
return l; // first index > target
```

> Problems:
>> * LC 34: First and Last Position
>> * Lower bound / upper bound usage
>> * Find first bad version (LC 278)
>> * Insert position problems

### ✅ $Pattern 4 — Binary Search on Rotated Sorted Array$

Trick to handle rotated + sorted arrays.

Rule:
* One of the halves is always sorted.
* Binary search which half target lies in.

Template:
```cpp
if (nums[l] <= nums[mid]) {
    if (nums[l] <= target && target <= nums[mid]) r = mid-1;
    else l = mid+1;
} else {
    if (nums[mid] <= target && target <= nums[r]) l = mid+1;
    else r = mid-1;
}
```

> Problems:
>> * LC 33: Search in Rotated Sorted
>> * LC 81: Search Rotated with Duplicates
>> * LC 153/154: Find Min in Rotated
>> * 1D geometry on nums = rotated search.

### ✅ $Pattern 5 — Binary Search on Real Numbers (BS on double)$

Used when searching for floating-point values.

Clues:
* “precision = `1e-6`”
* “minimize maximum distance”
* “find minimum radius”

Template:
```cpp
double l = 0, r = 1e9;

for (int i = 0; i < 80; i++) {
    double mid = (l + r) / 2.0;
    if (can(mid)) r = mid;
    else l = mid;
}
return l;
```

> Problems:
>> * LC 644: Maximum Average Subarray
>> * LC 1552: Magnetic Force (double version)
>> * LC 2343 (precision tasks)
>> * GFG: Minimize Max Distance Between Gas Stations

Binary search doesn’t care about ints/doubles — monotonicity is key.

### ✅ $Pattern 6 — Binary Search on Function (Parametric Search)$

You binary search on a parameter used inside a function.

Used when:
* sorting + searching inside
* prefix conditions
* constraints create monotonic behaviour

Example: `Find smallest x such that f(x) >= K.`

> Used in:
>> * LC 1760: Minimum Limit of Balls
>> * LC 1283: Find Smallest Divisor
>> * LC 1870: Min Speed to Arrive on Time

Template:
```cpp
int l = 1, r = maxLimit;

auto good = [&](int x){
    return f(x) <= threshold;
};

while (l < r) {
    int mid = (l+r)/2;
    if (good(mid)) r = mid;
    else l = mid+1;
}
```
----

### <span style="color:yellow">HOW TO KNOW IT’S A BINARY SEARCH PROBLEM?</span>

Check these signs:

✔️ answer lies in a continuous numeric range<br>
✔️ want min X such that `condition(c) == true` <br>
✔️ want max X such that `condition(c) == true` <br>
✔️ monotonic pattern:
1. can(1) = false
2. can(2) = true
3. can(3) = true<br>
=> binary search

✔️ sorted array involved <br>
✔️ rotated sorted array <br>
✔️ search space too large for brute force <br>
✔️ “minimize maximum” / “maximize minimum” <br>
✔️ double precision question

If ANY of these show → it’s binary search.


----

### <span style="color:yellow">3 Major Templates</span>


Binary Search for Min Feasible Value
```cpp
if (can(mid)) r = mid;
else l = mid + 1;
```

Binary Search for Max Feasible Value
```cpp
if (can(mid)) l = mid;
else r = mid - 1;
```

Bounded Binary Search (positions)
```cpp
while (l < r) {
    mid = (l+r)/2;
    if (a[mid] >= target) r = mid;
    else l = mid+1;
}
```

These 3 solve 95% of problems.


----

### <span style="color:yellow">PROBLEMS</span>
🟢 Easy:

> LC 704
> 
> LC 35
> 
> LC 69 (sqrt)
> 
> LC 278 (first bad version)

🟡 Medium:

> LC 33, 81 (rotated)
> 
> LC 153, 154 (find min rotated)
> 
> LC 34 (first/last pos)
> 
> LC 74/240 (search matrix)
> 
> LC 875: Koko Bananas
> 
> LC 1011: Ship Packages
> 
> LC 162: Peak Element

🔥 Hard:

> LC 410: Split Array
> 
> LC 887: Egg Drop (binary search on dp)
> 
> LC 1552: Magnetic Force
> 
> LC 774: Minimize Max Distance
> 
> LC 668: Kth Smallest in Multiplication Table