### Leetcode - 206 - [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/description/)

1. Recursive Method

```cpp
// Definition of singly Linked List
struct ListNode{
    int val ;
    ListNode *next ;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(0), next(nullptr) {}
    ListNode(int x, ListNode *next) : val(x), next(next) {}
};

class Solution{
    public :
    ListNode* reverse(ListNode* head, ListNode* prev){
        if(head == NULL){
            return prev ;
        }
        ListNode* temp = head->next ;
        head->next = prev ;

        return reverse(temp, head) ;
    }
    ListNode* reverseList(ListNode* head){
        ListNode* prev = nullptr ;
        return reverse(head, prev) ;
    }
};
```
> Reversal Tree Diagram for `1->2->3->4->NULL`
>> ![LinkedListInPlaceReversal](LinkedListInPlaceReversal.jpg)

> Time Complexity - O(1*N)

> Space Complexity - O(1)

---

2.Iterative Method

```cpp
// Definition of singly Linked List
struct ListNode{
    int val ;
    ListNode *next ;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(0), next(nullptr) {}
    ListNode(int x, ListNode *next) : val(x), next(next) {}
};

class Solution{
    public :
    ListNode* reverseList(ListNode* head){
        ListNode* prev = nullptr ;
        
        while(head != NULL){
            ListNode* temp = head->next ;
            head->next = prev ;
            prev = head ;
            head = temp ;
        }
        return prev ;
    }
};
```

> Time Complexity - O(1*N)

> Space Complexity - O(1)