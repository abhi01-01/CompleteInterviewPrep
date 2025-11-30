## LC - 3222 - [Find the Winning Player in Coin Game](https://leetcode.com/problems/find-the-winning-player-in-coin-game/?envType=problem-list-v2&envId=game-theory)

* TopDown Approach - Without Memoization
```cpp
class TopDown{
    public:
    bool solveWithoutMem(int x, int y, bool player){
        if(x <= 0 or y <= 3){
            return player ;
        }

        return solveWithoutMem(x-1, y-4, !player) ;
    }

    string winningPlayer(int x, int y) {
        bool player = true ;        // denoting alice by true and bob by false
        bool win = solveWithoutMem(x, y, player) ;
        if(win == true){
            return "Bob" ;
        }
        return "Alice" ;
    }
};
```

> Time Complexity = O(min(x, y))

> Space Complexity = O(x) -- Recursion Stack

---

* TopDown Approach - With Memoization

```cpp
class TopDown{
  public:
    bool solveWithMem(int x, int y, bool player, vector<vector<int>>& dp){
        if(x <= 0 or y <= 3){
            return player ;
        }

        if(dp[x][y] != -1){
            return dp[x][y] ;
        }

        return dp[x][y] = solveWithMem(x-1, y-4, !player, dp) ;
    }

    string winningPlayer(int x, int y) {
        bool player = true ;        // denoting alice by true and bob by false
        vector<vector<int>> dp(x+1, vector<int>(y+1, -1)) ;
        bool win = solveWithMem(x, y, player, dp) ;
        if(win == true){
            return "Bob" ;
        }
        return "Alice" ;
    }  
};
```
* Since there is only one branch in recursion, hence momoization is not effective solution.

> Time Complexity = O(min(x, y))

> Space Complexity = O(x) -- Recursion Stack + Vector 

---

* Bottom Up Approach -- Tabulation / Loop Method

```cpp
class BottomUp{
public:
    bool tabulation(int x, int y, bool player){
        vector<vector<bool>> dp(x+1, vector<bool>(y+1, true)) ;
        
        for(int r = 1 ; r <= x ; ++r){
            for(int c = 4 ; c <= y ; ++c){
                dp[r][c] = !dp[r-1][c-4] ;
            }
        }

        return dp[x][y] ;
    }

    string winningPlayer(int x, int y) {
        bool player = true ;        // denoting alice by true and bob by false
        // In this case return statement is not dependent on grid's cell, while it's on which player couldn't make the move, and we're deciding it by bool variabe win
        bool win = tabulation(x, y, player) ;
        if(win == true){
            return "Bob" ;
        }
        return "Alice" ;
    }
};
```

> Time Complexity = O(x*y)

> Space Complexity = O(x*y)

---

* Bottom Up Approach -- Optimized

```cpp
class BottomUp{
// Can't be optimized
};
```

> Time Complexity = O()

> Space Complexity = O()

---

* Brainteaser

Mathematical Observation (1-line insight)

```cpp
class Solution {
public:
    string winningPlayer(int x, int y) {
        return (min(x, y/4)%2) == 1 ? "Alice" : "Bob" ;
    }
};
```


> Time Complexity = O(1)

> Space Complexity = O(1)