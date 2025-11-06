### Leetcode - 343 - [Integer Break](https://leetcode.com/problems/integer-break/description/)

## Explanation

### 1. 🔹 Recurrence Definition
Let **`F(n)`** be the maximum product after splitting **`n`** into `≥ 2` positive integers.

For each possible first split **`a ∈ [1, n−1]`**,
we define: 

$$
F(n) = \max_{1 \le a < n} \big( a \times \max(n - a, F(n - a)) \big)
$$
Here, we either:
- **stop splitting** the remainder *`(n−a)`*, or  
- **break it further** optimally using recursion.

### 2. 🔹 Why It Guarantees `≥ 2` Parts
Every recursive call picks some **`a < n`**, so we immediately create **at least two parts**:
- one part = **`a`**,  
- the other = **`n − a`**.

If the remainder *`(n−a)`* is split again, we naturally get more than two parts.

Thus, this ensures **`k ≥ 2`** parts in every valid decomposition.

### 3. 🔹 Base Case Justification
- For **`n = 2`**, the only valid split is `1 + 1`, giving product `1`.  
- For **`n = 1`**, no further splitting is possible, but returning `1` serves as a neutral multiplier.

Hence:
```cpp
if (n <= 2) return 1;
```

### 4. 🔹 Mathematical soundness (induction sketch):

Assume the formula gives the correct `𝐹(𝑘)` for all `𝑘 < 𝑛`<br>
For `𝑛` every valid partition starts with some first part `𝑎`<br>
The recursion explores all `𝑎` and multiplies it by the best way to handle `𝑛−𝑎` <br>
so it computes the true maximum product over all partitions — proving correctness.

### 5. 🔹 Intuition summary:
Each recursion chooses the first piece, and either stops or keeps breaking the remainder,
ensuring every possible split of 
𝑛
n is covered.
The base case locks the chain, guaranteeing valid sums and at least two parts.
<br>
<br>
<br>


* TopDown Approach - Without Memoization
```cpp
class TopDown{
public:
    int solveWithoutMemo(int n){
        if(n <= 3){
            return (n-1) ;
        }

        int maxProduct = 1 ;

        for(int i = 1 ; i < n ; ++i){
            int nextProduct = max(n-i, solveWithoutMemo(n-i)) ;
            maxProduct = max(maxProduct, nextProduct*i) ;
        }
        return maxProduct ;
    }

    int integerBreak(int n) {
        return solveWithoutMemo(n) ;
    }   
};
```

> Time Complexity = O(N<sup>N</sup>)

> Space Complexity = O(N) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
public:
    int solveWithMemo(int n, vector<int>& dp){
        if(n <= 3){
            return (n-1) ;
        }

        if(dp[n] != -1){
            return dp[n] ;
        }

        int maxProduct = 1 ;

        for(int i = 1 ; i < n ; ++i){
            int nextProduct = max(n-i, solveWithMemo(n-i, dp)) ;
            maxProduct = max(maxProduct, nextProduct*i) ;
        }
        return dp[n] = maxProduct ;
    }

    int integerBreak(int n) {
        vector<int> dp(n+1, -1) ;
        return solveWithMemo(n, dp) ;
    }    
};
```

> Time Complexity = O(N<sup>2</sup>)

> Space Complexity = O(2*N) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- With 1D table

```cpp
class BottomUp{
public:
    int solveWith1Dtable(int n){
        vector<int> dp(n+1, -1) ;
        dp[0] = 1, dp[1] = 1, dp[2] = 1 ;

        for(int idx = 3 ; idx <= n ; ++idx){
            int maxProduct = 1 ;
            for(int i = 1 ; i < idx ; ++i){
                int nextProduct = max(idx-i, dp[idx-i]) ;
                maxProduct = max(maxProduct, nextProduct*i) ;
            }
            dp[idx] = maxProduct ;
        }
        return dp[n] ; 
    }

    int integerBreak(int n) {
        if(n<=3){
            return (n-1) ;
        }
        return solveWith1Dtable(n) ;
    }
};
```

> Time Complexity = O(N<sup>2</sup>)

> Space Complexity = O(N)

---

* Bottom Up Approach -- Without 1D table

```cpp
class BottomUp{
// Can't be optimized further
};
```

> Time Complexity = O()

> Space Complexity = O()