### GFG - [Problem](Link)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
public:
    int solveWithoutMemo(vector<int>& energy, int k, int magician) {
        int n = energy.size() ;
        if(magician >= n)
            return 0;

        return (energy[magician] + solveWithoutMemo(energy, k, magician + k)) ;
    }

    int maximumEnergy(vector<int>& energy, int k) {
        // int start = 0 ;
        int maxEnergy = INT_MIN ;
        for(int start = 0 ; start < energy.size() ; ++start)
            maxEnergy = max(maxEnergy, solveWithoutMemo(energy, k, start)) ;

        return maxEnergy ; 
    }    
}
```

> Time Complexity = O(N*N)

> Space Complexity = O(N) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
public:
    int solveWithMemo(vector<int>& energy, int k, int magician, vector<int>& dp) {
        int n = energy.size() ;
        if(magician >= n)
            return 0;

        if(dp[magician] != -1){
            return dp[magician] ;
        }

        return dp[magician] = (energy[magician] + solveWithMemo(energy, k, magician + k, dp)) ;
    }

    int maximumEnergy(vector<int>& energy, int k) {
        int maxEnergy = INT_MIN, n = energy.size() ;
        vector<int> dp(n, -1) ;
        for(int start = 0 ; start < energy.size() ; ++start)
            maxEnergy = max(maxEnergy, solveWithMemo(energy, k, start, dp)) ;

        return maxEnergy ; 
    }    
}
```

> Time Complexity = O(2*N)

> Space Complexity = O(3*N) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- With 1D table

```cpp
class BottomUp{
public:
    int solveWith1DTable(vector<int>& energy, int k) {
        int n = energy.size(), maxEnergy = INT_MIN ;
        vector<int> dp(n, -1) ;
        // dp[i] represents, maximum energy achievable if you start from index i

        for(int magician = n-1 ; magician >= 0 ; --magician){
            int nextAbsorption = ((magician+k) < n) ? dp[magician+k] : 0 ;
            dp[magician] = energy[magician] + nextAbsorption ;
            maxEnergy = max(maxEnergy, dp[magician]) ;
        }
        return maxEnergy ;
    }

    int maximumEnergy(vector<int>& energy, int k) {
        return solveWith1DTable(energy, k) ;
    }
}
```

> Time Complexity = O(1*N)

> Space Complexity = O(1*N)

>Note:
>>We cannot always return `dp[0]` in problems where the answer is the maximum value across all states, not just starting from index `0`.
In this problem, the magician can start from any index, so the result is the maximum `dp[i]` over all `i`.
Therefore, we maintain maxEnergy while filling DP and return it instead of `dp[0]`.

---

* Bottom Up Approach -- Without 1D table

```cpp
class BottomUp{
// Can't be optimized further
}
```

> Time Complexity = O()

> Space Complexity = O()