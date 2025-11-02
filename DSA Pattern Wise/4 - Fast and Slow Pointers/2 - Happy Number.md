### Leetcode - 202 - [Happy Number](https://leetcode.com/problems/happy-number/description/)

1. Brute Force

```cpp
class Solution{
    public :
    int digitsSquareSum(int n){
        int sum = 0 ;
        while(n > 0){
            int digit = n%10 ;
            n /= 10 ;
            sum += (digit*digit) ;
        }
        return sum ;
    }
    bool isHappy(int n){
        unordered_set<int> seen ;
        while(n != 1){
            if(seen.find(n) != seen.end()){
                return false ;
            }
            seen.insert(n) ;
            n = digitsSquareSum(n) ;
        }
        return (n==1) ;
    }
};
```

> Time Complexity - O(logN) 

> Space Complexity - O(logN)

---

2. Two Pointer

```cpp
class Solution{
    public :
    int digitsSquareSum(int n){
        int sum = 0 ;
        while(n > 0){
            int digit = n%10 ;
            n /= 10 ;
            sum += (digit*digit) ;
        }
        return sum ;
    }
    bool isHappy(int n){
        int slow = n, fast = digitsSquareSum(n) ;
        while((slow != 1) and (fast != slow)){
            slow = digitsSquareSum(slow) ;
            fast = digitsSquareSum(digitsSquareSum(fast)) ;
        }
        return (slow==1) ;
    }    
};
```

> Time Complexity - O(logN) 

> Space Complexity - O(1)