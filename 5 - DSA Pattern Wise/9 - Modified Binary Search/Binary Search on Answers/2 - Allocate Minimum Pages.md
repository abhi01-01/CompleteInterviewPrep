## GFG - [Allocate Minimum Pages](https://www.geeksforgeeks.org/problems/allocate-minimum-number-of-pages0937/1)

### 1. Naive Approach 

The approach is to search for the minimum possible value of the maximum number of pages that can be assigned to any student.

* The lowest possible page limit is the maximum number of pages in a single book, since that book must be assigned to some student.
* The highest possible page limit is the total number of pages across all books, which would happen if one student gets all the books.

To check if a given page limit can work, we simulate the process of assigning books to students:
 We start with the first student and keep assigning books one by one until adding the next book would exceed the current page limit. At that point, we assign books to the next student, and continue this process.

As soon as we find the smallest page limit that allows us to allocate all books to exactly k students, we return it.


```cpp
// function to check if books can be allocated to
// all k students without exceeding 'pageLimit'
bool check(vector<int> &arr, int k, int pageLimit) {
    
    // starting from the first student
    int cnt = 1;
    int pageSum = 0;
    for(int i = 0; i < arr.size(); i++) {
        
        // if adding the current book exceeds the page 
        // limit, assign the book to the next student
        if(pageSum + arr[i] > pageLimit) {
            cnt++;
            pageSum = arr[i];
        }
        else {
            pageSum += arr[i];
        }
    }
    
  	// if books can assigned to less than k students then
    // it can be assigned to exactly k students as well
    return (cnt <= k);
}

int findPages(vector<int> &arr, int k) {
    
    // if number of students are more than total books
    // then allocation is not possible
    if(k > arr.size())
        return -1;
        
    // minimum and maximum possible page limits
    int minPageLimit = *max_element(arr.begin(), arr.end());
    int maxPageLimit = accumulate(arr.begin(), arr.end(), 0);
    
    // iterating over all possible page limits
    for(int i = minPageLimit; i <= maxPageLimit; i++) {
        
        // return the first page limit with we can
        // allocate books to all k students
        if(check(arr, k, i))
            return i;
    }
    
    return -1;
}
```

> Time Complexity - O(n × (sum(arr) - max(arr)))

> Space Complexity - O(1)

---

### 2. Using Binary Search

The maximum number of pages (page limit) that a student can be allocated has a monotonic property:

* If at a page limit p, books cannot be allocated to all k students, then we need to reduce the page limit to ensure more students receive books.
* If at a page limit p, we can allocate books to more than k students, then we need to increase the page limit so that fewer students are allocated books.


Therefore, we can apply binary search to minimize the maximum pages a student can be allocated. To check the number of students that can be allotted books for any page limit, we start assigning books to the first student until the page limit is reached, then move to the next student.

```cpp
class Solution {
  public:
    bool check(vector<int>& arr, int k, int pageLimit){
        int students = 1 ;
        int pageSum = 0 ;
        
        for(int i = 0 ; i < arr.size() ; ++i){
            if((pageSum + arr[i]) > pageLimit ){
                students++ ;
                pageSum = arr[i] ;
            }
            else{
                pageSum += arr[i] ;
            }
        }
        return (students <= k) ;
    }
    
    int findPages(vector<int> &arr, int k) {
        // code here
        
        if(k > arr.size()) return -1 ;
        
        int minPageLimit = *max_element(arr.begin(), arr.end()) ;   // which is low
        int maxPageLimit = accumulate(arr.begin(), arr.end(), 0) ;  // which is high
        
        int ans = -1 ;          // to handle -1 condition wla case otherwise we can return high as we used to do
        
        while(minPageLimit <= maxPageLimit){
            
            int mid = minPageLimit + (maxPageLimit - minPageLimit)/2 ;
            
            if(check(arr, k, mid)){
                ans = mid ;
                maxPageLimit = mid - 1  ;
            }
            else{
                minPageLimit = mid + 1 ;
            }
            
        }
        
        return ans ;
    }
};
```

> Time Complexity - O(n × Log(sum(arr) - max(arr)))

> Space Complexity - O(1)
