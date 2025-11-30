>### 1. Sliding Window
>>The Sliding Window pattern is used to perform a required operation on a specific window size of a given array or linked list, such as finding the longest subarray containing all `1s`. Sliding Windows start from the `1st` element and keep shifting right by one element and adjust the length of the window according to the problem that you are solving. In some cases, the window size remains constant and in other cases the sizes grows or shrinks.
>><br>
![Sliding window](/DSA%20Pattern%20Wise/Pattern%20Wise%20DSA%20Problems%20from%20Different%20Sources/Hackernoon%20images/image.png)
>>
>Following are some ways you can identify that the given problem might require a sliding window:
>> * The problem input is a linear data structure such as a linked list, array, or string.
>> * You’re asked to find the longest/shortest substring, subarray, or a desired value.
>
>Common problems you use the sliding window pattern with:
>
>---
>> * [Maximum sum subarray of size ‘K’ (easy)]()
>>```cpp
>>class Solution {
>>  public:
>>    int maxSubarraySum(vector<int>& arr, int k) {
>>        int maxSum = 0, sum = 0, end = 0, start = 0, size = arr.size() ;
>>        while(end < size){
>>            sum += arr[end] ;
>>            while((end-start+1) > k and start < size){
>>                sum -= arr[start++] ;
>>            }
>>            maxSum = max(maxSum, sum) ;
>>            end++ ;
>>        }
>>        return maxSum ;
>>    }
>>};
>>```
>> Time Complesity - `O(N)`<br>
>> Space Complexity - `O(1)` 
>---
>> * [Longest substring with ‘K’ distinct characters (medium)](https://www.geeksforgeeks.org/problems/longest-k-unique-characters-substring0853/1)
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()`
>---
>> * [String anagrams (Medium)](https://www.geeksforgeeks.org/problems/anagram-1587115620/1)
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()`
>---
>> * [Find All Anagrams in a String (Medium)](https://leetcode.com/problems/find-all-anagrams-in-a-string/description/)
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()`
>---
---
<br>

>### 2. Two Pointers or Iterators
>>
>>Two Pointers is a pattern where two pointers iterate through the data structure in tandem until one or both of the pointers hit a certain condition.Two Pointers is often useful when searching pairs in a sorted array or linked list; for example, when you have to compare each element of an array to its other elements.
>>
>>Two pointers are needed because with just pointer, you would have to continually loop back through the array to find the answer. This back and forth with a single iterator is inefficient for time and space complexity — a concept referred to as asymptotic analysis. While the brute force or naive solution with 1 pointer would work, it will produce something along the lines of `O(n²)`. In many cases, two pointers can help you find a solution with better space or runtime complexity.
>>
>> ![Two Pointers](/DSA%20Pattern%20Wise/Pattern%20Wise%20DSA%20Problems%20from%20Different%20Sources/Hackernoon%20images/image-1.png)
>
>Ways to identify when to use the Two Pointer method:
>>It will feature problems where you deal with sorted arrays (or Linked Lists) and need to find a set of elements that fulfill certain constraints
>>The set of elements in the array is a pair, a triplet, or even a subarray
>
>Here are some problems that feature the Two Pointer pattern:
>
>---
>> * [Squaring a sorted array (easy)]()
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()` 
>---
>> * [Triplets that sum to zero (medium)]()
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()` 
>---
>> * [Comparing strings that contain backspaces (medium)]()
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()` 
>---
---
<br>

> ### 3. Fast and Slow pointers
>>
>>The Fast and Slow pointer approach, also known as the Hare & Tortoise algorithm, is a pointer algorithm that uses two pointers which move through the array (or sequence/linked list) at different speeds. This approach is quite useful when dealing with cyclic linked lists or arrays.
>>
>>By moving at different speeds (say, in a cyclic linked list), the algorithm proves that the two pointers are bound to meet. The fast pointer should catch the slow pointer once both the pointers are in a cyclic loop.<br>
>><br>
>> ![Fast and Slow Pointer](/DSA%20Pattern%20Wise/Pattern%20Wise%20DSA%20Problems%20from%20Different%20Sources/Hackernoon%20images/fastandslow.png)
>><br>
>
>How do you identify when to use the Fast and Slow pattern?
>>
>> * The problem will deal with a loop in a linked list or array
>> * When you need to know the position of a certain element or the overall length of the linked list.
>
> When should I use it over the Two Pointer method mentioned above?
>> * There are some cases where you shouldn’t use the Two Pointer approach such as in a singly linked list where you can’t move in a backwards direction. An example of when to use the Fast and Slow pattern is when you’re trying to determine if a linked list is a palindrome.
>
>Problems featuring the fast and slow pointers pattern:
>
>---
>> * [Linked List Cycle (easy)]()
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()` 
>---
>> * [Palindrome Linked List (medium)]()
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()` 
>---
>> * [Cycle in a Circular Array (hard)]()
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()` 
>---
---
<br>

> ### 4. Merge Intervals
>>
>>The Merge Intervals pattern is an efficient technique to deal with overlapping intervals. In a lot of problems involving intervals, you either need to find overlapping intervals or merge intervals if they overlap. The pattern works like this:
>>
>> Given two intervals (`‘a’` and `‘b’`), there will be six different ways the two intervals can relate to each other: <br>
>><br>
>> ![merge intervals](/DSA%20Pattern%20Wise/Pattern%20Wise%20DSA%20Problems%20from%20Different%20Sources/Hackernoon%20images/mergeintervals.png)
>><br>
>
> Understanding and recognizing these six cases will help you help you solve a wide range of problems from inserting intervals to optimizing interval merges.
>
>How do you identify when to use the Merge Intervals pattern?
>>
>> * If you’re asked to produce a list with only mutually exclusive intervals
>> * If you hear the term “overlapping intervals”.
>
> Merge interval problem patterns:
>> ---
>> * [Intervals Intersection (medium)]()
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()` 
>---
>> * [Maximum CPU Load (hard)]()
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()` 
>---
---
<br>

> ### 5. Cyclic sort
>>
>>This pattern describes an interesting approach to deal with problems involving arrays containing numbers in a given range. The Cyclic Sort pattern iterates over the array one number at a time, and if the current number you are iterating is not at the correct index, you swap it with the number at its correct index. You could try placing the number in its correct index, but this will produce a complexity of `O(n^2)` which is not optimal, hence the Cyclic Sort pattern.<br>
>> <br>
>> ![cyclicsort](/DSA%20Pattern%20Wise/Pattern%20Wise%20DSA%20Problems%20from%20Different%20Sources/Hackernoon%20images/cyclicsort.png)
>><br>
>
>How do I identify this pattern?
>>
>> * They will be problems involving a sorted array with numbers in a given range.
>> * If the problem asks you to find the missing/duplicate/smallest number in an sorted/rotated array
>
>Problems featuring cyclic sort pattern:
>
>---
>> * [Find the Missing Number (easy)]()
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()` 
>---
>> * [Find the Smallest Missing Positive Number (medium)]()
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()` 
>---
---
<br>

> ### 6. In-place reversal of linked list
>>
>>In a lot of problems, you may be asked to reverse the links between a set of nodes of a linked list. Often, the constraint is that you need to do this in-place, i.e., using the existing node objects and without using extra memory. This is where the above mentioned pattern is useful.
>>
>>This pattern reverses one node at a time starting with one variable (current) pointing to the head of the linked list, and one variable (previous) will point to the previous node that you have processed. In a lock-step manner, you will reverse the current node by pointing it to the previous before moving on to the next node. Also, you will update the variable “previous” to always point to the previous node that you have processed.<br>
>><br>
>> ![reversal](/DSA%20Pattern%20Wise/Pattern%20Wise%20DSA%20Problems%20from%20Different%20Sources/Hackernoon%20images/reversal.png)
>><br>
>
>How do I identify when to use this pattern:
>>
>> * If you’re asked to reverse a linked list without using extra memory
>
>Problems featuring in-place reversal of linked list pattern::
>
>---
>> * [Reverse a Sub-list (medium)]()
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()` 
>---
>> * [Reverse every K-element Sub-list (medium)]()
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()` 
>---
---
<br>

> ### 7. Tree BFS
>>
>>This pattern is based on the Breadth First Search (BFS) technique to traverse a tree and uses a queue to keep track of all the nodes of a level before jumping onto the next level. Any problem involving the traversal of a tree in a level-by-level order can be efficiently solved using this approach.
>>
>>The Tree BFS pattern works by pushing the root node to the queue and then continually iterating until the queue is empty. For each iteration, we remove the node at the head of the queue and “visit” that node. After removing each node from the queue, we also insert all of its children into the queue.<br>
>
>How to identify the Tree BFS pattern:
>>
>> * If you’re asked to traverse a tree in a level-by-level fashion (or level order traversal).
>
>Problems featuring Tree BFS pattern:
>
>---
>> * [Binary Tree Level Order Traversal (easy)]()
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()` 
>---
>> * [Zigzag Traversal (medium)]()
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()` 
>---
---
<br>


> ### 8. Tree DFS
>>
>>Tree DFS is based on the Depth First Search (DFS) technique to traverse a tree. You can use recursion (or a stack for the iterative approach) to keep track of all the previous (parent) nodes while traversing.
>>
>>The Tree DFS pattern works by starting at the root of the tree, if the node is not a leaf you need to do three things:<br>
>>> 1. Decide whether to process the current node now (pre-order), or between processing two children (in-order) or after processing both children (post-order).
>>> 2. Make two recursive calls for both the children of the current node to process them.
>
>How to identify the Tree DFS pattern:
>>
>> * If you’re asked to traverse a tree with in-order, preorder, or postorder DFS.
>> * If the problem requires searching for something where the node is closer to a leaf
>
>Problems featuring Tree DFS pattern:
>
>---
>> * [Sum of Path Numbers (medium)]()
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()` 
>---
>> * [All Paths for a Sum (medium)]()
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()` 
>---
---
<br>

> ### 9. Two heaps
>>
>>In many problems, we are given a set of elements such that we can divide them into two parts. To solve the problem, we are interested in knowing the smallest element in one part and the biggest element in the other part. This pattern is an efficient approach to solve such problems.
>>
>>This pattern uses two heaps; A Min Heap to find the smallest element and a Max Heap to find the biggest element. The pattern works by storing the first half of numbers in a Max Heap, this is because you want to find the largest number in the first half. You then store the second half of numbers in a Min Heap, as you want to find the smallest number in the second half. At any time, the median of the current list of numbers can be calculated from the top element of the two heaps.<br>
>
>Ways to identify the Two Heaps pattern:
>>
>> * Useful in situations like Priority Queue, Scheduling.
>> * If the problem states that you need to find the smallest/largest/median elements of a set.
>> * Sometimes, useful in problems featuring a binary tree data structure.
>
>Problems featuring two heaps:
>
>---
>> * [Find the Median of a Number Stream (hard)](https://leetcode.com/problems/find-median-from-data-stream/description/)
>>
>> ![lc295](/DSA%20Pattern%20Wise/Pattern%20Wise%20DSA%20Problems%20from%20Different%20Sources/Hackernoon%20images/lc295.png)
>>```cpp
>>class MedianFinder {
>>public:
>>    priority_queue<int> maxHeap ;
>>    priority_queue<int, vector<int>, greater<int>> minHeap ;
>>
>>    MedianFinder() {
>>        
>>    }
>>    
>>    void addNum(int num) {
>>        maxHeap.push(num) ;
>>        minHeap.push(maxHeap.top()) ;
>>        maxHeap.pop() ;
>>        if(minHeap.size() > maxHeap.size()){
>>            maxHeap.push(minHeap.top()) ;
>>            minHeap.pop() ;
>>        }
>>    }
>>    
>>    double findMedian() {
>>        if(maxHeap.size() > minHeap.size()) return maxHeap.top() ;
>>        else if(maxHeap.size() == minHeap.size()){
>>            return (double)(maxHeap.top() + minHeap.top())/2 ;
>>        }
>>        return 0 ;
>>    }
>>};
>>```
>> Time Complesity - `O(N)`<br>
>> Space Complexity - `O(N)`  
>---
---
<br>


> ### 10. Subsets
>>
>>A huge number of coding interview problems involve dealing with Permutations and Combinations of a given set of elements. The pattern Subsets describes an efficient Breadth First Search (BFS) approach to handle all these problems.<br>
>><br>
>> ![subsets](/DSA%20Pattern%20Wise/Pattern%20Wise%20DSA%20Problems%20from%20Different%20Sources/Hackernoon%20images/subsets.png)
>><br>
>
>How to identify the Subsets pattern:
>>
>> * Problems where you need to find the combinations or permutations of a given set.
>
>Problems featuring Subsets pattern:
>
>---
>> * [Subsets With Duplicates (easy)]()
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()` 
>---
>> * [String Permutations by changing case (medium)]()
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()` 
>---
---
<br>


> ### 11. Modified binary search
>>
>>Whenever you are given a sorted array, linked list, or matrix, and are asked to find a certain element, the best algorithm you can use is the Binary Search. This pattern describes an efficient way to handle all problems involving Binary Search.
>
>The patterns looks like this for an ascending order set:
>> 1. First, find the middle of start and end. An easy way to find the middle would be: `middle = (start + end) / 2`. But this has a good chance of producing an integer overflow so it’s recommended that you represent the middle as: `middle = start + (end — start) / 2.`
>> 2. If the key is equal to the number at index middle then return middle.
>> 3. If `‘key’` isn’t equal to the index middle:
>> 4. Check if `key < arr[middle]`. If it is reduce your search to `end = middle — 1.`
>> 5. Check if `key > arr[middle]`. If it is reduce your search to `end = middle + 1.`
>
> Here is a visual representation of the Modified Binary Search pattern:<br>
><br>
> ![modifiedbs](/DSA%20Pattern%20Wise/Pattern%20Wise%20DSA%20Problems%20from%20Different%20Sources/Hackernoon%20images/modifiedbs.png)
>
>Problems featuring the Modified Binary Search pattern:
>
>---
>> * [Order-agnostic Binary Search (easy)]()
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()` 
>---
>> * [Search in a Sorted Infinite Array (medium)]()
>>```cpp
>>```
>> Time Complesity - `O()`<br>
>> Space Complexity - `O()`
>---
---
<br>

> ### 12. Top K elements
>>
>>Any problem that asks us to find the top/smallest/frequent ‘K’ elements among a given set falls under this pattern.
>>
>>The best data structure to keep track of `‘K’` elements is Heap. This pattern will make use of the Heap to solve multiple problems dealing with ‘K’ elements at a time from a set of given elements. The pattern looks like this:
>>> 1. Insert `‘K’` elements into the min-heap or max-heap based on the problem.
>>> 2. Iterate through the remaining numbers and if you find one that is larger than what you have in the heap, then remove that number and insert the larger one.
>>
>>
>> ![topkele](/DSA%20Pattern%20Wise/Pattern%20Wise%20DSA%20Problems%20from%20Different%20Sources/Hackernoon%20images/topkele.png)
>><br>
>
>There is no need for a sorting algorithm because the heap will keep track of the elements for you.
>
>How to identify the Top `‘K’` Elements pattern:
>>
>> * If you’re asked to find the top/smallest/frequent `‘K’` elements of a given set.
>> * If you’re asked to sort an array to find an exact element.
>
>Problems featuring Top `‘K’` Elements pattern:
>
>---
>> * [Top ‘K’ Numbers (easy)]()
>> ```cpp
>> class Solution{
>> public :
>>     vector<int> findKthLargest(vector<int>& nums, int k) {
>>         priority_queue<int, vector<int>, greater<int>> minHeap ;
>>         for(auto const& num : nums){
>>             minHeap.push(num) ;
>>             if(minHeap.size() > k)
>>                 minHeap.pop() ; 
>>         }
>>         vector<int> result ;
>>         while(!minHeap()){
>>             int ele = minHeap.top() ;
>>             result.push_back(ele) ;
>>             minHeap.pop() ;
>>         }
>>         return result ;
>>     }
>> };
>> ```
>> Time Complesity - `O(NLogK)`<br>
>> Space Complexity - `O(N)`
>---
>> * [Top ‘K’ Frequent Numbers (medium)](https://leetcode.com/problems/top-k-frequent-elements/description/)
>> ```cpp
>> class Solution{
>> public :
>>     int topKFrequentElements(vector<int>& nums, int k){
>>         unordered_map<int, int> count ;
>>         for(auto const& num : nums){
>>             count[num]++ ;
>>         }
>>         // <frequency, num>
>>         using _pair = pair<int, int> ;
>>         priority_queue<_pair, vector<_pair>, greater<_pair>> minHeap ;
>> 
>>         for(auto const& p : count){
>>             minHeap.push({p.second, p.first}) ;
>>             if(minHeap.size() > k){
>>                 minHeap.pop() ;
>>             }
>>         }
>>         vector<int> result ;
>>         
>>         while(!minHeap.empty()){
>>             int ele = minHeap.top().second ;
>>             result.push_back(ele) ;
>>             minHeap.pop() ;
>>         }
>>         return result ;
>>     }
>> };
>> ```
>> Time Complesity - `O(NLogK)`<br>
>> Space Complexity - `O(N)` 
>---
---
<br>


> ### 13. K-way Merge
>>
>>K-way Merge helps you solve problems that involve a set of sorted arrays.
>>
>>Whenever you’re given ‘K’ sorted arrays, you can use a Heap to efficiently perform a sorted traversal of all the elements of all arrays. You can push the smallest element of each array in a Min Heap to get the overall minimum. After getting the overall minimum, push the next element from the same array to the heap. Then, repeat this process to make a sorted traversal of all elements.<br>
>><br>
>> ![kwaymerge](/DSA%20Pattern%20Wise/Pattern%20Wise%20DSA%20Problems%20from%20Different%20Sources/Hackernoon%20images/kwaymerge.png)
>><br>
>
>The pattern looks like this:
>> * Insert the first element of each array in a Min Heap.
>> * After this, take out the smallest (top) element from the heap and add it to the merged list.
>> * After removing the smallest element from the heap, insert the next element of the same list into the heap.
>> * Repeat steps `2` and `3` to populate the merged list in sorted order.
>
>How to identify the K-way Merge pattern:
>>
>> * The problem will feature sorted arrays, lists, or a matrix
>> * If the problem asks you to merge sorted lists, find the smallest element in a sorted list.
>
> Problems featuring the K-way Merge pattern:
>
>---
>> * [Merge K Sorted Lists (medium)](https://leetcode.com/problems/merge-k-sorted-lists/description/)
>> 1. Solution - 01
>>```cpp
>>class Solution {
>>public:
>>    ListNode* mergeTwoLists(ListNode *list1, ListNode *list2){
>>        if(list1 == NULL) return list2 ;
>>        if(list2 == NULL) return list1 ;
>>
>>        if(list1->val < list2->val){
>>            list1->next = mergeTwoLists(list1->next, list2) ;
>>            return list1 ;
>>        }
>>        else{
>>            list2->next = mergeTwoLists(list1, list2->next) ;
>>            return list2 ;
>>        }
>>    }
>>
>>    ListNode* mergeKLists(vector<ListNode*>& lists) {
>>        ListNode *temp = NULL ;
>>
>>        for(int i = 0 ; i < lists.size() ; ++i ){
>>            temp = mergeTwoLists(temp, lists[i]) ;
>>        }
>>        return temp ;
>>    }
>>};
>>```
>> Time Complesity - `O(N^2)`<br>
>> Space Complexity - `O(N)` <br>
>> <br>
>> 2. Solution - 02
>>```cpp
>>class Solution {
>>public:
>>    ListNode* mergeKLists(vector<ListNode*>& lists) {
>>        if(lists.empty()) return nullptr ;
>>        priority_queue<pair<int, ListNode*>, vector<pair<int, ListNode*>>, greater<pair<int, ListNode*>>> minHeap ;
>>        for(int i = 0 ; i < lists.size() ; ++i ){
>>            if(lists[i] != NULL)
>>                minHeap.emplace(lists[i]->val, lists[i]) ;
>>        }
>>
>>        ListNode *dummyNode = new ListNode(-1) ;
>>        ListNode *dummyPtr = dummyNode ;
>>
>>        while(!minHeap.empty()){
>>            auto [intVal, node] = minHeap.top() ; minHeap.pop() ;
>>            if(node->next != NULL){
>>                minHeap.emplace(node->next->val, node->next) ;
>>            }
>>            dummyPtr->next = node ;
>>            dummyPtr = dummyPtr->next ;
>>        }
>>        return dummyNode->next ; 
>>    }
>>};
>>```
>> Time Complexity - O(N^2) <br>
>> Space Complexity - O(N^2)
>---
>> * [K Pairs with Smallest Sums (Hard)](https://leetcode.com/problems/find-k-pairs-with-smallest-sums/description/) - Similar [Maximum Sum Combination](https://www.geeksforgeeks.org/problems/maximum-sum-combination/1)
>> 1. Naive Approach
>>```cpp
>>class Solution {
>>public:
>>    vector<vector<int>> kSmallestPairs(vector<int>& nums1, vector<int>& nums2, int k) {
>>        int n = nums1.size() ;
>>        int m = nums2.size() ;
>>        // pair = pair<nums1[i] + nums2[j], pair<nums1[i], nums2[j]>>
>>        using _pair = pair<int, pair<int, int>> ;
>>        priority_queue<_pair> maxHeap ;
>>        for(int i = 0 ; i < n ; ++i){
>>            for(int j = 0 ; j < m ; ++j){
>>                _pair temp = make_pair(nums1[i] + nums2[j], make_pair(nums1[i], nums2[j]));
>>                maxHeap.emplace(temp) ;
>>                if(maxHeap.size() > k) maxHeap.pop() ;
>>            }
>>        }
>>        vector<vector<int>> KsmallestPairs_ ;
>>        while(k > 0){
>>            _pair top = maxHeap.top() ;
>>            maxHeap.pop() ;
>>            int a = top.second.first ;
>>            int b = top.second.second ;
>>            KsmallestPairs_.push_back({a, b}) ;
>>            --k ;
>>        } 
>>        return KsmallestPairs_ ;
>>    }
>>};
>>```
>> Time Complesity - `O(N^2log(N^2))`<br>
>> Space Complexity - `O(N^2)` <br>
>> <br>
>> 2. Optimal Solution - 
>>```cpp
>>class Solution {
>>public:
>>    vector<vector<int>> kSmallestPairs(vector<int>& nums1, vector<int>& nums2, int k) {
>>        int n = nums1.size() ;
>>        int m = nums2.size() ;
>>        // pair = pair<nums1[i] + nums2[j], pair<nums1[i], nums2[j]>>
>>        using _pair = pair<int, pair<int, int>> ;
>>        priority_queue<_pair, vector<_pair>, greater<_pair>> minHeap ;
>>        vector<vector<int>> KsmallestPairs_ ;
>>        set<pair<int, int>> isVisited ;   // to acoid duplicate insertion of pairs
>>
>>        // nums are sorted so 1st pair (0, 0) will be the smallest sum pair
>>
>>        isVisited.insert({0, 0}) ;
>>        minHeap.push({nums1[0]+nums2[0], {0, 0}}) ;
>>
>>        while(!minHeap.empty() and k > 0){
>>            _pair top = minHeap.top() ;
>>            minHeap.pop() ;
>>            int i = top.second.first ;
>>            int j = top.second.second ;
>>            KsmallestPairs_.push_back({nums1[i], nums2[j]}) ;
>>
>>            if((i+1) < n and j < m and isVisited.find({i+1, j}) == isVisited.end()){
>>                minHeap.push({(nums1[i+1]+nums2[j]), {i+1, j}}) ;
>>                isVisited.insert({i+1, j}) ;
>>            }
>>            if(i < n and (j+1) < m and isVisited.find({i, j+1}) == isVisited.end()){
>>                minHeap.push({(nums1[i]+nums2[j+1]), {i, j+1}}) ;
>>                isVisited.insert({i, j+1}) ;
>>            }
>>            --k ;
>>        } 
>>        return KsmallestPairs_ ;
>>    }
>>};
>>```
>> Time Complexity - `O(KlogK)`<br>
>> Space Complexity - `O(K)`
>---
---
<br>


> ### 14. Topological sort
>>
>>Topological Sort is used to find a linear ordering of elements that have dependencies on each other. For example, if event `‘B’` is dependent on event `‘A’`, `‘A’` comes before `‘B’` in topological ordering.
>>
>>This pattern defines an easy way to understand the technique for performing topological sorting of a set of elements.
>
> The pattern works like this:
>> 1. Initialization
>>> * Store the graph in adjacency lists by using a HashMap.<br>
>>> * To find all sources, use a HashMap to keep the count of in-degreesBuild the graph and find in-degrees of all vertices.
>>
>> 2. Build the graph from the input and populate the in-degrees HashMap.
>> 3. Find all sources
>>> * All vertices with `‘0’` in-degrees will be sources and are stored in a Queue.
>>
>> 4. Sort
>>> a) For each source, do the following things:
>>>> * Add it to the sorted list.
>>>> * Get all of its children from the graph.
>>>> * Decrement the in-degree of each child by `1`.
>>>> * If a child’s in-degree becomes `‘0’`, add it to the sources Queue.
>>>
>>> b) Repeat (a), until the source Queue is empty.<br>
>>
>> ![toposort](/DSA%20Pattern%20Wise/Pattern%20Wise%20DSA%20Problems%20from%20Different%20Sources/Hackernoon%20images/toposort.png)
>><br>
>
>How to identify the Topological Sort pattern:
>>
>> * The problem will deal with graphs that have no directed cycles.
>> * If you’re asked to update all objects in a sorted order.
>> * If you have a class of objects that follow a particular order
>
>Problems featuring the Topological Sort pattern:
>
>---
>> * [Task scheduling (medium)](https://leetcode.com/problems/task-scheduler/description/)
>> 1. Solution - 01
>>```cpp
>>class Solution {
>>public:
>>    int leastInterval(vector<char>& tasks, int n) {
>>        vector<int> frequency(26, 0) ;
>>        for(auto& task : tasks){
>>            frequency[task-'A']++ ;
>>        }
>>        using _pair = pair<int, char> ;
>>        priority_queue<_pair> maxHeap ;
>>
>>        for(int i = 0 ; i < 26 ; ++i){
>>            if(frequency[i] > 0){
>>                maxHeap.push({frequency[i], (i+'A')}) ;
>>            }
>>        }
>>        int time = 0 ;
>>        vector<char> ans ;
>>        stack<_pair> store ;
>>        while(!maxHeap.empty()){
>>            int cycle = n+1 ;
>>            int taskCounter = 0 ;
>>            while(cycle > 0 and !maxHeap.empty()){
>>                // topElement.first = freuqency, topElement.second = char
>>                _pair topElement = maxHeap.top() ;
>>                maxHeap.pop() ;
>>                if(topElement.first > 1){
>>                    store.push({topElement.first-1, topElement.second}) ;
>>                }
>>                ans.push_back(topElement.second) ;
>>                taskCounter++ ;
>>                --cycle ;
>>            }
>>            while(!store.empty()){
>>                maxHeap.push(store.top()) ;
>>                store.pop() ;
>>            }
>>            if(!maxHeap.empty()){
>>                while(taskCounter < (n+1)){
>>                    ans.push_back('*') ;
>>                    taskCounter++ ;
>>                }
>>            }
>>            time += taskCounter ;
>>        }
>>        //for(auto c : ans) cout << c << " " ;
>>        return time ;
>>    }
>>};
>>```
>> Time Complesity - `O(N)`<br>
>> Space Complexity - `O(N)` <br>
>> <br>
>> 2. Solution - 02 
>>```cpp
>>class Solution {
>>public:
>>    int leastInterval(vector<char>& tasks, int n) {
>>        vector<int> frequency(26, 0) ;
>>        for(auto& task : tasks){
>>            frequency[task-'A']++ ;
>>        }
>>        // either sort or push into maxHeap to work with maxFreq
>>        sort(frequency.begin(), frequency.end()) ;
>>        int maxFreq = frequency.back()-1 ;
>>        // if the maxFreq task is placed on scale, calculating gaps b/w 
>>        int idleSlots = maxFreq*n ;
>>
>>        // iterate over 2nd frequent task to least frequest task and palce these b/w gaps
>>        for(int i = 24 ; i >= 0 and frequency[i] > 0 ; --i){
>>            // place minimum of maximum frequency and current frequency taks b/w gaps
>>            idleSlots -= min(maxFreq, frequency[i]) ;
>>        }
>>
>>        // if any idle/gaps left add them with total number of slots
>>        return (idleSlots > 0) ? (idleSlots + tasks.size()) : tasks.size() ;
>>    }
>>};
>>```
>> Time Complesity - `O(N)`<br>
>> Space Complexity - `O(1)`
>---
>> * [Minimum height of a tree (hard)](https://leetcode.com/problems/minimum-height-trees/description/)
>> 1. Brute Force
>>```cpp
>>class Solution {
>>public:
>>    // measure height from all nodes and return the all min heightts
>>    int findHeight(int root, vector<vector<int>>& adjList){
>>        queue<int> q ;
>>        q.push(root) ;
>>        int level = 0 ;
>>        vector<bool> isVisited(adjList.size(), false) ;
>>        isVisited[root] = true ;
>>        while(!q.empty()){
>>            int currQSize = q.size() ;
>>            for(int i = 0 ; i < currQSize ; ++i){
>>                int frontNode = q.front() ;
>>                q.pop() ;
>>                for(auto &adj : adjList[frontNode]){
>>                    if(isVisited[adj] == false){
>>                        q.push(adj) ;
>>                        isVisited[adj] = true ;
>>                    }
>>                }
>>            }
>>            level++ ;
>>        }
>>        return level-1 ;
>>    }
>>
>>    vector<int> findMinHeightTrees(int n, vector<vector<int>>& edges) {
>>        vector<vector<int>> adjList(n) ;
>>        for(auto e : edges){
>>            adjList[e[0]].push_back(e[1]) ;
>>            adjList[e[1]].push_back(e[0]) ;
>>        }
>>
>>        vector<vector<int>> heights ;
>>        for(int i = 0 ; i < n ; ++i){
>>            int height = findHeight(i, adjList) ;
>>            heights.push_back({height, i}) ;
>>        }
>>        sort(heights.begin(), heights.end()) ;
>>
>>        vector<int> minHeightTrees ;
>>        minHeightTrees.push_back(heights[0][1]) ;
>>
>>        for(int i = 1 ; i < heights.size() ; ++i){
>>            if(heights[i][0] == heights[0][0]){
>>                minHeightTrees.push_back(heights[i][1]) ;
>>            }
>>            //cout << "height" << heights[i][0] << " " << "Node" << heights[i][1] << "\n" ;
>>        }
>>
>>        return minHeightTrees ;
>>    }
>>};
>>```
>> Time Complesity - `O(N^2)`<br>
>> Space Complexity - `O(N)` <br>
>> <br>
>> 2. Optimal Solution
>>```cpp
>>class Solution {
>>public:
>>    vector<int> findMinHeightTrees(int n, vector<vector<int>>& edges) {
>>        // edge case
>>        if(n==1) return {0} ;
>>        // make adjacency list of all the nodes
>>        vector<unordered_set<int>> adjList(n) ;
>>        for(auto& e : edges){
>>            adjList[e[0]].insert(e[1]) ;
>>            adjList[e[1]].insert(e[0]) ;            
>>        }
>>        // push all the leaf nodes into the queue 
>>        queue<int> q ;
>>        for(int i = 0 ; i < n ; ++i){
>>            if(adjList[i].size() == 1){
>>                q.push(i) ;
>>            }
>>        }
>>        int level = 0 ;
>>        while(n > 2){
>>            int qCurrSize = q.size() ;
>>            n -= qCurrSize ; 
>>            for(int i = 0 ; i < qCurrSize ; ++i){
>>                int frontNode = q.front() ;
>>                q.pop() ;
>>                for(auto& adj : adjList[frontNode]){
>>                    // since adj is adjacent of frontNode and vice versa is ture, since we are shrinking to middle 
>>                    // so remove frontNode as adjacent node for its neighbours
>>                    adjList[adj].erase(frontNode) ;
>>
>>                    // if the adj node is leafNode now, push it into queue
>>                    if(adjList[adj].size() == 1){
>>                        q.push(adj) ;
>>                    }
>>                }
>>
>>            }
>>            level++ ;
>>        }
>>        vector<int> minTreeNodes ;
>>
>>        while(!q.empty()){
>>            minTreeNodes.push_back(q.front()) ;
>>            q.pop() ;
>>        }
>>        cout << level ;
>>        return minTreeNodes ;
>>    }
>>};
>>```
>> Time Complesity - `O(N)`<br>
>> Space Complexity - `O(N)` <br>
>> Optimal Solution Reference - [Reference-1](https://leetcode.com/problems/minimum-height-trees/submissions/1240262260/), [Reference-2](https://stackoverflow.com/questions/63237671/how-many-minimum-height-trees-mhts-can-a-graph-have-at-most), [Reference-3](https://en.wikipedia.org/wiki/Centered_tree#:%7E:text=A%20graph%20can%20have%20an), [Reference-4](https://cs.stackexchange.com/questions/2615/prove-that-every-two-longest-paths-have-at-least-one-vertex-in-common/2622#2622)
>---
---
<br>



[Source](https://hackernoon.com/14-patterns-to-ace-any-coding-interview-question-c5bb3357f6ed)
