# Top 50 Patterns (Identify + Theory + Templates)

![PathToLearnDS](/centralImageRepo/neetcode150path.png)

### 🟩 1. Prefix Sum
Trigger:

> “Count subarrays…”, “sum equals…”, “range queries”, “fast range sum”.

Theory:

> Prefix sum lets you convert range queries to O(1), subarray sum problems to hash maps.

Template:
```cpp
vector<int> pref(n+1);
for(int i=0;i<n;i++) pref[i+1]=pref[i]+nums[i];
int range = pref[r+1] - pref[l];
```
> Qus
>> * LC 560 – Subarray Sum Equals K
>> * LC 523 – Continuous Subarray Sum
>> * LC 974 – Subarray Sums Divisible by K
>> * LC 1248 – Count Nice Subarrays
>> * LC 363 – Max Sum Rectangle No Larger Than K

---

### 🟩 2. Prefix XOR
Trigger:

> “subarray XOR”, “XOR equality”, “parity toggle”.

Theory:

> XOR prefix works like sum but reversible.

Template:
```cpp
vector<int> pref(n+1);
for(int i=0;i<n;i++) pref[i+1] = pref[i] ^ nums[i];
int xr = pref[r+1] ^ pref[l];
```

> Qus
>> * LC 1442 – Count Triplets That Can Form Two Arrays of Equal XOR
>> * LC 1371 – Longest Substring with Even Vowels (parity mask)
>> * LC 1935 – Maximum Number of Words You Can Type
>> * LC 1542 – Longest Awesome Substring

---

### 🟩 3. Prefix Parity / Bitmask State
Trigger:

> “even/odd count”, “at most one odd”, “balanced vowels”, “palindrome substring counts”.

Theory:

> Track parity using bits, compare masks.

Template:
```cpp
int mask = 0;
unordered_map<int,int> freq;
freq[0]=1;

for (char c: s) {
    mask ^= (1 << (c-'a'));
    ans += freq[mask];
    for(int b=0;b<26;b++)
        ans += freq[ mask^(1<<b) ];
    freq[mask]++;
}
```

> Qus
>> * LC 1915 – Wonderful Substrings
>> * LC 1652 (parity form)
>> * LC 2002 – Maximum Product of Word Lengths (mask dp)

---

### 🟩 4. Sliding Window (Fixed)
Trigger:

> “subarray sum ≤ k”, “longest window with…”, “max consecutive…”, “at most k…”.

Theory:

> Two pointers expanding contract window ensuring condition holds.

Template:
```cpp
int l=0;
for(int r=0;r<n;r++){
    // add r
    while(condition_violated()){
        // remove l
        l++;
    }
    // window [l..r] valid
}
```

> Qus
>> * LC 643 – Maximum Average Subarray
>> * LC 1052 – Grumpy Bookstore Owner
>> * LC 1423 – Maximum Points You Can Obtain from Cards

---

### 🟩 5. Sliding Window (Variable / Frequency)
Trigger:

> “count of chars”, “at most k distinct”, “longest substring with…”.

Template:
```cpp
unordered_map<char,int> cnt;
int l=0;
for(int r=0;r<n;r++){
    cnt[s[r]]++;
    while(bad_condition){
        cnt[s[l]]--;
        l++;
    }
    ans = max(ans, r-l+1);
}
```

> Qus
>> * LC 3 – Longest Substring Without Repeating Characters
>> * LC 904 – Fruit Into Baskets
>> * LC 713 – Subarray Product Less Than K
>> * LC 992 – Subarrays With K Distinct Integers

---

### 🟦 6. Two Pointers (Opposite Ends)
Trigger:

> “sorted array”, “pair sum”, “3Sum”, “min diff”.

Template:
```cpp
int l=0, r=n-1;
while(l<r){
    if(a[l]+a[r] < target) l++;
    else if(...) r--;
}
```

> Qus
>> * LC 167 – Two Sum II (sorted)
>> * LC 15 – 3Sum
>> * LC 986 – Interval List Intersections

---

### 🟦 7. Greedy by Sorting
Trigger:

> “maximize/minimize something”, “choose smallest/largest first”, “interval scheduling”.

