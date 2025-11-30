# Intervals(7 Patterns)

### ✅ ***Pattern 1 — Merge Intervals***

If intervals overlap → merge into one.

Template
```cpp
sort(intervals.begin(), intervals.end()); // by start
vector<vector<int>> ans;

for (auto &it : intervals) {
    if (ans.empty() || ans.back()[1] < it[0])
        ans.push_back(it);
    else
        ans.back()[1] = max(ans.back()[1], it[1]);
}
```

> Problems:
>> * LC 56: Merge Intervals
>> * LC 986: Interval Intersection
>> * LC 1288: Remove Covered Intervals
>> * LC 57: Insert Interval

Key idea:
Sort by start → merge greedily.

### ✅ ***Pattern 2 — Non-overlapping Intervals (Greedy by End Time)***

* Find max non-overlapping intervals.
* Classic interval scheduling.

Rule: pick earliest ENDING interval

```cpp
sort(intervals by end);
take interval if start >= lastEnd;
```

> Problems:
>> * LC 435: Non-overlapping Intervals
>> * LC 452: Min Arrows to Burst Balloons
>> * LC 1024: Video Stitching



### ✅ ***Pattern 3 — Minimum Number of Meeting Rooms (Sweep Line / PQ)***

Intervals where multiple run at the same time.

$Sweep Line Template:$
```cpp
vector<int> start, end;
sort(start); sort(end);

i = j = rooms = 0;

while(i < n) {
    if(start[i] < end[j]) rooms++, i++;
    else j++, i--;
}
```

$PQ-Template (classic):$

```cpp
sort(intervals by start);
priority_queue<int, vector<int>, greater<int>> pq;

for(interval):
    if (!pq.empty() && pq.top() <= interval.start)
        pq.pop();
    pq.push(interval.end);
```

> Problems:
>> * LC 253: Meeting Rooms II
>> * LC 759: Employee Free Time


### ✅ ***Pattern 4 — Interval Containment (Cover / Inside / Outside)***

Check if one interval fully contains another.

Template:
```cpp
sort by start ascending, end descending
```

> Problems:
>> * LC 1288: Remove Covered Intervals
>> * LC 715: Range Module (hard)


### ✅ ***Pattern 5 — Interval Intersection (Two Pointers)***
When given two sorted interval lists.

Template:
```cpp
i = j = 0;

while (i<n && j<m) {
    int l = max(a[i].start, b[j].start);
    int r = min(a[i].end,   b[j].end);

    if (l <= r) ans.push_back({l, r});

    if (a[i].end < b[j].end) i++;
    else j++;
}
```

> Problems:
>> * LC 986: Interval List Intersections
>> * LC 1229: Meeting Scheduler



### ✅ ***Pattern 6 — Interval Greedy + Heap (Scheduling)***

When tasks must be done before deadlines.

🔥 Template:
```cpp
sort by end time
push duration in max-heap
if totalTime > deadline → pop largest task
```

> Problems:
>> * LC 630: Course Schedule III
>> * Hard scheduling problems


This is one of the most OP greedy+interval tricks.

### ✅ ***Pattern 7 — Interval DP (Interval → DP[l][r])***
Game theory, max score, merging cost → interval DP.

Template:
```cpp
for(len=2..n):
  for(l=0..n-len):
    r=l+len-1
    dp[l][r] = best split on k in [l..r]
```

> Problems:
>> * LC 375: Guess Number Higher or Lower II
>> * LC 312: Burst Balloons
>> * LC 1547: Minimum Cost to Cut Stick
>> * Stone Game series


This is your boss-tier interval pattern.

---

### <span style="color:yellow">HOW TO RECOGNIZE INTERVAL PROBLEMS</span>

Look for:
✔️ start & end <br>
✔️ overlap / non-overlap<br>
✔️ meeting rooms<br>
✔️ schedule tasks / deadlines<br>
✔️ continuous segments<br>
✔️ merge / split ranges<br>
✔️ DP on ranges `(l,r)`<br>

If ANY appear → it’s an interval problem.

<span style="color:orange">PRINT THIS IN YOUR BRAIN</span>

✔️ Overlap detection
```perl
if (a.start <= b.end AND b.start <= a.end)
```
✔️ Merge rule
```perl
newEnd = max(a.end, b.end)
```
✔️ Best picking rule
```perl
Pick earliest finishing interval.
```
✔️ Two pointers for interval lists
```perl
Whichever ends first → move pointer.
```
✔️ Meeting Rooms
```perl
PQ of end times.
```
✔️ Hard problems
```ini
Use interval DP (dp[l][r]).
```


----

### <span style="color:yellow">PROBLEMS<span>

🟢 Easy/Medium:

> * LC 56: Merge Intervals
> * LC 57: Insert Interval
> * LC 252: Meeting Rooms
> * LC 253: Meeting Rooms II
> * LC 452: Min Arrows
> * LC 435: Non-overlapping Intervals
> * LC 986: Interval Intersection


🔥 Hard Core:
> * LC 630: Course Schedule III
> * LC 759: Employee Free Time
> * LC 715: Range Module
> * LC 732: My Calendar III
> * LC 1547: Minimum Cost to Cut Stick
> * LC 312: Burst Balloons

----

### THE REAL TRUTH: ONLY 2 BASE PATTERNS EXIST FOR INTERVAL PROBLEMS

All interval problems in the universe fall into one of two fundamental patterns:

✅ $Pattern A — Interval GREEDY (Sorting + Choosing)$

This is for non-DP interval problems.

If all you do is:
* sort intervals
* check overlaps
* merge
* assign rooms
* pick earliest ending interval

→ that’s pure greedy.

Classic examples:
* Merge Intervals
* Insert Interval
* Minimum Arrows
* Non-Overlapping Intervals
* Meeting Rooms
* Video Stitching

Logic:

* You NEVER explore all possibilities.

You ALWAYS:
* sort
* choose best interval
* maintain a structure (PQ or pointer)

That’s it.

This is Interval Greedy.

✅ $Pattern B — Interval DP (dp[l][r])$

This is the DP side of intervals, for the HARD problems.

Used when:
* picking interval affects subintervals
* order of picking matters
* result depends on splitting `[l, r]`
* merging cost inside ranges
* games on intervals
* triangulation, balloon bursts, cuts

Examples:
* Guess Number Higher or Lower II
* Burst Balloons
* Min Cost to Cut Stick
* Stone Game series
* Triangulation
* Palindrome DP
* Any dp[l][r] recurrence

Core recurrence:
```cpp
dp[l][r] = best over all k in [l..r] of:
    dp[l][k] + dp[k+1][r] + cost(l, k, r)
```

This is Interval DP.