# THE 4 CORE TREE DP PATTERNS

✅ **Pattern 1 — DFS: “Return Info Upwards” (Bottom-Up DP)**

> This is the MOST important DP on trees.

You do:

* DFS down

* compute info on children

* return result up

Template:

```cpp
int dfs(int u, int parent) {
    int dpValue = base;

    for (int v : adj[u]) {
        if (v == parent) continue;
        int child = dfs(v, u);

        dpValue = combine(dpValue, child);
    }

    return dpValue;
}
```

> Problems
>> * Diameter of tree
>> * Max depth, min depth
>> * Sum of subtree, count nodes
>> * Count good nodes
>> * Balanced binary tree
>> * Maximum path sum in tree
>> * House Robber III
>> * Tree queries

This is the most common pattern.

Example: Diameter of a Tree
```cpp
int ans = 0;

int dfs(int u, int p) {
    int longest = 0, second = 0;

    for (int v : adj[u]) {
        if (v == p) continue;
        int depth = dfs(v, u);

        if (depth > longest) {
            second = longest;
            longest = depth;
        } else if (depth > second) {
            second = depth;
        }
    }

    ans = max(ans, longest + second);
    return longest + 1;
}
```
---

✅ **Pattern 2 — “Root DP → Rerooting DP” (DP on all roots)**

When you need DP value for EVERY NODE as ROOT.

Idea:

* First DFS: compute dp[u] using children

* Second DFS: push parent info down to children (REROOT)

This is for problems like:

> * LC 834: Sum of Distances in Tree
> * Tree rerooting DP
> * Count ways if each node becomes root
> * Number of nodes in subtree vs outside

Template:

```cpp
void dfs1(int u, int p) {
    for (int v : adj[u]) {
        if (v == p) continue;
        dfs1(v, u);
        dp[u] = combine(dp[u], dp[v]);
    }
}

void dfs2(int u, int p) {
    for (int v : adj[u]) {
        if (v == p) continue;

        dp2[v] = recompute(dp[u], dp[v]);  // reroot transition

        dfs2(v, u);
    }
}
```


> Problems:
>> * Sum of distances in tree
>> * Expected value rerooting
>> * Max path sum from each node
>> * Subtree + complement-subtree computations

Example: Sum of Distances in Tree

(FAANG interview classic)

----

✅ **Pattern 3 — “Tree DP with State” (DP[u][state])**

> Used when each node has multiple states:

* include / exclude
* take / skip
* color black / white
* choose / not choose
 
Template:

```cpp
int dp[u][2];

void dfs(int u, int p) {
    dp[u][0] = 0;      // excluded state
    dp[u][1] = value;  // included state

    for (int v : adj[u]) {
        if (v == p) continue;
        dfs(v, u);

        dp[u][0] += max(dp[v][0], dp[v][1]);  // if u excluded
        dp[u][1] += dp[v][0];                 // if u included
    }
}
```

> Problems:
>> * LC 337: House Robber III
>> * Maximum independent set in tree
>> * Tree coloring DP
>> * Minimum vertex cover
>> * Maximum matching in tree
>> * DP on tree subsets

This is one of the most powerful patterns.

Example: House Robber III
```cpp
int dfs(TreeNode* root) {
    if (!root) return {0, 0};

    auto L = dfs(root->left);
    auto R = dfs(root->right);

    int rob = root->val + L.skip + R.skip;
    int skip = max(L.rob, L.skip) + max(R.rob, R.skip);

    return {rob, skip};
}
```

----

✅ **Pattern 4 — “Tree Divide & Conquer (Centroid DP)”**

This is advanced, used when:

* Counting pairs with constraints
* Distance-k problems
* Heavy subtree merging

Large tree constraints (up to 2e5)

Template Concept:

```mathematica
Pick centroid
Solve problem rooted at centroid
Recurse on remaining components
```

> Problems:
>> * Count pairs with distance ≤ K
>> * Tree queries on large input
>> * CF hard tree problems

This is optional unless doing hard CP.

----

### HOW TO RECOGNIZE TREE DP PROBLEMS

Ask:

✔️ Does the problem ask something for each subtree?

→ Pattern 1 (bottom-up)

✔️ Need answer for whole tree with root changes?

→ Pattern 2 (reroot DP)

✔️ Node has different choices/states?

→ Pattern 3 (`dp[u][state]`)

✔️ Need to combine many child results?

→ Tree DP

✔️ Very large tree + constraints?

→ Centroid DP

---

### GOLDEN TEMPLATE (memorize this)

```cpp
int dfs(int u, int p) {
    for (int v : adj[u]) {
        if (v == p) continue;
        int child = dfs(v, u);
        // combine child info
    }
    return result_for_u;
}
```

Every tree DP reduces to:

* combine child results
* return something to parent

----


### <span style="color:yellow">MUST-SOLVE TREE DP PROBLEMS (ordered)<span>

🟢 Easy:

> LC 543: Diameter of Binary Tree
> 
> LC 104: Maximum Depth
> 
> LC 572: Subtree of Another Tree
> 
> LC 226: Invert Tree

🟡 Medium:

> LC 337: House Robber III
> 
> LC 1026: Max Ancestor Difference
> 
> LC 124: Max Path Sum
> 
> LC 199: Right Side View
> 
> LC 863: Distance K Nodes

🔥 Hard:

> LC 834: Sum of Distances in Tree
> 
> LC 968: Binary Tree Cameras
> 
> LC 1245: Tree Diameter
> 
> LC 1932: Merge BSTs
> 
> LC 1617: Count Subtrees with Max Distance
> 
> LC 2049: Count Nodes With Highest Score

💀 Giga-hard (CF level):

> Centroid decomposition problems
> 
> Subtree merging in O(n log² n)
> 
> LCT (Link-Cut Trees)


-----

### <span style="color:yellow">TREE DP CHEAT SHEET</span>

| Pattern      | Use                          |
| ------------ | ---------------------------- |
| Bottom-up DP | Combine child info           |
| Reroot DP    | Compute DP for every root    |
| `DP[u][state]` | Take/skip decisions on nodes |
| Centroid DP  | Large heavy constraints      |