Template:
```cpp
sort(v.begin(), v.end()); 
for(auto &x: v){
    // greedily take x if possible
}
```
> Qus
>> * LC 455 – Assign Cookies
>> * LC 1029 – Two City Scheduling
>> * LC 1851 – Minimum Interval to Include Each Query

---

### 🟦 8. Merge Intervals
Trigger:

> “overlapping intervals”, “combine ranges”, “free time”.

Template:
```cpp
sort(iv.begin(), iv.end());
vector<vector<int>> res;
for(auto &it: iv){
    if(res.empty() || it[0] > res.back()[1]) res.push_back(it);
    else res.back()[1] = max(res.back()[1], it[1]);
}
```

> Qus
>> * LC 56 – Merge Intervals
>> * LC 57 – Insert Interval
>> * LC 759 – Employee Free Time

-----

### 🟦 9. Activity Selection
Trigger:

> “maximum number of non-overlapping intervals”.

Template:
```cpp
sort(iv.begin(), iv.end(), [](A,B){
    return A.end < B.end;
});
int lastEnd = -inf;
for(auto &it: iv){
    if(it.start >= lastEnd){
        take++;
        lastEnd = it.end;
    }
}
```

> Qus
>> * LC 252 – Meeting Rooms
>> * LC 253 – Meeting Rooms II
>> * LC 1235 – Maximum Profit in Job Scheduling

---

### 🟨 10. Monotonic Stack (Next Greater Element)
Trigger:

> “next greater/smaller”, “stock span”, “daily temperatures”.

Template:
```cpp
stack<int> st;
for(int i=0;i<n;i++){
    while(!st.empty() && nums[st.top()] < nums[i]){
        ans[st.top()] = i;
        st.pop();
    }
    st.push(i);
}
```

> Qus
>> * LC 496 – Next Greater Element I
>> * LC 503 – Next Greater Element II
>> * LC 739 – Daily Temperatures

----


### 🟨 11. Monotonic Stack (Histogram Area)
Trigger:

> “largest rectangle”, “max subarray of heights”, “minimum subarray with constraints”.

Template:
```cpp
stack<int> st;
for(int i=0;i<=n;i++){
    while(!st.empty() && (i==n || h[st.top()] > h[i])){
        int height = h[st.top()]; st.pop();
        int left = st.empty() ? -1 : st.top();
        ans = max(ans, height * (i-left-1));
    }
    st.push(i);
}
```

> Qus 
>> * LC 84 – Largest Rectangle in Histogram
>> * LC 85 – Maximal Rectangle
>> * LC 2281 – Sliding window beauty + monotonic

---

### 🟨 12. Monotonic Queue
Trigger:

> “sliding maximum”, “window monotonicity”.

Template:
```cpp
deque<int> dq;
for(int i=0;i<n;i++){
    while(!dq.empty() && dq.front() <= i-k) dq.pop_front();
    while(!dq.empty() && nums[dq.back()] <= nums[i]) dq.pop_back();
    dq.push_back(i);
    if(i>=k-1) ans.push_back(nums[dq.front()]);
}
```

> Qus
>> * LC 239 – Sliding Window Maximum
>> * LC 1499 – Max Value of Equation
>> * LC 862 – Shortest Subarray with Sum ≥ K

---

### 🟥 13. Binary Search
Trigger:

> “min X such that…”, “can we…?”, “maximize / minimize”.

Template:
```cpp
int l=0, r=1e9;
while(l<r){
    int mid = (l+r)/2;
    if(can(mid)) r=mid;
    else l=mid+1;
}
```
> Qus
>> * LC 35 – Search Insert Position
>> * LC 162 – Find Peak Element
>> * LC 410 – Split Array Largest Sum

---

### 🟥 14. Binary Search on Real Numbers
Trigger:

> “precision”, “min distance”, “rope cutting”, “geometry”.

Template:
```cpp
double l=0, r=1e9;
for(int i=0;i<100;i++){
    double mid = (l+r)/2;
    if(can(mid)) r=mid;
    else l=mid;
}
```

> Qus
>> * LC 875 – Koko Eating Bananas
>> * LC 1011 – Ship Within Days
>> * LC 1552 – Magnetic Force Between Balls

---

### 🟥 15. Lower Bound / Upper Bound Tricks
Trigger:

> “insert in sorted”, “find first >= x”.

