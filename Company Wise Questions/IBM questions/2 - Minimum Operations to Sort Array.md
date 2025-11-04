### Minimum operations to sort Array

 Implement a function which determines the minimum number if operations required to sort an array of size n in non-decreasing order using the following operations any number of times possibly zero.
 * Extract the 1st element of the array and insert it at the end.
 * Then swap the element with the previous one until it becomes the first or is strictly greater than the previous one. 

 The function munOperationsToSort will take the following input vector<int> arr

### Naive Approach

```cpp
class Solution{
    public :
    int minOperationsToSort(vector<int>& arr){
        int size = arr.size() ;

        if(size <= 1){
            return 0 ;
        }

        vector<int> sortedArr = arr ;
        sort(sortedArr.begin(), sortedArr.end()) ;

        for(int opr = 1 ; opr <= size ; ++opr){
            int first = arr[0] ;

            arr.erase(arr.begin()) ;
            arr.push_back(first) ;

            int j = size-1 ;

            while(j > 0 and arr[j] < arr[j-1]){
                swap(arr[j], arr[j-1]) ;
                j-- ;
            }

            if(arr == sortedArr){
                return opr ;
            }
        }
        return -1 ;
    }
};
```

> Time Complexity - O(N<sup>2</sup>)

> Space Complexity - O(N)

### Optimized Approach

```cpp
class Solution{
    public:
    int minOperationsToSort(vector<int>& arr){
        int size = arr.size() ;
        int dropCount = 0, dropIndex = -1 ;

        for(int i = 0 ; i < size ; ++i){
            if(arr[i] > arr[i+1]){
                dropCount++ ;
                dropIndex = i ;
            }
        }

        if(dropCount == 0) return 0 ;  // already sorted 
        if(dropCount > 1) return -1 ;   // Can't be soted 

        // rotate the given array and check
        vector<int> sorted ;
        for(int i = dropIndex+1 ; i < size ; ++i){
            sorted.push_back(arr[i]) ;
        }
        for(int i = 0 ; i <= dropIndex ; ++i){
            sorted.push_back(arr[i]) ;
        }

        if(is_sorted(sorted.begin(), sorted.end())){
            return (size - (dropIndex+1)) ;
        }
        return -1 ;
    }
};
```

> Time Complexity - O(N)

> Space Complexity - O(N)

### Optimal Approach (above idea but space optimized)

```cpp
class Solution{
    public :
    int minOperationsToSort(vector<int>& arr){
        int size = arr.size(), dropIndex = -1 ;

        // Find the position where order breaks
        for(int i = 0 ; i < size-1 ; ++i){
            if(arr[i] > arr[i+1]){
                if(dropIndex != -1){
                    return -1 ;     // More than one drop => not possible
                }
                dropIndex = i ;
            }
        }

        // if already sorted 
        if(dropIndex == -1){
            return 0 ;
        }

        // Check if rotation after dropIndex sorts the array
        if(arr[size-1] <= arr[0]){
            // Verify full sorted order after dropIndex
            for(int i = dropIndex+1 ; i < size-1 ; ++i){
                if(arr[i] > arr[i+1]){
                    return -1 ;
                }
            }
            return size - (dropIndex+1) ;   // No of rotations needed
        }
        return -1 ;
    }
};
```

> Time Complexity - O(N)

> Space Complexity - O(1)