## LC - 291 - [Flip Game](Link)


### Description
You are playing a Flip Game with your friend.

You are given a string currentState that contains only `'+'` and `'-'`. You and your friend take turns to flip two consecutive `"++"` into `"--"`. The game ends when a person can no longer make a move, and therefore the other person will be the winner.

Return all possible states of the string currentState after one valid move. You may return the answer in any order. If there is no valid move, return an empty list [].

 

Example 1:
```yaml
Input: currentState = "++++"
Output: ["--++","+--+","++--"]
```
Example 2:
```yaml
Input: currentState = "+"
Output: []
 ```

Constraints:

* 1 <= currentState.length <= 500
* currentState[i] is either '+' or '-'.


```cpp
class Solution{
    public :
    vector<string> generatePossibleNextMoves(string currState){
        vector<string> ans ;
        int n = currState.size() ;
        for(int i = 0 ; i < n-1 ; ++i){
            if(currState[i] == '+' and currState[i+1] == '+'){
                currState[i] = '-' ;
                currState[i+1] = '-' ;
                ans.push_back(currState) ;
                currState[i] = '+' ;
                currState[i+1] = '+' ;
            } 
        }
        return ans ;
    }
};
```


> Time Complexity = O(N<sup>2</sup>)

> Space Complexity = O(N)