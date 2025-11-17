### Leetcode - 875 - [Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/description/)

Example
```cpp
piles = [3, 6, 7, 11]
h = 8
```

If Koko eats at speed k = 4 bananas/hour:

Pile 1: 3 → takes 1 hour

Pile 2: 6 → takes 2 hours

Pile 3: 7 → takes 2 hours

Pile 4: 11 → takes 3 hours
Total = 8 hours ✅

So k = 4 works, and it’s the minimum possible speed.

⚙️ 1. Observations

* If Koko eats faster, she’ll finish earlier or on time ✅

* If she eats slower, she’ll take longer ❌

So this is a monotonic condition → perfect for binary search!

🧩 2. How to Think About It

We wanna find the minimum speed k that satisfies:

total_hours_needed(k) ≤ h

So binary search the answer between:
```
low = 1                // min possible speed
high = max(piles)      // max pile — no point going faster than biggest pile
```
🧮 3. Compute total hours for a given k

For each pile:
```
hours = ceil(pile / k)
```

In C++:
```
hours += (pile + k - 1) / k;  // neat way to avoid floating point
```

* Code 

```cpp
class Solution {
public:
    int minEatingSpeed(vector<int>& piles, int h) {
        int low = 1, high = *max_element(piles.begin(), piles.end()) ;

        while(low < high){
            int k = low + (high - low)/2 ;

            long long hours = 0 ;
            for(int pile : piles){
                hours += (pile + k - 1)/k ;    // safe ceil division
            }

            if(hours <= h){         // she is eating fast
                high = k ;          // slow here down
            }
            else{
                low = k+1 ;         // make her to eat fast
            }
        }
        return high ;
    }
};
```

> Time Complexity - O(NLogN)

> Space Complexity - O(1)