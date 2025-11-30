# Greedy

Greedy is NOT “just take the best local choice”.
That’s baby-level.

Real greedy =
> * Find a global ordering rule,
> * prove that local optimal → global optimal,
> * then implement that rule.

## 6 GREEDY PATTERNS

### ✅ ***Pattern 1 — Sorting + Choosing Best First (Classic Greedy)***

This is the most iconic greedy.

You:

1. Sort items
2. Pick best item first
3. Continue until constraints break

Template

```cpp
sort(a.begin(), a.end());
for (auto x : a) {
    if (canTake(x)) take(x);
}
```

> Problems:
>> * LC 455: Assign Cookies
>> * LC 135: Candy
>> * LC 1647: Min Deletions so frequencies unique
>> * LC 406: Queue Reconstruction
>> * LC 630: Course Schedule III

Reason why this works:<br>
→ Sorted order ensures future choices remain optimal.


### ✅ ***Pattern 2 — Greedy with Priority Queue (Always pick best available now)***

> When choices are dynamic (available items change), go PQ.

Template

```cpp
priority_queue<int> pq;

for event in sorted_events:
    pq.push(event.value);
    if bad_condition: pq.pop();  // fix greedily
```

> Problems:
>> * LC 857: Min Cost to Hire K Workers
>> * LC 502: IPO
>> * LC 215: Kth Largest
>> * LC 253: Meeting Rooms
>> * LC 1705: Eat Fruits While Fresh

Key idea:<br>
→ Maintain current feasible set with PQ and fix when it breaks.


### ✅ ***Pattern 3 — Greedy Interval Scheduling (Intervals Greedy)***

This entire pattern is MASSIVE.<br>
Every interval problem falls into one of these greedy rules:

* **Greedy Rule 1 — Pick the earliest-ending interval**

Used for max non-overlapping intervals

```perl
sort by end
take if(start >= lastEnd)
```

* **Greedy Rule 2 — Minimize conflict using PQ**

Meeting rooms

```perl
sort by start
use pq to track end times
```

* **Greedy Rule 3 — Merge intervals**

```perl
sort by start
if overlap → merge
```

> Problems:
>> * LC 435: Non-overlapping intervals
>> * LC 452: Min Arrows to Burst Balloons
>> * LC 56: Merge Intervals
>> * LC 253: Meeting Rooms 2
>> * LC 621: Task Scheduler

### ✅ ***Pattern 4 — Greedy Math / Observation***

This is where you use properties like:
* Largest element matters
* Remove locally worst
* String/number transformations
* “Take minimum exception” logic

> Examples:
>> * LC 402: Remove K digits → remove highest possible leftmost peak
>> * LC 55: Jump Game → track farthest reachable
>> * LC 763: Partition Labels → partition when all chars resolved
>> * LC 1405: Rearrange String → always pick largest freq

Core idea:<br>
→ You find a monotonic property.

### ✅ ***Pattern 5 — Greedy + Two Pointers***

Combine greedy with two-pointer movement.

Used in:
* sorting both arrays and pairing
* interval pairing
* maximizing matches

Template
```cpp
sort(a); sort(b);
i = j = 0;
while (i<n && j<m) {
    if (good(a[i], b[j])) { take; i++; j++; }
    else j++;
}
```

> Problems:
>> * LC 11: Container With Most Water
>> * LC 986: Interval Intersection
>> * LC 881: Boats to Save People
>> * LC 167: Two Sum Sorted

### ✅ ***Pattern 6 — Greedy Proof via Exchange Argument***

This is the actual theory behind greedy:

> * Start with your greedy solution
> * Exchange with optimal solution step by step
> * Show greedy never gets worse

Used in:

* Job Scheduling
* Minimum Platforms
* K workers
* Interval scheduling
* Shortest finishing time tasks

This is how you prove greedy correctness in interviews.

----

### <span style="color:yellow">GREEDY RULES</span>

Here are the “magic rules” behind 90% of greedy problems:

1. Sort by end time → interval selection

2. Sort by start time → merging intervals

3. Sort by ratio → fractional knapsack

4. Pick local maximum benefit → PQ-based scheduling

5. Pick local minimum conflict → PQ remove long tasks

6. Choose smallest possible digit/character → lexical greedy

7. Greedily merge smallest items first → Huffman coding

8. Greedily destroy largest “bad” element → monotonic stacks

9. Reachability greedy → Jump Game

10. Pick tasks with least processing time first → SJF/BFS greedy

11. Negative-positive pairing → maximize sum

12. Take most constrained first → greedy coloring

You’ll see these again and again.

---

### <span style="color:yellow">How to approach any greedy problem</span>

Whenever facing a greedy problem:

**<span style="color:orange">Step 1</span> — Sort the data**

Always consider:

* by start
* by end
* by value
* by value/time ratio
* by frequency
* lexicographically

**<span style="color:orange">Step 2</span> — Try adding one item at a time**

Consider what happens if you pick:

* smallest
* largest
* earliest
* latest

**<span style="color:orange">Step 3</span> — If choices dynamic → use priority queue**

When greedy needs modifications, PQ automatically keeps system optimal.

**<span style="color:orange">Step 4</span> — If choices depend on interval relationships → interval greedy**

**<span style="color:orange">Step 5</span> — If it feels like a stack → monotonic greedy**

**<span style="color:orange">Step 6</span> — PROVE the greedy choice**

* exchange argument
* contradiction
* “If greedy fails, optimal also fails”
* “Taking this choice opens more future options than any other choice”

If you can do these steps → greedy is done.

---

### <span style="color:yellow">GREEDY CHEAT SHEET</span>

* Sort → choose best current
* Priority queue → keep set optimal
* Intervals → end time matters
* Two pointers → greedy matching
* Monotonic stack → greedy removal
* Greedy is ALWAYS about “global ordering rule”


---

### <span style="color:yellow">GREEDY PROBLEMS</span>

🟢 Beginner

>LC 455: Assign Cookies
>
>LC 605: Can Place Flowers
>
>LC 122: Best Time to Buy/Sell II
>
>LC 409: Longest Palindrome
>
>LC 121: Buy/Sell I

🟡 Medium

> LC 763: Partition Labels
> 
> LC 881: Boats to Save People
> 
> LC 406: Queue Reconstruction
> 
> LC 452: Minimum Arrows
> 
> LC 435: Non-overlapping Intervals
> 
> LC 621: Task Scheduler

🔥 Hard

> LC 857: Min Cost to Hire K Workers
> 
> LC 902: At Most N Using Digit Set
> 
> LC 630: Course Schedule III
> 
> LC 135: Candy
> 
> LC 1647: Min deletions to make freq unique
> 
> LC 239: Sliding Window Max (greedy + monotonic queue)