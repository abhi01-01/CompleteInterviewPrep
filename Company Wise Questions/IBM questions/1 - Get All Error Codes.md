### Get All Error Codes

Given timeStamps(vector of integers) represents timestamp in non decreasing order and logs(vector of string) represents errorcodes and 2 integers `t` and `k`. Find all errorcodes from logs which occurred at least k times within last t seconds.

like - 
```cpp
timeStamp = [100, 101, 102, 103, 105 108, 110]
logs     =  ["e1","e2","e3","e1","e1","e2"] 
        k = 2 
        t = 10 
```

### Solution

```cpp
class Solution{
    public :
    vector<string> getLogs(int t, int k, vector<int>& stamp, vector<string>& logs){
        int size = stamp.size() ;

        if(size == 0){
            return {} ;
        }

        unordered_map<string, int> counts ;

        int lastestStamp = stamp.back() ;
        int startTime = latestStamp-t+1 ;

        for(int i = size-1 ; i >= 0 ; --i){
            if(stamp[i] < startTime){
                break ;
            }
            counts[log[i]]++ ;
        }

        vector<string> result ;

        for(auto const& pair : counts){
            if(pair.second >= k){
                result.push_back(pair.first) ;
            }
        }
        return result ;
    }
};
```

> Time Complexity - O(N)

> Space Complexity - O(N)