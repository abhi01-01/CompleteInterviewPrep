### Leetcode - 92 - [Reverse LinkedList II](https://leetcode.com/problems/reverse-linked-list-ii/)

```cpp
// Definition of singly linked list
struct ListNode{
    int val ;
    ListNode *next ;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode *next) : val(x), next(next) {}
};
class Solution{
    public :
    vector<ListNode*> reverse(ListNode *currNode, int right, int loop){
        ListNode *prev = NULL ;
        while(currNode != NULL){
            if(loop == 0){
                return {prev, currNode} ;
                break ;
            }
            ListNode* temp = currNode->next ;
            currNode->next = prev ;
            prev = currNode ;
            currNode = temp ;
            loop-- ;  
        }
    return {prev, currNode} ;
    }

    ListNode* reverseBetween(ListNode* head, int left, int right) {
        // base case
        if(head == NULL){
            return head ;
        }

        ListNode *prev = NULL ;
        ListNode *currptr = head ;
        vector<ListNode*> returnedNodes ;
        int nodeCount = 0 ;

        while(currptr != NULL){
            nodeCount++ ;
            if(nodeCount == left){
                returnedNodes = reverse(currptr, right, (right-nodeCount+1)) ;
                break ;
            }
            prev = currptr ;
            currptr = currptr->next ;
        }

        ListNode *returnedHead = returnedNodes[0] ;
        ListNode *returnedHeadNext = returnedNodes[1] ;
        if(prev == NULL){
            head = returnedHead ;
        }
        else{
            prev->next = returnedHead ;
        }
        currptr->next = returnedHeadNext ;
        return head ;     
    }
};
```
> Time Complexity - O(1*N)

> Space Complexity - O(1)