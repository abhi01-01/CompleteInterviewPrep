## GFG - [Square Root](https://www.geeksforgeeks.org/problems/square-root/1)

* Using loop 

```cpp
class Solution {
  public:
    int floorSqrt(int n) {
        // code here
        int i = 1 ;
        while((i*i) <= n){
            i++ ;
        }
        return i-1 ;
    }
};
```

> Time Complexity - O(√N)

> Space Complexity - O(1)

---
* Binary Search

```cpp
class Solution {
  public:
    int floorSqrt(int n) {
       int low = 1, high = n, ans = 1 ;
       
       while(low <= high){
           
           int mid = low + (high - low)/2 ;
           
           if((mid*mid) <= n){
               ans = mid ;
               low = mid + 1 ;
           }
           else{
               high = mid - 1 ;
           }
       }
       return ans ;
    }
};
```

> Time Complexity - O(LogN)

> Space Complexity - O(1)

---

* Using formula

Let's say square root of n is x:

=> x = √n

Squaring both the sides:

=> x<sup>2</sup> =n

Taking log on both the sides:

=> log(x<sup>2</sup>) = log(n)

=> 2 × log(x) = log(n)

=> log(x) = 1/2 × log(n)

To isolate x, exponentiate both sides with base e:

=> x = e<sup>1/2 * log(n)</sup>

x is the square root of n:
So, 
√n = e<sup>1/2 × log(n)</sup>


```cpp
int floorSqrt(int n) {
    
  	// calculating square root using 
  	// mathematical formula	
    int res = exp(0.5 * log(n));
    
    // If square of  res + 1 is less than or equal to n
  	// then, it will be our answer
    if ((res + 1) * (res + 1) <= n) {
        res++;
    }
    
    return res;
}
```

> Time Complexity - O(1)

> Space Complexity - O(1)

---

## GFG - [N-th root of a number](https://www.geeksforgeeks.org/dsa/n-th-root-number/)

* Using Binary Search