Template:
```cpp
int p = lower_bound(v.begin(), v.end(), x) - v.begin();
```

> Qus
>> * LC 300 – Longest Increasing Subsequence
>> * LC 354 – Russian Doll Envelopes
>> * CF - LIS on segments type problems

---

### 🟥 16. Graph BFS
Trigger:

> “shortest path unweighted”, “levels”, “minimum steps”.

Template:
```cpp
queue<int> q; q.push(src);
vector<int> dist(n, -1); dist[src]=0;
while(!q.empty()){
    int u=q.front(); q.pop();
    for(auto v: adj[u]){
        if(dist[v]==-1){
            dist[v]=dist[u]+1;
            q.push(v);
        }
    }
}
```
> Qus
>> * LC 733 – Flood Fill
>> * LC 994 – Rotting Oranges
>> * LC 815 – Bus Routes

----

### 🟥 17. 0-1 BFS
Trigger:

> “edges with 0 or 1 weight”.

Template:
```cpp
deque<int> dq;
dist[src]=0;
dq.push_front(src);

while(!dq.empty()){
    int u=dq.front(); dq.pop_front();
    for(auto [v,w]: adj[u]){
        if(dist[v] > dist[u] + w){
            dist[v] = dist[u] + w;
            if(w==0) dq.push_front(v);
            else dq.push_back(v);
        }
    }
}
```

> Qus
>> * LC 505 – Maze II
>> * LC 1293 – Shortest Path With Obstacles
>> * LC 1263 – Minimum Moves to Move a Box

----

### 🟥 18. Dijkstra
Trigger:

> “shortest path with weights”.

Template:
```cpp
priority_queue<pair<int,int>, vector<...>, greater<...>> pq;
dist[src]=0; pq.push({0,src});
while(!pq.empty()){
    auto [d,u] = pq.top(); pq.pop();
    if(d!=dist[u]) continue;
    for(auto [v,w]: adj[u]){
        if(dist[v] > d+w){
            dist[v]=d+w;
            pq.push({dist[v],v});
        }
    }
}
```

> Qus
>> * LC 743 – Network Delay Time
>> * LC 1514 – Path With Max Probability
>> * LC 1786 – Number of Restricted Paths

---

### 🟥 19. Union-Find (DSU)
Trigger:

> “connected components”, “cycle detection”, “merge groups”.

Template:
```cpp
vector<int> parent(n), sz(n,1);
int find(int x){ return parent[x]==x?x:parent[x]=find(parent[x]); }
void unite(int a,int b){
    a=find(a); b=find(b);
    if(a!=b){
        if(sz[a]<sz[b]) swap(a,b);
        parent[b]=a;
        sz[a]+=sz[b];
    }
}
```

> Qus
>> * LC 547 – Number of Provinces
>> * LC 1319 – Number of Operations to Connect Network
>> * LC 924 – Minimize Malware Spread

---

### 🟩 20. Trie
Trigger:

> “prefix search”, “dictionary words”, “string DP”.

Template:
```cpp
struct Node{
    int nxt[26];
    bool end=false;
    Node(){ memset(nxt,-1,sizeof(nxt)); }
};
vector<Node> trie;

void insert(string s){
    int cur=0;
    for(char c: s){
        int t=c-'a';
        if(trie[cur].nxt[t]==-1){
            trie[cur].nxt[t]=trie.size();
            trie.emplace_back();
        }
        cur = trie[cur].nxt[t];
    }
    trie[cur].end=true;
}
```

> Qus
>> * LC 208 – Implement Trie
>> * LC 211 – Word Dictionary
>> * LC 421 – Maximum XOR of Two Numbers

----

### 🟩 21. Segment Tree (Range Query)
Trigger:

> “range min/max/sum”, “point update”.

Template:
```cpp
vector<int> seg(4*n);

int query(int idx, int l, int r, int ql, int qr){
    if(ql>r || qr<l) return INF;
    if(ql<=l && r<=qr) return seg[idx];
    int mid=(l+r)/2;
    return min(query(idx*2,l,mid,ql,qr),
               query(idx*2+1,mid+1,r,ql,qr));
}
```

> Qus
>> * LC 307 – Range Sum Query
>> * LC 699 – Falling Squares
>> * LC 315 – Count of Smaller Numbers After Self

