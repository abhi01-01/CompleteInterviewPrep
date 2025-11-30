# DSU (4 Patterns)

DSU IN ONE LINE

>DSU = MERGE sets + QUERY sets<br>
>If problem is about connectivity, grouping, or cycles → DSU is always top 1 option.

### ✅ $Pattern 1 — Basic Connectivity (Union Components)$

Used when you need to:
* connect nodes
* check if two nodes are in same component
* count components
* combine sets

Template
```cpp
vector<int> parent(n), size(n,1);

int find(int x){
    return parent[x] == x ? x : parent[x] = find(parent[x]);
}

void unite(int a, int b){
    a = find(a);
    b = find(b);
    if(a == b) return;
    if(size[a] < size[b]) swap(a,b);
    parent[b] = a;
    size[a] += size[b];
}
```

> Problems:
>> * LC 200: Number of Islands (grid as graph)
>> * LC 547: Number of Provinces
>> * LC 1319: Make Connected
>> * LC 323: Connected Components

Core idea:

Merge when connected. Query using find().

### ✅ $Pattern 2 — DSU for Cycle Detection$

Used when:
* detecting cycle in undirected graph
* identifying redundant connections
* finding extra edge

Template:
```cpp
for each (u, v):
    if(find(u) == find(v)):
        cycle found
    unite(u, v)
```

> Problems:
>> * LC 684: Redundant Connection
>> * Detect cycle in undirected graph
>> * Railway/road connections problems

Why it works:

If u and v already in same set → adding edge creates cycle.

### ✅ $Pattern 3 — DSU on Grid (2D → 1D conversion)$

Used for:
* islands
* percolation
* counting territories
* merging adjacent cells

Conversion:
```ini
id = r * cols + c
```

Template:
```cpp
if(grid[r][c] == 1){
    for neighbors:
        if(neigh is land)
            unite(id, neighId)
}
```

> Problems:
>> * LC 200: Number of Islands
>> * LC 305: Number of Islands II (dynamic)
>> * LC 952: Largest Component by Common Factor
>> * LC 990: Satisfiability of Equality Equations

### ✅ $Pattern 4 — DSU With Extra State (Advanced DSU)$

When each node holds extra information:

Types:

a) <span style="color:orange">***Weighted DSU***</span>

Used when:
* edges have weights
* ratios (division equations)
* distances

Example: LC 399 — Evaluate Division
Store:
```perl
parent[x]  
weight[x] = value(x) / value(parent[x])  
```

b) <span style="color:orange">***Bipartite DSU / Color DSU***</span>

Used when:
* checking bipartite
* parity constraints
* 2-color union constraints

c) <span style="color:orange">***DSU with Rollback (rare, ICPC only)***</span>

Used for:
* offline queries
* undo unite operations

d) <span style="color:orange">***DSU with Rank / Size***</span>

Classic optimization:

* union by size → stable
* union by rank → balanced

> Advanced DSU Problems:
>> * LC 399: Evaluate Division (weighted)
>> * LC 952: Largest Component by Common Factor
>> * LC 839: Similar String Groups
>> * LC 721: Accounts Merge
>> * LC 990: Satisfiability of Equality Equations
>> * LC 1697: Checking Existence of Edge (offline queries)

----

### <span style="color:yellow">HOW TO KNOW IT’S A DSU PROBLEM?</span>

Look for keywords:

✔️ “connected” / “component” / “province” <br>
✔️ “merge groups”<br>
✔️ “are X and Y connected?”<br>
✔️ “count number of components”<br>
✔️ “cycle exists?”<br>
✔️ “group items by relationship”<br>
✔️ “same set?”<br>
✔️ “union of people/accounts/strings”<br>
✔️ “equations or constraints between items”

If ANY appear → DSU is king.

---

### <span style="color:yellow">DSU CHEAT CODES</span>

✔️ Always compress path for `O(α(n))`
```cpp
parent[x] = find(parent[x]);
```
✔️ Always union by size
```cpp
if(size[a] < size[b]) swap(a, b);
parent[b] = a;
size[a] += size[b];
```
✔️ For 2D grid → convert to 1D ID
```ini
id = r * m + c
```

✔️ For cycle detection → check root before union

✔️ For equations `“x == y”` / `“x != y”`

> 1. Union all `x == y`
> 2. Check contradictions for x != y

✔️ For weighted DSU → store multipliers / differences

---

### <span style="color:yellow">PROBLEMS</span>

🟢 Easy/Medium:

> LC 547: Number of Provinces
> 
> LC 200: Number of Islands
> 
> LC 1319: Make Connected
> 
> LC 684: Redundant Connection
> 
> LC 839: Similar String Groups

🟡 Medium/Hard:

> LC 721: Accounts Merge
> 
> LC 990: Satisfiability of Equality Equations
> 
> LC 952: Largest Component by Common Factor
> 
> LC 1202: String Swap Lexicographically Smallest

🔥 Hard:

> LC 305: Number of Islands II
> 
> LC 1697: Distance Limited Paths (offline DSU)
> 
> LC 1627: Graph Connectivity With Threshold
> 
> DSU Rollback problems (Codeforces)
