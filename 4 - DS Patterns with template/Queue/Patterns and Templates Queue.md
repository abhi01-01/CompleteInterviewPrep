# Queue (5 Patterns)

*  Need level-by-level, shortest path, or window max/min?<br>
→ `Queue or Deque is the answer.`<br>
* Need ordered processing with constraints?<br>
→ `Queue.`

### ✅ $Pattern 1 — BFS (Breadth-First Search Using Queue)$

This is the KING of queues.

If problem says:
* shortest path
* minimum steps
* “level by level”
* grid traversal
* multi-source BFS

→ BFS + queue is ALWAYS correct.

Template:

```cpp
queue<pair<int,int>> q;
q.push({start, 0});

while (!q.empty()) {
    auto [node, dist] = q.front(); q.pop();

    for (auto &nbr : graph[node]) {
        if (!visited[nbr]) {
            visited[nbr] = true;
            q.push({nbr, dist + 1});
        }
    }
}
```

> Problems:
>> * LC 102: Binary Tree Level Order
>> * LC 994: Rotting Oranges
>> * LC 286: Walls and Gates
>> * LC 752: Open the Lock
>> * LC 1091: Shortest Path in Binary Matrix
>> * LC 542: 01 Matrix (multi-source BFS)

Why it works:

BFS naturally explores in increasing step/distance order.

### ✅ $Pattern 2 — Monotonic Queue (Deque Trick)$

This is TOP 3 DS in interviews.

Used for:

* sliding window maximum/minimum
* maintaining max/min in `O(1)`
* longest subarray with constraints

Template:
```cpp
deque<int> dq;

for (int i = 0; i < n; i++) {

    // pop smaller elements for max queue
    while (!dq.empty() && nums[dq.back()] <= nums[i])
        dq.pop_back();

    dq.push_back(i);

    // remove out-of-window indices
    if (dq.front() <= i - k)
        dq.pop_front();

    if (i >= k - 1)
        ans.push_back(nums[dq.front()]);
}
```

> Problems:
>> * LC 239: Sliding Window Maximum
>> * LC 1438: Longest Abs Diff <= Limit
>> * LC 862: Shortest Subarray Sum >= K
>> * LC 1696: Jump Game VI

Why it works:

Deque stores candidates in BEST-first order.

### ✅ $Pattern 3 — Queue for Simulation (Process in Time Order)$

Used when problem describes a real-life queue scenario, like:

* customers standing in line
* CPU task scheduling
* event simulation
* printers / servers / counters
* BFS-like scheduling but not graph

Template:

```cpp
queue<Task> q;

while (!q.empty()) {
    Task cur = q.front(); q.pop();
    
    update state;
    push new events into queue;
}
```

> Problems:
>> * LC 2073: Time Needed to Buy Tickets
>> * LC 1700: Students and Lunch Queue
>> * LC 621: Task Scheduler (depends)
>> * LC 2258: Escape the Spreading Fire (multi-BFS)

Why it works:

Queue preserves temporal order exactly.

### ✅ $Pattern 4 — Topological Sort (Kahn’s Algorithm Using Queue)$

Used when:
* prerequisites
* ordering tasks
* detect cycle in directed graph
* course scheduling

Template:
```cpp
queue<int> q;
for (i in 0..n)
    if (indegree[i] == 0)
        q.push(i);

while (!q.empty()) {
    int u = q.front(); q.pop();
    order.push_back(u);

    for (v : graph[u]) {
        if (--indegree[v] == 0)
            q.push(v);
    }
}
```

> Problems:
>> * LC 207: Course Schedule
>> * LC 210: Course Schedule II
>> * LC 269: Alien Dictionary
>> * LC 310: Minimum Height Trees

Why it works:

Queue ensures that only “ready” nodes are processed.

### ✅ $Pattern 5 — Rotating Queue (Useful for Circular Structures)$

Used when:
* simulating circular dequeue
* Josephus-like problems
* rotating array
* printing queue in cycles

Template:

```cpp
queue<int> q;

while (!q.empty()) {
    for (int i = 1; i < k; i++) {
        q.push(q.front());
        q.pop();
    }
    eliminate(q.front());
    q.pop();
}
```

> Problems:
>> * LC 1823: Find the Winner (Josephus)
>> * Simulate circular process
>> * Card rotation tricks
>> * Task elimination games

---

### <span style="color:yellow">Priority Queue ≠ Queue (Don’t confuse them!)</span>

* Queue = FIFO
* Deque = push/pop from both sides
* Priority Queue = always remove best item first
* Only deque/queue go under queue patterns.

<span style="color:yellow">***HOW TO RECOGNIZE A QUEUE PROBLEM?***</span>

Look for:

✔️ level-by-level<br>
✔️ shortest number of steps<br>
✔️ BFS traversal<br>
✔️ sliding window max/min<br>
✔️ “expired items” in a window<br>
✔️ prerequisites / topological<br>
✔️ real-life queue simulation<br>
✔️ multi-source BFS<br>
✔️ increasing / decreasing window property<br>

If any appear → queue/deque is the weapon.

<span style="color:yellow">QUEUE CHEAT</span>

* `Need shortest steps?`
→ `BFS (queue)`

* `Sliding window max/min?`
→ `Monotonic deque`

* `Topological order?`
→ `Queue (Kahn’s algorithm)`

* `Simulation of real-line?`
→ `Queue`

* `Multi-source BFS?`
→ `Push all starting points into queue first`

* `Longest/shortest subarray with constraints?`
→ `Monotonic deque or sliding window with array indices`

---

### <span style="color:yellow">QUEUE / DEQUE PROBLEMS</span>

🟢 Easy:

> LC 933: Number of Recent Calls
> 
> LC 225: Implement Stack Using Queues
> 
> LC 232: Implement Queue Using Stacks

🟡 Medium:

> LC 102: Level Order
> 
> LC 994: Rotting Oranges
> 
> LC 239: Sliding Window Maximum
> 
> LC 1438: Longest Abs Diff Window
> 
> LC 210: Course Schedule II
> 
> LC 207: Course Schedule

🔥 Hard:

> LC 862: Shortest Subarray >= K
> 
> LC 301: Remove Invalid Parentheses (BFS)
> 
> LC 2258: Escape the Spreading Fire
> 
> Word Ladder (classic BFS)