---

### 🟥 22. Topological Sort (Kahn / DFS)
Trigger:

> “Prerequisites”, “dependencies”, “order of tasks”
> 
> “Graph is DAG”
> 
> “Must process before”

Theory:

> Topological order = linear ordering of nodes where all edges go forward.

Template (Kahn’s Algorithm):
```cpp
queue<int> q;
vector<int> indeg(n);
for (auto &e : edges) indeg[e.to]++;

for(int i=0;i<n;i++)
    if(indeg[i]==0) q.push(i);

vector<int> topo;
while(!q.empty()){
    int u = q.front(); q.pop();
    topo.push_back(u);
    for(int v: adj[u]){
        if(--indeg[v]==0) q.push(v);
    }
}
```

> Qus
>> * LC 207 – Course Schedule
>> * LC 210 – Course Schedule II
>> * LC 269 – Alien Dictionary

---

### 🟦 23. Cycle Detection in Graph
Trigger:

> “Detect cycle”, “can we finish tasks?”, “circular dependency”.

Theory:

> DFS with 3-color states or DSU for undirected graphs.

Template (Directed, DFS):
```cpp
vector<int> vis(n,0); // 0=unvisited,1=visiting,2=done

bool dfs(int u){
    vis[u]=1;
    for(int v: adj[u]){
        if(vis[v]==1) return true;
        if(vis[v]==0 && dfs(v)) return true;
    }
    vis[u]=2;
    return false;
}
```

> Qus 
>> * LC 141 – Linked List Cycle
>> * LC 142 – Detect Cycle II
>> * LC 802 – Eventual Safe States

----


### 🟫 24. Interval DP
Trigger:

> “`dp[l][r]` depends on smaller sub-intervals”

> “palindrome partitions”, “matrix chain multiplication”, “burst balloons”.

Theory:

> DP expands by length.

Template:
```cpp
for (int len = 1; len <= n; len++) {
    for (int i = 0; i + len - 1 < n; i++) {
        int j = i + len - 1;
        // dp[i][j] = combine(dp[i][k], dp[k+1][j])
    }
}
```

> Qus
>> * LC 516 – Longest Palindromic Subsequence
>> * LC 131 – Palindrome Partitioning
>> * LC 312 – Burst Balloons

----

### 🟪 25. String DP (Edit Distance, LCS)
Trigger:

> "minimum operations", "insert/delete/replace", "common subsequence".

Template (Edit Distance):
```cpp
for(int i=0;i<=n;i++) dp[i][0]=i;
for(int j=0;j<=m;j++) dp[0][j]=j;

for(int i=1;i<=n;i++){
    for(int j=1;j<=m;j++){
        if(a[i-1]==b[j-1])
            dp[i][j] = dp[i-1][j-1];
        else
            dp[i][j] = 1 + min({ dp[i-1][j], dp[i][j-1], dp[i-1][j-1] });
    }
}
```
> Qus
>> * LC 72 – Edit Distance
>> * LC 97 – Interleaving String
>> * LC 115 – Distinct Subsequences

----

### 🟨 26. Subsequence DP
Trigger:

> “count subsequences”, “pick or skip”, “dp over index + count”.

Template:
```cpp
for(int i=1;i<=n;i++){
    for(int j=0;j<=target;j++){
        dp[i][j] = dp[i-1][j]; // skip
        if(j >= nums[i-1])
            dp[i][j] |= dp[i-1][j - nums[i-1]]; // take
    }
}
```

> Qus
>> * LC 392 – Is Subsequence
>> * LC 1143 – LCS
>> * LC 1458 – Max Dot Product of Subsequences

---

### ⬜️ 27. Tree DFS (Classic)
Trigger:

> “subtree sum”, “count nodes”, “propagate info upward”.

Template:
```cpp
int dfs(int u, int parent){
    int subtotal = 1;
    for(int v: adj[u]){
        if(v==parent) continue;
        subtotal += dfs(v,u);
    }
    return subtotal;
}
```

> Qus
>> * LC 104 – Max Depth
>> * LC 543 – Diameter
>> * LC 834 – Sum of Distances in Tree

---

### 🟥 28. Tree DP (Rerooting)
Trigger:


> “compute answer for every node”, “reroot tree”, “tree diameter".

