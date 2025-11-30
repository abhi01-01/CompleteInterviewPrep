## GFG - [Minimize Max Distance to Gas Station](https://www.geeksforgeeks.org/problems/minimize-max-distance-to-gas-station/1)

* 1 - Brute force

Intution behind this is to calculating all the gaps between stations and store it into priority queue.

“Keep adding points, one by one,
always inside the largest current gap.”

Because the largest gap is what defines the “max distance” right now —
reducing that has the biggest impact.

```cpp
class Solution {
  public:
    double minMaxDist(vector<int> &stations, int K) {
        // Code here
        int n = stations.size() ;
        
        // <updated_gap, <original_gap, added_stations>>
        using _pair = pair<double, pair<double, double>> ;
        priority_queue<_pair> maxHeap ;       // stores the gaps 
        for(int i = 0 ; (i+1) < n ; ++i){
            double gap = stations[i+1] - stations[i] ;
            maxHeap.push({gap,{gap, 0}}) ;
        }
        
        while(K > 0 and !maxHeap.empty()){
            _pair top = maxHeap.top() ;
            maxHeap.pop() ;
            double original_gap = top.second.first ;
            double added_stations = top.second.second + 1 ;
            double updated_gap = original_gap/(added_stations+1) ;
            maxHeap.push({updated_gap, {original_gap, added_stations}}) ;
            K-- ;
        }
        return (maxHeap.empty()) ? 0.00 : maxHeap.top().first ;
    }
};
```

> Time Complexity - O(2*NLogN)

> Space Complexity - O(N)

---

* 2 - optimize using binary search on answers


**The core logic idea**

You’re searching for a value:

“What is the smallest possible max distance (D) between adjacent points
after adding ≤ K new points?”

That’s a monotonic condition 👇

If you allow large D, it’s always possible ✅

If you try smaller D, maybe not ❌

So yep, binary search on the answer fits perfectly.


```cpp
class Solution {
  public:
  
    bool canDisburse(vector<int>& arr, int K, double maxDist){
        int countOfStat = 0, n = arr.size() ;
        
        for(int i = 0 ; (i+1) < n ; ++i){
            double gap = arr[i+1] - arr[i] ;
            countOfStat += (int)(ceil(gap/maxDist)) - 1;
        }
        return (countOfStat <= K) ;
    } 
    
    double minMaxDist(vector<int> &stations, int K) {
        // Code here
        double low = 0, high = (stations.back() - stations.front()) ;
        
        while((high-low) > 1e-6){       // Precision Control - Binary search on floating Numbers
            double mid = (high + low)/2.0 ;
            
            if(canDisburse(stations, K, mid)){
                high = mid ;    // feasible -> try smaller distance
            }
            else{
                low = mid ;         // infeasible -> try bigger distance
            }
        }
        return high ;
    }
};
```

> Time Complexity - O(NlogM)

> Space Complexity - O(1)