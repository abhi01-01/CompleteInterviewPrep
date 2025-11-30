# Stack (5 Patterns)

If problem needs “previous/next something,” “maintain structure,” or “nested parsing,”<br>
→ stack is the GOAT.<br>
If it asks “next greater/smaller,”<br>
→ monotonic stack instantly.

### ✅ ***Pattern 1 — Basic Stack (Process Characters / Validation)***

Used when:
* parentheses matching
* encoding/decoding
* backtracking strings
* remove adjacent duplicates

Template:

```cpp
stack<char> st;

for (char c : s) {
    if (!st.empty() && st.top() matches c)
        st.pop();
    else
        st.push(c);
}
```

> Problems:
>> * LC 20: Valid Parentheses
>> * LC 1047: Remove Adjacent Duplicates
>> * LC 232/225: Queue/Stack using stack
>> * LC 735: Asteroid Collision
>> * LC 844: Backspace String Compare

Why this works:

Stack maintains history. Perfect for last-seen symbol.

### ✅ ***Pattern 2 — Monotonic Stack (Most Important Stack Pattern)***

This pattern ALONE solves 15+ LC problems.

* Monotonic increasing stack → next greater element
* Monotonic decreasing stack → next smaller element

Template (standard):
```cpp
for (i from 0..n-1):
    while (!st.empty() && nums[st.top()] < nums[i]):
        answer[st.top()] = nums[i];
        st.pop();
    st.push(i);
```

> Problems:
>> * LC 739: Daily Temperatures
>> * LC 496: Next Greater Element
>> * LC 503: Next Greater Circular
>> * LC 901: Stock Span
>> * LC 84: Largest Rectangle in Histogram
>> * LC 85: Max Rectangle in Binary Matrix

Why it works:

Maintains useful candidates while removing useless ones greedily.

$Monotonic Stack THINKING RULE$

Ask:
* “Next greater?” → INC stack
* “Next smaller?” → DEC stack
* “How far can this element stretch?” → histogram trick
* “Nearest boundary left/right?” → monotonic stack again

### ✅ ***Pattern 3 — Min Stack / Max Stack (Extra Info)***

Stack that tracks min/max on the fly.

Template:
```cpp
stack<pair<int,int>> st; // {value, currentMin}

push(x):
    minVal = st.empty() ? x : min(x, st.top().second)
    st.push({x, minVal})

min():
    return st.top().second
```

> Problems:
>> * LC 155: Min Stack
>> * LC 716: Max Stack
>> * LC 150: Evaluate Reverse Polish
>> * LC 394: Decode String

Used when you need:
stack + additional state information.

### ✅ ***Pattern 4 — Stack for String Decoding / Expression Evaluation***

Used for:
* nested expressions
* decode patterns `k[abc]`
* evaluate RPN
* parse expressions with + - * / ()

Decode String Template:

```cpp
stack<string> stStr;
stack<int> stNum;
string cur = "";
int num = 0;

for (char c : s) {
    if (isdigit(c)) num = num*10 + (c-'0');
    else if (c == '[') {
        stNum.push(num);
        stStr.push(cur);
        num = 0;
        cur = "";
    }
    else if (c == ']') {
        int repeat = stNum.top(); stNum.pop();
        string prev = stStr.top(); stStr.pop();
        cur = prev + string(repeat, cur);
    }
    else cur += c;
}
```

> Problems:
>> * LC 394: Decode String
>> * LC 150: Evaluate RPN
>> * LC 224/227: Basic Calculator I/II

### ✅ ***Pattern 5 — Stack Simulation (Greedy + Stack)***

Used when you want to remove elements to achieve best result.

Like:
* remove k digits
* remove bad chars
* maintain increasing number
* monotonic-but-with-rules stack

Template:
```cpp
for (char c : s) {
    while (!st.empty() && st.top() > c && canRemoveMore)
        st.pop();
    st.push(c);
}
```

> Problems:
>> * LC 402: Remove K Digits
>> * LC 316: Remove Duplicate Letters
>> * LC 1081: Smallest Subsequence of Distinct
>> * LC 1544: Make String Great

Key idea:

Keep result lexicographically smallest by popping previous bad characters.

----

### <span style="color:yellow">HOW TO RECOGNIZE STACK PROBLEMS?</span>

Look for:

✔️ “next greater/smaller”<br>
✔️ “span”<br>
✔️ “previous smaller/greater”<br>
✔️ “histogram”<br>
✔️ “decode / nested / parse / brackets”<br>
✔️ “balance parentheses”<br>
✔️ “remove digits / letters”<br>
✔️ “simulate operations”

If ANY of these show → STACK, especially monotonic stack.

* **Keep in mind**

```perl
For next greater → Monotonic inc stack
```

```perl
For next smaller → Monotonic dec stack
```

```perl
For lexicographically minimal string → Greedy monotonic removal
```

```perl
For nested structure → Use stack to store partial states
```

```perl
For histogram & rectangles → Use stack to find nearest smaller on both sides
```

---

### <span style="color:yellow">PROBLEMS</span> 
🟢 Easy:

> LC 20: Valid Parentheses
> 
> LC 1047: Remove Adjacent Duplicates
> 
> LC 155: Min Stack
> 
> LC 844: Backspace Compare

🟡 Medium:

> LC 739: Daily Temperatures
> 
> LC 901: Stock Span
> 
> LC 394: Decode String
> 
> LC 150: Reverse Polish
> 
> LC 503: Next Greater Circular
> 
> LC 316 / 1081: Remove Duplicate Letters

🔥 Hard:

> LC 84: Largest Rectangle in Histogram
> 
> LC 85: Max Rectangle in Matrix
> 
> LC 224/227: Basic Calculator I/II
> 
> LC 856: Score of Parentheses