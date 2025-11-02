### Leetcode - 15 - [3 Sum](https://leetcode.com/problems/3sum/description/)

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> res ;
        sort(nums.begin(),nums.end()) ;
        for( int i = 0 ; i < nums.size() ; i++ ){
            int j = i+1 , k = nums.size()-1 ;
            while(j<k){
                if(nums[i]+nums[j]+nums[k]>0)
                    k-- ;
                else if(nums[i]+nums[j]+nums[k]<0)
                    j++ ;
                else{
                    vector<int>inner={nums[i],nums[j],nums[k]};
                    res.push_back(inner) ;
                    
                    // Avoiding dupliates
                    while(j<k&&nums[j]==inner[1]) j++ ;
                    while(j<k&&nums[k]==inner[2]) k-- ;
                }
            }
            // Avoiding dupliates
            while(i+1<nums.size()&&nums[i+1]==nums[i])
                i++ ;
        }
        return res ;
    }
};
```

> Time Complexity - O(N<sup>2</sup> + NlogN) = O(N<sup>2</sup>)

> Space Complexity - O(1*N) - While Sorting