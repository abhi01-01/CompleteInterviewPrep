## Leetcode - 2226 - [Maximum Candies Allocated to K Children](https://leetcode.com/problems/maximum-candies-allocated-to-k-children/description/)

* This ques is as same as GFG - [Allocate Minimum Pages](https://www.geeksforgeeks.org/problems/allocate-minimum-number-of-pages0937/1)

```cpp
class Solution {
public:
    bool canDisburse(vector<int>& candies, long long k, int candy){

        long long children = 0 ;

        for(int c : candies){
            children += (c/candy) ;
        }
        return (children >= k) ;
    }

    int maximumCandies(vector<int>& candies, long long k) {
        int low = 1 ;       // at leat 1 candy will be distributed to each children
        int high = *max_element(candies.begin(), candies.end()) ;       // children can't get candies from diff piles, so max candy one can get is max(candies)
        int ans = 0 ;       // if candies are less than children, so candies can't be distubuted equally, in some qus we return -1  

        while(low <= high){

            int mid = low + (high - low)/2 ;

            if(canDisburse(candies, k, mid)){
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

> Time Complexity - O(n × Log(sum(arr) - max(arr)))

> Space Complexity - O(1)