Template:
```cpp
void dfs1(int u, int p){
    for(int v: adj[u]){
        if(v==p) continue;
        dfs1(v,u);
        dp1[u] += dp1[v] + size[v];
    }
}

void dfs2(int u, int p){
    for(int v: adj[u]){
        if(v==p) continue;
        dp2[v] = dp2[u] - (dp1[v] + size[v]) + (n - size[v]);
        dfs2(v,u);
    }
}
```

> Qus
>> * LC 310 – Minimum Height Trees
>> * LC 834 – Sum of Distances in Tree
>> * CF: Tree DP rerooting problems

----

### 🟩 29. LCA (Binary Lifting)
Trigger:

> “find LCA”, “u-v distance”, "repeated root queries".

Template:
```cpp
int up[N][LOG], depth[N];

void dfs(int u,int p){
    up[u][0] = p;
    for(int i=1;i<LOG;i++)
        up[u][i]=up[up[u][i-1]][i-1];
    for(int v: adj[u]){
        if(v==p) continue;
        depth[v]=depth[u]+1;
        dfs(v,u);
    }
}

int lca(int a,int b){
    if(depth[a]<depth[b]) swap(a,b);
    int k=depth[a]-depth[b];
    for(int i=0;i<LOG;i++)
        if(k>>i & 1) a=up[a][i];
    if(a==b) return a;
    for(int i=LOG-1;i>=0;i--)
        if(up[a][i]!=up[b][i]){
            a=up[a][i];
            b=up[b][i];
        }
    return up[a][0];
}
```

> Qus
>> * LC 236 – LCA of Binary Tree
>> * LC 1483 – Kth Ancestor
>> * LC 2196 + extra constraints

----

### 🟧 30. Floyd–Warshall
Trigger:

> “all-pairs shortest path”.

Template:
```cpp
for(int k=0;k<n;k++)
    for(int i=0;i<n;i++)
        for(int j=0;j<n;j++)
            d[i][j] = min(d[i][j], d[i][k] + d[k][j]);
```

> Qus
>> * LC 1334 – City With Smallest Number of Neighbors
>> * LC 1617 – Serve Using Nearest
>> * Any APSP CF problem

---

### 🟪 31. KMP String Matching
Trigger:

> “find substring fast”, “pattern matching”, “avoid `O(nm)`”.

Template:
```cpp
vector<int> lps(m);
for(int i=1,len=0;i<m;){
    if(p[i]==p[len]) lps[i++]=++len;
    else if(len) len=lps[len-1];
    else lps[i++]=0;
}

int j=0;
for(int i=0;i<n;i++){
    while(j>0 && s[i]!=p[j]) j=lps[j-1];
    if(s[i]==p[j]) j++;
    if(j==m){
        // match at i-m+1
        j=lps[j-1];
    }
}
```

> Qus
>> * LC 28 – Find Substring
>> * LC 686 – Repeated String Match
>> * LC 214 – Shortest Palindrome

---

### 32. Z-Algorithm
Trigger:

> “find pattern matches”, “string equality inside string”.

Template:
```cpp
vector<int> z(n);
for(int i=1,l=0,r=0;i<n;i++){
    if(i<=r) z[i]=min(r-i+1, z[i-l]);
    while(i+z[i]<n && s[z[i]]==s[i+z[i]]) z[i]++;
    if(i+z[i]-1 > r) l=i, r=i+z[i]-1;
}
```

> Qus
>> * LC 1764 – Form Array by Concatenating
>> * LC 2223 – Sum of Scores of Built Strings
>> * CF Z-problems

---

### 🟥 33. Rolling Hash (Rabin–Karp)
Trigger:

> “string hashing”, “substring equals quickly”, “compare ranges”.

Template:
```cpp
vector<long long> h(n+1), p(n+1);
const long long B = 131, MOD = 1e9+7;

for(int i=0;i<n;i++){
    h[i+1] = (h[i]*B + s[i]) % MOD;
    p[i+1] = p[i]*B % MOD;
}

long long get(int l, int r){
    return (h[r] - h[l]*p[r-l] % MOD + MOD) % MOD;
}
```

> Qus
>> * LC 187 – Repeated DNA Sequences
>> * LC 1044 – Longest Duplicate Substring
>> * LC 718 – Maximum Repeated Subarray

