## THE 6 CORE GRAPH PATTERNS

* These patterns cover everything from BFS/DFS to Dijkstra, Union-Find, Toposort, and even grid-based problems.

---

✅ **Pattern 1 — DFS Graph (Depth-First Search)**

> Explore everything deeply. Used for connected components, cycle detection (directed/undirected), island problems, etc.

**Template:**
```cpp
void dfs(int node, vector<vector<int>>& adj, vector<bool>& vis) {
    vis[node] = true;

    for (int nei : adj[node]) {
        if (!vis[nei]) {
            dfs(nei, adj, vis);
        }
    }
}
```

> Recommended Problems:
>> * Number of Connected Components
>> * Detect Cycle in Undirected Graph
>> * Number of Islands
>> * Clone Graph
>> * Surrounded Regions

---

✅ **Pattern 2 — BFS (Breadth-First Search)**

> Used for shortest path in unweighted graphs, levels, bipartite checks.

**Template:**

```cpp
queue<int> q;
q.push(start);
vis[start] = true;

while (!q.empty()) {
    int u = q.front(); q.pop();
    for (int v : adj[u]) {
        if (!vis[v]) {
            vis[v] = true;
            q.push(v);
        }
    }
}
```

> Recommended Problems:
>> * Shortest Path in Binary Matrix
>> * Bipartite Graph Check
>> * Rotting Oranges
>> * Minimum Depth of Binary Tree (yes, tree = graph)
>> * Word Ladder

----

✅ **Pattern 3 — Topological Sort (Directed Acyclic Graphs)**

> Two ways: BFS (Kahn) and DFS.

**Kahn’s Template:**

```cpp
queue<int> q;
vector<int> indeg(n);

for (int u = 0; u < n; u++)
    for (int v : adj[u])
        indeg[v]++;

for (int i = 0; i < n; i++)
    if (indeg[i] == 0) q.push(i);

vector<int> order;
while (!q.empty()) {
    int u = q.front(); q.pop();
    order.push_back(u);
    for (int v : adj[u]) {
        if (--indeg[v] == 0) q.push(v);
    }
}
```

> Problems:
>> * Course Schedule I
>> * Course Schedule II
>> * Alien Dictionary
>> * Minimum Height Trees
>> * Build System / Task Scheduling Problems

----

✅ **Pattern 4 — Union-Find / DSU**

> The ninja tool to detect connectivity, merging sets, cycles.

**Template:**
```cpp
int find(int x) {
    return parent[x] == x ? x : parent[x] = find(parent[x]);
}

void unite(int a, int b) {
    a = find(a); b = find(b);
    if (a != b) parent[b] = a;
}
```

> Recommended Problems:
>> * Number of Provinces
>> * Accounts Merge
>> * Redundant Connection
>> * Graph Valid Tree
>> * Kruskal’s Minimum Spanning Tree

---

✅ **Pattern 5 — Dijkstra’s (Shortest Path on Weighted Graphs)**

> Use when edges have positive weights.

**Template:**

```cpp
priority_queue<pair<int,int>, vector<pair<int,int>>, greater<pair<int,int>>> pq;
vector<int> dist(n, INF);

dist[src] = 0;
pq.push({0, src});

while (!pq.empty()) {
    auto [d, u] = pq.top(); pq.pop();
    if (d != dist[u]) continue;

    for (auto [v, w] : adj[u]) {
        if (dist[v] > d + w) {
            dist[v] = d + w;
            pq.push({dist[v], v});
        }
    }
}
```

> Recommended Problems:
>> * Network Delay Time
>> * Cheapest Flights with K Stops
>> * Path With Minimum Effort
>> * Swim in Rising Water

----

✅ **Pattern 6 — Grid-as-Graph DFS/BFS (The “Matrix Graph” Pattern)**

> Grid-based problems are just graphs with 4-directional neighbors.

**Template:**
```cpp
vector<pair<int,int>> dirs = {{1,0},{-1,0},{0,1},{0,-1}};

void dfs(int r, int c) {
    vis[r][c] = true;
    for (auto& [dr, dc] : dirs) {
        int nr = r + dr, nc = c + dc;
        if (valid && !vis[nr][nc]) dfs(nr, nc);
    }
}
```
> Recommended Problems:
>> * Number of Islands
>> * Walls and Gates
>> * Flood Fill
>> * Pacific Atlantic Water Flow
>> * Shortest Path in a Grid (BFS)

---

✅ **Pattern 7 — Bellman-Ford / Topo-based DP (Advanced Shortest Path)**

> Used when:
>> * Graph has negative weights
>> * You need to detect negative cycles
>> * You want DP on DAG

**Bellman-Ford Template:**

```cpp
vector<int> dist(n, INF);
dist[src] = 0;

for (int i = 0; i < n-1; i++) {
    for (auto& e : edges) {
        int u = e.u, v = e.v, w = e.w;
        if (dist[u] + w < dist[v]) {
            dist[v] = dist[u] + w;
        }
    }
}
```

> Recommended Problems:
>> * Bellman-Ford implementation
>> * Detect Negative Cycle
>> * Longest Path in DAG (Topo DP)
>> * Shortest Path in DAG (Topo DP)
>> * Coin change on DAG-styled graphs

---

<span style="color:yellow">**BONUS (Patterns inside the patterns)**</span>

Some problems combine multiple patterns, for example:
* “Minimum Effort Path” → BFS + Dijkstra
* “Pacific Atlantic Water Flow” → DFS + multi-source BFS
* “Word Ladder II” → BFS + backtracking

----

⭐ **SUMMARY TABLE (KEEP THIS FOREVER)**

| Pattern               | Use                         | Recommended Areas   |
| --------------------- | --------------------------- | ------------------- |
| DFS                   | Explore deeply, cycles      | Components, islands |
| BFS                   | Levels, shortest unweighted | Bipartite, path     |
| Toposort              | DAG order                   | Dependencies        |
| DSU                   | Connectivity                | Cycle detect        |
| Dijkstra              | Weighted shortest path      | Networks            |
| Grid BFS/DFS          | Matrix graph                | Flood, islands      |
| Bellman-Ford / DAG DP | Negative weights            | Cycle detect, DP    |
