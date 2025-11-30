## THE 7 CORE TREE PATTERNS

✅ **Pattern 1: DFS – Preorder / Postorder / Inorder**

> The “basic traversal” pattern — used everywhere.

**Use when:**

* You need to inspect every node

* Problems like: count, sum, print, serialize, simple recursion

**Template:**

```cpp
void dfs(TreeNode* root) {
    if (!root) return;

    // preorder: use(root)
    dfs(root->left);
    // inorder: use(root)
    dfs(root->right);
    // postorder: use(root)
}
```

>Problems:
>> * Binary Tree Inorder Traversal
>> * Invert Binary Tree
>> * Maximum Depth of Binary Tree

---

✅ **Pattern 2: DFS with Return Value (The “Ask Child → Return Result” Pattern)**

This is S-Tier. Used in diameter, LCA, path-sum, balanced tree etc.

**Idea:**

Child gives a value → parent uses it → returns computed value to ancestor.

**Template:**

```cpp
int dfs(TreeNode* root) {
    if (!root) return base_value;

    int left  = dfs(root->left);
    int right = dfs(root->right);

    // compute something with left & right

    return something;  // returned to parent
}
```

> Problems:
>> * Binary Tree Diameter
>> * Balanced Binary Tree
>> * Max Path Sum
>> * LCA (Lowest Common Ancestor)

<span style="color:yellow">This is the most important tree DP pattern.</sapn>

---

✅ **Pattern 3: DFS with Global Result (Tree DP + update global)**

> When recursion returns helper values but final answer is stored outside.

**Template:**

```cpp
int ans = something;

int dfs(TreeNode* root) {
    if (!root) return 0;

    int l = dfs(root->left);
    int r = dfs(root->right);

    ans = max(ans, compute(l, r, root));  // update global

    return useful_value_for_parent;
}
```

> Problems:
>> * Max Path Sum
>> * Diameter of Tree
>> * Longest Univalue Path
>> * Pseudo-palindromic paths

**Same as Pattern 2 but with global scoring.**

----

✅ **Pattern 4: BFS (Level Order Traversal)**

> Use queue. Best for levels, closest node, vertical/zigzag, etc.

**Template:**

```cpp
void bfs(TreeNode* root) {
    queue<TreeNode*> q;
    q.push(root);

    while (!q.empty()) {
        int size = q.size();

        for (int i = 0; i < size; i++) {
            auto* node = q.front(); q.pop();
            // process this level's node

            if (node->left)  q.push(node->left);
            if (node->right) q.push(node->right);
        }
    }
}
```

> Problems:
>> * Level Order Traversal
>> * Zigzag Level Order
>> * Right Side View
>> * Minimum Depth of Binary Tree

----

✅ **Pattern 5: Tree Construction (Build a tree from array/traversals)**

> Recursion on preorder/inorder or inorder/postorder.

**Template (build from preorder + inorder):**

```cpp
TreeNode* build(int& preIdx, int l, int r, vector<int>& pre, vector<int>& in, unordered_map<int,int>& mp) {
    if (l > r) return NULL;

    TreeNode* root = new TreeNode(pre[preIdx]);
    int mid = mp[pre[preIdx++]];

    root->left = build(preIdx, l, mid - 1, pre, in, mp);
    root->right = build(preIdx, mid + 1, r, pre, in, mp);

    return root;
}
```

> Problems:
>> * Construct Tree from Preorder + Inorder
>> * Construct Tree from Inorder + Postorder

----

✅ **Pattern 6: Path Building (Root-to-leaf paths / sums / conditions)**

> Carry current path downward → check at leaves.

**Template**

```cpp
void dfs(TreeNode* root, vector<int>& path) {
    if (!root) return;

    path.push_back(root->val);

    if (!root->left && !root->right) {
        // use path (root-to-leaf)
    }

    dfs(root->left, path);
    dfs(root->right, path);

    path.pop_back();   // backtrack
}
```

> Problems:
>> * Path Sum I, II
>> * Binary Tree Paths
>> * Sum Root-to-Leaf Numbers

---

✅ **Pattern 7: Subtree Recursion (Check something in every subtree)**

> Ask: “Does this subtree satisfy property X?”

**Template:**


```cpp
bool dfs(TreeNode* root) {
    if (!root) return true;

    bool left = dfs(root->left);
    bool right = dfs(root->right);

    if (!left || !right) return false;

    // check condition for subtree rooted at root
    return condition(root);
}
```

> Problems:
>> * Symmetric Tree
>> * Same Tree
>> * Subtree of Another Tree

----

## Bonus: Binary Search Tree (BST) Patterns (4 sub-patterns)

1️⃣ <span style="color:yellow">**Search/Insert/Delete**</span>

```cpp
if (!root) return new TreeNode(val);
if (val < root->val) root->left = insert(root->left, val);
else root->right = insert(root->right, val);
return root;
```

2️⃣ <span style="color:yellow">**BST Inorder = sorted list**</span>

* Use inorder when you need sorted output.

3️⃣ <span style="color:yellow">**Validate BST**</span>

* Use lower/upper bounds:

```cpp
bool valid(TreeNode* root, long low, long high) {
    if (!root) return true;
    if (root->val <= low || root->val >= high) return false;
    return valid(root->left, low, root->val) &&
           valid(root->right, root->val, high);
}
```

4️⃣ <span style="color:yellow">**Kth Smallest / Kth Largest**</span>

* Use inorder with counter.