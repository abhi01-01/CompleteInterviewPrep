## LC - 294 - [Flip Game II](Link)


**Problem Statement**

You’re given a string s consisting of only `'+'` and `'-'`.
Two players take turns flipping any consecutive pair `"++"` into `"--"`.
The player who cannot make a move loses.

Return true if you, as the first player, can force a win, assuming both play optimally.

>Example 1:
```cpp
Input: s = "++++"
Output: true
Explanation:
You can flip the first two chars → "--++"
Then no matter what opponent does, you can always respond to win.
```
>Example 2:
```cpp
Input: s = "+-+-"
Output: false
```

This is an “all possible moves” game theory puzzle

Your job is to:

* Generate all valid next moves from current state

* Recursively check if any move leads to a losing state for opponent

* Memoize states to avoid recomputation

* Return true if you can force a win

Step 1: Recursive approach (without memoization)

Core idea:

For every `"++"` in the string, we flip it to `"--"` and check if the opponent loses from that state.
If there exists any such move → current state is winning.


* TopDown Approach - Without Memoization
```cpp
class TopDown{
    public:
    bool canWin(string s) {
        for (int i = 0; i < s.length() - 1; i++) {
            if (s[i] == '+' && s[i+1] == '+') {
                // Flip "++" to "--"
                s[i] = s[i+1] = '-';
                bool opponentWins = canWin(s);
                // Revert the change (backtracking)
                s[i] = s[i+1] = '+';
                
                // If opponent loses, you win
                if (!opponentWins) return true;
            }
        }
        return false; // No winning move found
    }
};
```

> Time Complexity = O(2<sup>n</sup>)

> Space Complexity = O(n) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
    public:
    unordered_map<string, bool> memo;

    bool canWin(string s) {
        if (memo.count(s)) return memo[s];

        for (int i = 0; i < s.length() - 1; i++) {
            if (s[i] == '+' && s[i+1] == '+') {
                s[i] = s[i+1] = '-';
                bool opponentWins = canWin(s);
                s[i] = s[i+1] = '+';  // backtrack
                
                if (!opponentWins) return memo[s] = true;
            }
        }
        return memo[s] = false;
    }
};
```

> Time Complexity = O(n<sup>2</sup>)

> Space Complexity = O(2*n) -- Recursion Stack + Vector 

---

* Tabulation?

Tabulation isn't suitable here — because we're not iterating through numerical states but exploring arbitrary states with backtracking.
So the usual DP table isn't feasible.

---

* Optional Optimization — Grundy Theory (advanced)

There’s a way to convert this into a Sprague-Grundy nimber game by breaking the string into independent segments of "++" and analyzing each segment using XOR.
But that’s only needed for very large problems and isn’t required here.

