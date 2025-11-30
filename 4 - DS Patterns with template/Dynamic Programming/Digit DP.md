# DIGIT DP

<span style="color:yellow">**WHY DIGIT DP?**</span>

> Because brute force on numbers up to `10^18` is impossible.
Digit DP breaks the number into digits and processes digit-by-digit.

digit DP solves problem involving:

* “Count numbers ≤ N satisfying…”
* “Count numbers with digits constraint”
* “Sum of digits over range”
* “Count beautiful numbers”
* “Find largest/smallest with digit rules”
* “No adjacent digits equal”
* “No repeated digits”
* “Digits DP on ranges [L, R]”

<span style="color:yellow">**THE 4 PARAMETERS OF DIGIT DP**</span>

| Parameter        | Meaning                                               |
| ---------------- | ----------------------------------------------------- |
| **pos**          | which digit index you’re at                           |
| **tight**        | whether current prefix equals prefix of limit N       |
| **leading_zero** | whether you are still adding leading zeros            |
| **state**        | problem-dependent state (sum, used mask, prev digit…) |

**The template becomes:**

```perl
dp[pos][tight][leading_zero][state] = count/answer
```
<span style="color:yellow">***DIGIT DP MASTER TEMPLATE***</span>

```cpp
long long dp[pos][tight][leading_zero][state];

long long solve(int pos, bool tight, bool leading,
                StateType state, string& s) {

    if (pos == s.size())
        return isValid(state);  // base condition depends on problem

    if (dp[pos][tight][leading][state] != -1)
        return dp[pos][tight][leading][state];

    int limit = tight ? (s[pos] - '0') : 9;
    long long ans = 0;

    for (int dig = 0; dig <= limit; dig++) {
        
        bool ntight = tight && (dig == limit);
        bool nlead = leading && (dig == 0);

        StateType nstate = transition(state, dig, nlead);

        ans += solve(pos+1, ntight, nlead, nstate, s);
    }

    return dp[pos][tight][leading][state] = ans;
}
```

----

## <span style="color:yellow">THE 5 DIGIT DP PATTERNS</span>

✅ ***Pattern 1 — Count Numbers With Some Digit Constraint***

Examples:

* Count numbers ≤ N where digit sum % 3 == 0
* Count numbers without digit 7
* Count numbers where adjacent digits differ
* Count numbers with no leading zeros allowed after some point

State often:

```ini
state = digit_sum
state = prev_digit
state = have_started
state = mask_of_used_digits
```

Example: `Count numbers ≤ N with sum of digits % K = 0`

State = sum % K
```cpp
long long solve(pos, tight, leading, mod_sum);
```
Transition:
```cpp
int nsum = (leading ? 0 : (mod_sum + dig) % K);
```

✅ ***Pattern 2 — No Repetition / Unique Digits (Bitmask DP + Digit DP)***

> If you want unique digits, use bitmask as the state.

State:
```scss
mask (10 bits) → which digits are used
```

Example:

> Count numbers with all distinct digits ≤ N.

DP state:
```css
dp[pos][tight][leading][mask]
```

Example Transition:
```cpp
if (!leading && (mask & (1 << dig))) continue;
int nmask = leading && (dig == 0) ? mask : mask | (1 << dig);
```

✅ ***Pattern 3 — Adjacent Relationship DP***

Used when:

* no adjacent digits equal
* digit increases
* digit alternates odd/even

State = prev_digit

Transition:
```cpp
if (!leading && dig == prev) continue;
```

Example:

Count numbers where no two adjacent digits are same.

DP:
```css
[pos][tight][leading][prev_digit]
```


✅ ***Pattern 4 — Range Queries [L, R] by digit DP***

Digit DP typically computes:

```pgsql
f(N) = count of valid numbers from 0 to N
```

Then:
```ini
answer = f(R) - f(L-1)
```

ALWAYS do range queries like this.

Template:
```cpp
long long countInRange(L, R) {
    return solve(R) - solve(L-1);
}
```

✅ ***Pattern 5 — Minimization / Maximization instead of Counting***

Examples:

* Smallest number `≥` N with digit constraints
* Maximum sum number
* Minimum deletions to satisfy constraint

Replace "count" with "best value".

Example:

```cpp
dp = best dp, not count dp
ans = min(ans, solve(...))
```

----

### <span style="color:yellow">COMPLETE DIGIT DP CHEAT SHEET</span>

| Constraint           | State             |
| -------------------- | ----------------- |
| sum/digit sum        | sum or sum%k      |
| no leading zeros     | leading_zero flag |
| ≤ N                  | tight flag        |
| no repeated digits   | mask (10 bits)    |
| no consecutive equal | prev_digit        |
| even/odd alternation | prev_parity       |
| value minimization   | dp stores min/max |


----

### <span style="color:yellow">DIGIT DP MINDSET (final boss knowledge)</span>

Digit DP = brute force numbers digit-by-digit
while controlling:

* tight → do not exceed N
* leading zeros → don’t add digits until needed
* transitions → add digit, update state
* memo → dp[pos][tight][leading][state]


---

### <span style="color:yellow">TOP DIGIT DP PROBLEMS (ordered)</span>

🟢 Beginner:

> LC 1012 — Numbers With Repeated Digits (mask DP)
> 
> Count # <= N with sum of digits <= K
> 
> Count numbers with digit 1
> 
> Count numbers without digit 7

🟡 Intermediate:

> LC 600 — Non-negative Integers Without Consecutive Ones
> 
> LC 902 — Numbers At Most N Given Digit Set
> 
> Count numbers with sum % 3 = 0
> 
> Count numbers where digits are increasing
> 
> Count beautiful numbers in range

🔥 Hard:

> LC 1397 — Find All Good Strings
> 
> LC 1067 — Digit Count in Range
> 
> LC 1416 — Restore The Array
> 
> LC 2376 — Count Special Integers
> 
> Count numbers with alternating parity