---

### 🟧 34. Sweep Line (Events)
Trigger:

> “maximum overlapping intervals”, “count active segments”.

Template:
```cpp
vector<pair<int,int>> events;
for(auto &it: intervals){
    events.push_back({it.start, +1});
    events.push_back({it.end+1, -1});
}
sort(events.begin(), events.end());

int cur=0;
for(auto &[x,v]: events){
    cur += v;
    ans = max(ans, cur);
}
```

> Qus
>> * LC 252 – Meeting Rooms
>> * LC 253 – Meeting Rooms II
>> * LC 218 – Skyline Problem

---

### 🟨 35. Difference Array
Trigger:

> “range increment updates”, “apply many operations fast”.

Template:
```cpp
vector<int> diff(n+1, 0);

void rangeAdd(int l, int r, int val){
    diff[l] += val;
    diff[r+1] -= val;
}

for (int i=1;i<n;i++)
    diff[i] += diff[i-1];
```

> Qus
>> * LC 370 – Range Addition
>> * LC 1109 – Flight Bookings
>> * LC 1854 – Maximum Population

---

### 🟩 36. Meet in the Middle
Trigger:

> “n = 40”, “subset sums”, “two half recursion”.

Template:
```cpp
vector<long long> A, B;
dfsA(0, mid, 0);
dfsB(mid, n, 0);

sort(B.begin(), B.end());
for(long long x: A){
    // binary search in B
}
```

> Qus
>> * LC 805 – Split Array With Same Average
>> * LC 1755 – Closest Subsequence Sum
>> * CF meet-in-middle classics

----

### 🟦 37. Fenwick Tree (BIT)
Trigger:

> “prefix sum updates”, “point queries”, “range queries”.

Template:
```cpp
vector<int> bit(n+1);

void update(int i, int v){
    for(;i<=n;i+=i&-i) bit[i]+=v;
}

int query(int i){
    int s=0;
    for(;i>0;i-=i&-i) s+=bit[i];
    return s;
}
```

> Qus
>> * LC 307 – Range Sum Query
>> * LC 315 – Count Smaller Numbers
>> * LC 493 – Reverse Pairs

----

### 🟪 38. Lazy Segment Tree
Trigger:

> “range update + range query”.

Template:
```cpp
void push(int idx){
    if(lazy[idx]){
        seg[idx*2] += lazy[idx];
        seg[idx*2+1] += lazy[idx];
        lazy[idx*2] += lazy[idx];
        lazy[idx*2+1] += lazy[idx];
        lazy[idx]=0;
    }
}
```

> Qus
>> * LC 307 (with lazy)
>> * LC 1157 – Majority Checker
>> * LC 715 – Range Module

----

### 🟫 39. Backtracking (DFS on decision tree)
Trigger:

> “generate permutations”, “subsets”, “N-Queens”.

Template:
```cpp
void dfs(int i){
    if(i==n){ save(); return; }
    for(choice in choices){
        take();
        dfs(i+1);
        undo();
    }
}
```

> Qus
>> * LC 46 – Permutations
>> * LC 39 – Combination Sum
>> * LC 212 – Word Search II

----

### 🟥 40. Bitmask DP
Trigger:

> “n ≤ 20”, “states = 2^n”, “TSP”, “assign tasks”.

Template:
```cpp
for(int mask=0; mask<(1<<n); mask++){
    for(int i=0;i<n;i++){
        if(mask&(1<<i)){
            dp[mask] = min(dp[mask], dp[mask^(1<<i)] + cost[i]);
        }
    }
}
```

> Qus
>> * LC 78 – Subsets
>> * LC 1879 – Minimum XOR Sum
>> * LC 847 – Shortest Path Visiting All Nodes

----

### 🟧 41 — Probability DP
Trigger:

> “expected value”, “probabilities”, “ways to reach state”.

Template:
```cpp
dp[0] = 1.0;
for(int i=0;i<n;i++){
    for(int j=... reverse ...){
        dp[j] += dp[j-1] * p[i];
    }
}
```

> Qus
>> * LC 688 – Knight Probability
>> * LC 808 – Soup Servings
>> * LC 1227 – Airplane Probability

----

### 🟨 42. Multi-Source BFS
Trigger:

