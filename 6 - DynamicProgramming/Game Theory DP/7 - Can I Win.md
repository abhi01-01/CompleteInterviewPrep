## LC - 464 - [Can I Win](https://leetcode.com/problems/can-i-win/?envType=problem-list-v2&envId=game-theory)


Important Observations

* If `desiredTotal` <= `maxChoosableInteger` → you instantly win by picking that number.

* If `sum(1..maxChoosableInteger)` < `desiredTotal` → no one can ever reach it → you lose.

```pgsql
sum = n*(n+1)/2
```

**Game Plan (Recursion + Memo + Bitmask ➡️ DP)**

<span style="color:yellow">**You need to simulate:**</span>

* Which numbers are already picked

* Whether the current player can win from that state

<span style="color:yellow">**We’ll represent the used numbers using a bitmask**</span>

* Bitmask of size up to 20 bits (because constraints: maxChoosableInteger ≤ 20)

* Each bit = 1 if that number is already picked.

> Solutions

* TopDown Approach - Without Memoization
```cpp
class TopDown{
    public:
    bool solveWithoutMemo(int maxChoosableInteger, int desiredTotal, vector<bool>& isVisited){
        if(desiredTotal <= 0) return false ;

        for(int i = 1 ; i <= maxChoosableInteger ; ++i){
            if(isVisited[i] != true){
                isVisited[i] = true ;       // pick i
                if(!solveWithoutMemo(maxChoosableInteger, desiredTotal-i, isVisited)){
                    isVisited[i] = false ;      // backtrack
                    return true ;   // because opponent loses here
                }
            isVisited[i] = false ;      // backtrack
            }
        }
        return false ;      // no winning move found
    }

    bool canIWin(int maxChoosableInteger, int desiredTotal) {
        if (desiredTotal <= maxChoosableInteger) return true;
        int sum = maxChoosableInteger * (maxChoosableInteger + 1) / 2;
        if (sum < desiredTotal) return false;

        vector<bool> isVisited(maxChoosableInteger+1, false) ;
        isVisited[0] = true ;
        return solveWithoutMemo(maxChoosableInteger, desiredTotal, isVisited) ;
    }
};
```

> Time Complexity = O(N*2<sup>N</sup>), where $N$ is maxChoosableInteger

> Space Complexity = O() -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
    private:
    // Memoization table: 
    // Key: String representation of the isVisited vector (e.g., "0101" means numbers 2 and 4 are chosen).
    // Value: bool (true if current player wins from this state).
    std::unordered_map<std::string, bool> memo;

    /**
     * Converts the isVisited vector into a unique string key for memoization.
     * The string represents the state of chosen numbers.
     */
    std::string getVectorKey(const std::vector<bool>& isVisited) {
        std::string key = "";
        // Start from i=1 since the problem uses numbers 1 to maxChoosableInteger
        for (size_t i = 1; i < isVisited.size(); ++i) {
            key += isVisited[i] ? '1' : '0';
        }
        return key;
    }

    bool solveWithMemo(int maxChoosableInteger, int desiredTotal, std::vector<bool>& isVisited) {
        // Base Case: If the desired total is met or exceeded by the *opponent's* previous move, 
        // it means the current player already lost.
        if (desiredTotal <= 0) return false;

        // Generate the unique key for the current state (set of chosen numbers)
        std::string key = getVectorKey(isVisited);

        // Check Memo: If the state has been computed, return the cached result
        if (memo.count(key)) {
            return memo[key];
        }

        // Recursive Step: Iterate through all available choices
        for (int i = 1; i <= maxChoosableInteger; ++i) {
            if (isVisited[i] != true) {
                isVisited[i] = true; // Pick 'i'
                
                // Recursively check if the *opponent* loses from the new state.
                if (!solveWithMemo(maxChoosableInteger, desiredTotal - i, isVisited)) {
                    isVisited[i] = false; // Backtrack
                    
                    // If the opponent loses (returns false), then the current player wins by picking 'i'.
                    // Cache the result for the current key and return true.
                    memo[key] = true;
                    return true;
                }
                isVisited[i] = false; // Backtrack
            }
        }

        // No winning move found: The current player loses from this state.
        // Cache the result for the current key and return false.
        memo[key] = false;
        return false;
    }

public:
    bool canIWin(int maxChoosableInteger, int desiredTotal) {
        // Handle Trivial Cases
        if (desiredTotal <= 0) return true;
        
        int sum = maxChoosableInteger * (maxChoosableInteger + 1) / 2;
        if (sum < desiredTotal) return false;

        // Clear memoization table for the new run
        memo.clear(); 

        std::vector<bool> isVisited(maxChoosableInteger + 1, false);
        // isVisited[0] is typically unused, but keeping it in line with your original code structure
        return solveWithMemo(maxChoosableInteger, desiredTotal, isVisited);
    }
};
```

> Time Complexity = O(2<sup>N</sup>), where $N$ is maxChoosableInteger

> Space Complexity = O(N) -- Recursion Stack + Vector 


**The above memoization problem cab be solved using bitMasking

```cpp
class TopDown{
    private:
    // Memoization table: key is the bitmask (state), value is the result (can current player win?)
    std::unordered_map<int, bool> memo; 

    // Function now takes the current state (bitmask) instead of the isVisited vector
    bool solveWithMemo(int maxChoosableInteger, int desiredTotal, int currentMask) {
        // Base Case 1: If the desired total is met or exceeded by the *opponent's* previous move,
        // it means the current player already lost.
        if (desiredTotal <= 0) return false; 

        // Check Memo: If the state has been computed, return the cached result
        if (memo.count(currentMask)) {
            return memo[currentMask];
        }

        // Recursive Step: Iterate through all available choices
        for (int i = 1; i <= maxChoosableInteger; ++i) {
            // Check if 'i' is available: The i-th bit in currentMask should be 0.
            if (!((currentMask >> i) & 1)) {
                
                // Try picking 'i': 
                // 1. Create the new mask: currentMask | (1 << i)
                // 2. Recursively check if the *opponent* loses from the new state.
                if (!solveWithMemo(maxChoosableInteger, desiredTotal - i, currentMask | (1 << i))) {
                    
                    // If the opponent loses (returns false), then the current player wins by picking 'i'.
                    // Cache the result for the currentMask and return true.
                    memo[currentMask] = true;
                    return true;
                }
            }
        }
        
        // No winning move found: The current player loses from this state.
        // Cache the result for the currentMask and return false.
        memo[currentMask] = false;
        return false;
    }

public:
    bool canIWin(int maxChoosableInteger, int desiredTotal) {
        // Handle Trivial Cases
        if (desiredTotal <= 0) return true;
        
        // Check if the total sum of all possible numbers is less than desiredTotal
        int sum = maxChoosableInteger * (maxChoosableInteger + 1) / 2;
        if (sum < desiredTotal) return false;

        // Clear memoization table for the new run (important if the class object is reused)
        memo.clear(); 

        // Start the recursion with an initial mask of 0 (no numbers chosen)
        return solveWithMemo(maxChoosableInteger, desiredTotal, 0);
    }
};
```

> Time Complexity = O(2<sup>N</sup>), where $N$ is maxChoosableInteger

> Space Complexity = O(N)

----