## BACKTRACKING — The 7 Core Patterns

✅ **Pattern 1 — Subsets (Power Set)**

“Choose or not choose” at each index.

> Problems:
>> * Subsets I / II
>> * Combination Sum (type variations)
>> * Target Sum (as recursion)

🧩 **Template:**

```cpp
void backtrack(int idx, vector<int>& nums, vector<int>& path, vector<vector<int>>& res) {
    res.push_back(path); // add current subset

    for (int i = idx; i < nums.size(); i++) {
        path.push_back(nums[i]);
        backtrack(i + 1, nums, path, res);
        path.pop_back();
    }
}
```

**Core idea:**

* Loop through choices starting from idx
* Use each element at most once
* Always include the current path

---

✅ **Pattern 2 — Combinations (k out of n)**

**Subset with fixed size.**

> Problems:
>> * Combinations (n choose k)
>> * Generate Parentheses (structure-based combos)

🧩 **Template:**

```cpp
void backtrack(int start, int n, int k, vector<int>& path, vector<vector<int>>& res) {
    if (path.size() == k) {
        res.push_back(path);
        return;
    }

    for (int i = start; i <= n; i++) {
        path.push_back(i);
        backtrack(i + 1, n, k, path, res);
        path.pop_back();
    }
}
```
---

✅ **Pattern 3 — Permutations (All Orderings)**

**Every index picks any unused element.**

> Problems:
>> * Permutations I / II
>> * Letter case permutation
>> * N-Queens (uses permutation logic)
 
🧩 **Template:**

```cpp
void backtrack(vector<int>& nums, vector<bool>& used, vector<int>& path, vector<vector<int>>& res) {
    if (path.size() == nums.size()) {
        res.push_back(path);
        return;
    }

    for (int i = 0; i < nums.size(); i++) {
        if (used[i]) continue;

        used[i] = true;
        path.push_back(nums[i]);

        backtrack(nums, used, path, res);

        used[i] = false;
        path.pop_back();
    }
}
```

**Core idea:**

* Choose one unused element at each level (depth = number of elements)

* Leads to factorial-time recursion.

---

✅ **Pattern 4 — Combination Sum (Unlimited Reuse)**

**Use an element multiple times.**

> Problems:
>> * Combination Sum I
>> * Unbounded knapsack recursion

🧩 **Template:**

```cpp
void backtrack(int idx, vector<int>& nums, int target, vector<int>& path, vector<vector<int>>& res) {
    if (target == 0) {
        res.push_back(path);
        return;
    }
    if (idx >= nums.size() || target < 0) return;

    // Pick (stay at idx because reuse allowed)
    path.push_back(nums[idx]);
    backtrack(idx, nums, target - nums[idx], path, res);
    path.pop_back();

    // Skip
    backtrack(idx + 1, nums, target, path, res);
}
```
---

✅ **Pattern 5 — Decision Tree (Try All Moves)**

**Used in game theory, flip game, DP + recursion, number guessing, etc.**

> Problems:
>> * Predict the Winner
>> * Can I Win
>> * Word Break (DFS version)
>> * Expression Add Operators

🧩 **Template:**

```cpp
bool backtrack(state) {
    if (base condition) return answer;

    for (all possible moves) {
        apply move;
        if (backtrack(newState) == desired) return desired;
        undo move;
    }

    return opposite result;
}
```

**This is the core minimax structure.**

----

✅ **Pattern 6 — Board Search (Grid Backtracking)**

**DFS + backtracking with directions.**

> Problems:
>> * Word Search
>> * Rat in a Maze
>> * Sudoku Solver
>> * N-Queens (board version)

🧩 **Template:**

```cpp
bool backtrack(int r, int c, ...) {
    if (goal) return true;

    for (auto& [dr, dc] : dirs) {
        int nr = r + dr, nc = c + dc;
        if (valid && !visited[nr][nc]) {
            visited[nr][nc] = true;

            if (backtrack(nr, nc)) return true;

            visited[nr][nc] = false;
        }
    }
    return false;
}
```
----

✅ **Pattern 7 — Build Strings / Paths (Sequence Construction)**

**Build character by character.**

> Problems:
>> * Generate Parentheses
>> * Restore IP Addresses
>> * Palindrome Partitioning
>> * Letter Tile Possibilities

🧩 **Template:**

```cpp
void backtrack(int pos, string& path) {
    if (pos == n) {
        res.push_back(path);
        return;
    }

    for (each possible character or choice) {
        path.push_back(c);
        backtrack(pos + 1, path);
        path.pop_back();
    }
}
```

---

✅ **The Universal Backtracking Template**

When you don’t know where to start, use this:

```cpp
void backtrack(type state, ...) {
    if (base case) {
        store result
        return;
    }

    for (choice in possibleChoices) {
        apply(choice);
        backtrack(updatedState, ...);
        undo(choice);
    }
}
```