> “multiple starts”, “spread”, “rotten oranges”.

Template:
```cpp
queue<int> q;
for(src in sources) q.push(src);

while(!q.empty()){
    int u = q.front(); q.pop();
    for(int v: adj[u]){
        if(dist[v] > dist[u] + 1){
            dist[v] = dist[u]+1;
            q.push(v);
        }
    }
}
```

> Qus
>> * LC 994 – Rotting Oranges
>> * LC 1765 – Map of Highest Peak
>> * LC 1162 – As Far From Land

----

### 🟩 43. DAG DP
Trigger:

> “DP on graph without cycles”, “longest path in DAG”.

Template:
```cpp
vector<int> topo = topological_sort();
for(int u: topo){
    for(int v: adj[u]){
        dp[v] = max(dp[v], dp[u] + weight[u][v]);
    }
}
```

> Qus
>> * LC 799 – Champagne Tower
>> * LC 2070 – Most Beautiful Item
>> * LC 2050 – Parallel Courses III

---

### 🟦 44. Palindrome DP
Trigger:

> “is palindrome substring”, “dp[i][j] check”.

Template:
```cpp
for(int i=n-1;i>=0;i--){
    for(int j=i;j<n;j++){
        if(s[i]==s[j] && (j-i<2 || dp[i+1][j-1]))
            dp[i][j]=true;
    }
}
```

> Qus
>> * LC 647 – Palindromic Substrings
>> * LC 516 – LPS
>> * LC 1246 – Palindrome Removal

----

### 🟪 45. Probability / Expected Value (Recurrent DP)
Trigger:

> “expected turns”, “game DP”.

Template:
```cpp
dp[i] = 1 + p * dp[i-1] + q * dp[i-2] + ...
```

> Qus
>> * LC 902 – Numbers at Most N Given Digit Set
>> * LC 1467 – Probability of 2 rectangles overlap
>> * Hard EDP CF problems

----

### ⬜️ 46. Two Heaps (Median Stream)
Trigger:

> “running median”, “insert & balance”.

Template:
```cpp
priority_queue<int> left;
priority_queue<int,vector<int>,greater<int>> right;

void add(int x){
    if(left.empty() || x <= left.top()) left.push(x);
    else right.push(x);

    if(left.size() > right.size()+1){
        right.push(left.top()); left.pop();
    } else if(right.size() > left.size()){
        left.push(right.top()); right.pop();
    }
}
```

> Qus
>> * LC 295 – Median of Data Stream
>> * LC 480 – Sliding Window Median
>> * Custom CF problems

----


### 🟫 47. Using Deque for DP Optimization (Convex Hull Trick)
Trigger:

> “`dp[i]` = `min(dp[j] + line(j)*x(i))`”, “linear optimization”.

(Advanced)

> Qus
>> * CF Edu CHT problems
>> * AtCoder DP Optimization
>> * CF 319C – Kalila and Dimna in the Logging Industry

----

### 🟥 48. Sweep Line with Active Set
Trigger:

> “max overlapping rectangles”, “conflicts”.

Template:
```cpp
set<int> active;
sort(events.begin(), events.end());

for(auto &ev : events){
    if(ev.type==ADD) active.insert(ev.y);
    else active.erase(ev.y);
}
```

> Qus
>> * LC 56 / 252
>> * LC 391 – Perfect Rectangle
>> * LC 218 – Skyline Problem (again)

---

### 🟧 49. Multi-DP (Combination of DP + Greedy)
Trigger:

> “partition with constraints”, “dp[i] with greedy prune”.

> Qus
>> * LC 300 – LIS
>> * LC 2407 – Longest Increasing Subsequence II
>> * LC 1691 – Max Height by Stacking Cuboids

----

### 🟩 50. Number Theory (Sieve, GCD, Modular Inverse)
Trigger:

> “mod 1e9+7”, “pow”, “inverse modulo prime”.

Template:
```cpp
long long modpow(long long a,long long e){
    long long r=1;
    while(e){
        if(e&1) r=r*a%MOD;
        a=a*a%MOD;
        e>>=1;
    }
    return r;
}
```

> Qus 
>> * LC 204 – Count Primes
>> * LC 149 – Max Points on a Line
>> * LC 233 – Count Digit One