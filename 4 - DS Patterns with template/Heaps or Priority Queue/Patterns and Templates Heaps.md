# PRIORITY QUEUE(5 Patterns)

Priority Queue in One Line
>PQ = “Always pick the best current option.<br>
>If constraints break → pop the worst.”

Greedy + PQ = S-tier interview combo.

### ✅ ***Pattern 1 — Always Pick Best Available Item (Top K / Max or Min Selection)***

Use when:
* “Find k largest / smallest”
* “Pick the best candidate repeatedly”
* “Greedy where best item at each step matters”

Template
```cpp
priority_queue<int> pq; // max-heap

for (int x : arr) pq.push(x);

while (!pq.empty()) {
    int best = pq.top();
    pq.pop();
    // process best item
}
```

> Problems:
>> * LC 215: K-th Largest Element
>> * LC 347: Top K Frequent
>> * LC 973: K Closest Points
>> * LC 692: Top K Words
>> * LC 451: Sort Characters by Frequency

Why it works:

Heaps give O(log n) best-element extraction → ideal for greedy.

### ✅ ***Pattern 2 — Maintain a Running Set with Constraints (Shrink PQ when invalid)***

Used when you keep taking items but must maintain constraints.

Template (super important)
```cpp
priority_queue<int> pq;

for (x in items_ordered_by_time) {
    pq.push(cost[x]);
    if (pq violates constraint) pq.pop();  // greedy fix
}
```


> Problems:
>> * LC 630: Course Schedule III (remove biggest duration)
>> * LC 857: Min Cost to Hire K Workers (remove worst wage ratio)
>> * LC 871: Minimum Refuel Stops
>> * LC 502: IPO (pick best-profit project)

Core reasoning:
Whenever constraint breaks → pop worst element from heap.

### ✅ ***Pattern 3 — Two-Heaps Trick (Median, sliding window)***

This is legendary.

You maintain:

* max-heap = lower half

* min-heap = upper half

Template
```cpp
priority_queue<int> left; // max-heap
priority_queue<int, vector<int>, greater<int>> right; // min-heap

void balance() {
    if(left.size() > right.size()+1) {
        right.push(left.top());
        left.pop();
    } else if(right.size() > left.size()) {
        left.push(right.top());
        right.pop();
    }
}
```

> Problems:
>> * LC 295: Find Median from Data Stream
>> * LC 480: Sliding Window Median
>> * LC 502: IPO with two PQs
>> * Event scheduling, CPU tasks

This pattern is crucial in interviews.

### ✅ ***Pattern 4 — Heap of Tasks / Scheduling (Event Simulation)***

Used when events arrive in sorted order and you must pick the “best” event.

Template:
```cpp
sort(tasks by start time);

priority_queue<Task> active;

for each time t:
    while (task.start <= t)
        active.push(task);

    process(active.top());  
```

> Problems:
>> * LC 253: Meeting Rooms II
>> * LC 857: Min cost to hire K workers
>> * LC 1847: Closest Room
>> * CPU Scheduling

This is how you simulate real-world systems.

### ✅ ***Pattern 5 — Multi-source Expansion (Dijkstra flavor)***

Heap problems that smell like shortest path.

Template

```cpp
priority_queue<pair<int,node>,
               vector<pair<int,node>>,
               greater<pair<int,node>>> pq;

pq.push({0, src});

while (!pq.empty()) {
    auto [dist, u] = pq.top(); pq.pop();
    if(dist > best[u]) continue; // skip old states

    for neighbor v:
        if(dist + w < best[v]) {
            best[v] = dist + w;
            pq.push({best[v], v});
        }
}
```

> Problems:
>> * LC 743: Network Delay Time
>> * LC 787: Cheapest Flights with K Stops
>> * LC 1631: Path With Minimum Effort
>> * LC 1926: Nearest Exit
>> * LC 505: Rolling Ball Maze

If a problem is like:
“Pick the next smallest distance / cost / risk / time” → Dijkstra.

### ✅ ***BONUS: MONOTONIC PRIORITY QUEUE***

Used to maintain min/max in sliding window + constraints.

Example:

> LC 1438: Longest Absolute Difference ≤ limit (two PQs)

----

### <span style="color:yellow">***HOW TO KNOW IT’S A HEAP PROBLEM?***</span>

Look for keywords:

✔️ “pick highest / lowest X at each step”<br>
✔️ “find k-th largest / smallest”<br>
✔️ “top K”<br>
✔️ “schedule tasks based on deadlines”<br>
✔️ “greedy but need dynamic corrections”<br>
✔️ “always pick the best available option”<br>
✔️ “simulate a process”<br>
✔️ “minimum time / cost / effort to reach something”

→ often Dijkstra = PQ

If you see any → priority queue.

----

✔️ Max-heap
```cpp
priority_queue<int> pq;
```
✔️ Min-heap
```cpp
priority_queue<int, vector<int>, greater<int>> pq;
```
✔️ Custom struct
```cpp
struct Node { int a,b; };
priority_queue<Node, vector<Node>, cmp> pq;
```

---

### PROBLEMS

🟢 Beginner

> LC 703: Kth Largest in Stream
> 
> LC 215: Kth Largest
> 
> LC 347: Top K Frequent
> 
> LC 1046: Last Stone Weight

🟡 Medium

> LC 973: K Closest Points
> 
> LC 253: Meeting Rooms II
> 
> LC 621: Task Scheduler
> 
> LC 502: IPO
> 
> LC 1962: Remove Stones
> 
> LC 1438: Longest Diff ≤ Limit

🔥 Hard

> LC 295: Median Data Stream
> 
> LC 480: Sliding Window Median
> 
> LC 857: Hire K Workers
> 
> LC 630: Course Schedule III
> 
> LC 787: Cheapest Flights
> 
> LC 1631: Path Minimum Effort
> 
> LC 2290: Reachable with Obstacles