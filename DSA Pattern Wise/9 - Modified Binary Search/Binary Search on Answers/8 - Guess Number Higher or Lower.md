## LC - 374 - [Guess Number Higher or Lower](https://leetcode.com/problems/guess-number-higher-or-lower/description/)


```cpp
/** 
 * Forward declaration of guess API.
 * @param  num   your guess
 * @return 	     -1 if num is higher than the picked number
 *			      1 if num is lower than the picked number
 *               otherwise return 0
 * int guess(int num);
 */

class Solution {
public:
    int guessNumber(int n) {
        int low = 1, high = n ;

        while(low <= high){
            int mid = low + (high-low)/2 ;

            int apiRes = guess(mid) ;
            if(apiRes == 0){
                return mid ;
            }
            else if(apiRes == -1){
                high = mid - 1 ;
            }
            else{
                low = mid + 1 ;
            }
        }
        return -1 ;
    }
};
```