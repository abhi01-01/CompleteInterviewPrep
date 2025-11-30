### Leetcode - 141 - [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/description/)

```cpp
struct ListNode{
    int val ;
    ListNode *next ;
    ListNode(int x) : val(x), next(NULL) {}
};
class Solution{
    public :
    bool hasCycle(ListNode *head){
        set<ListNode*> st ;
        while(head != NULL){
            if(st.count(head)){
                return true ;
            }
            head = head->next ;
        }
        return false ;
    }
};
```

> Time Complexity - O(1*N)

> Space Complexity - O(1*N)

---

```cpp
class Solution{
    public :
    bool hasCycle(ListNode* head){
        ListNode *fast = head, *slow = head ;
        while(slow->next != NULL and fast->next->next != NULL){
            if(slow == fast){
                return true ;
            }
            slow = slow->next ;
            fast = fast->next->next ;
        }
        return false ; 
    }
};
```

> Time Complexity - O(1*N)

> Space Complexity - O(1)

