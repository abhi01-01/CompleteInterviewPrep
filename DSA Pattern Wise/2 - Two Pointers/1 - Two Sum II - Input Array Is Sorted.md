### Leetcode - 167 - [Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/)


```cpp
class Solution {
public:
    int binarySearch(int value, vector<int>& numbers){
        int start = 0, end = numbers.size()-1 ;

        while(start <= end){
            int mid = start + (end-start)/2 ;

            if(numbers[mid] == value){
                return mid ;
            }

            else if(numbers[mid] > value){
                end = mid - 1 ;
            }
            else{
                start = mid + 1 ; 
            }
        }
        // return -1, if value not present in numbers
        return -1 ;
    } 

    vector<int> twoSum(vector<int>& numbers, int target) {
        int size = numbers.size() ;

        for(int i = 1 ; i <= size ; ++i){
            int idx = binarySearch((target - numbers[i-1]), numbers) ;
            // return value is a 0 based index
            if(idx != -1 and i != (idx+1)){
                return (i <= (idx+1)) ? std::vector<int>{i, idx+1} : std::vector<int>{idx+1, i} ;
            }
        }
        return {-1, -1} ;
    }
};
```

> Time Complexity - O(NlogN)

> Space Complexity - O(1)

---

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int start = 0, end = numbers.size()-1 ;

        while(start < end){
            if((numbers[start] + numbers[end]) == target){
                return {start+1, end+1} ;
            }
            else if((numbers[start] + numbers[end]) > target){
                end-- ;
            }
            else{
                start++ ;
            }
        }
        return {-1, -1} ;
    }
};
```

> Time Complexity - O(N)

> Space Complexity - O(1)