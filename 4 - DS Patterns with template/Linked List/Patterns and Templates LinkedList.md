# Linked List (6 Patterns)

### ✅ $Pattern 1 — Two-Pointer (Fast $&$ Slow Pointer)$

This is the GOD pattern of linked lists.

Used for:
* finding middle
* detecting cycle
* cycle entry
* palindrome
* reordering list
* remove nth node from end

Template:

```cpp
ListNode *slow = head, *fast = head;

while (fast && fast->next) {
    slow = slow->next;
    fast = fast->next->next;
}
```

> Problems:
>> * LC 876: Middle of Linked List
>> * LC 141: Cycle Detection (Floyd)
>> * LC 142: Cycle Entry Point
>> * LC 234: Palindrome Linked List
>> * LC 19: Remove Nth Node From End
>> * LC 143: Reorder List

Why this works:

Floyd’s algorithm lets you extract structure without extra memory.

### ✅ $Pattern 2 — In-Place Reversal (Reverse List or Sublist)$

If problem requires:
* reversing whole list
* reversing nodes in k-groups
* reverse a portion
* reorder + reverse operations

Template:

```cpp
ListNode *prev = NULL, *cur = head;

while (cur) {
    ListNode *next = cur->next;
    cur->next = prev;
    prev = cur;
    cur = next;
}
return prev;
```

> Problems:
>> * LC 206: Reverse Linked List
>> * LC 92: Reverse Linked List II
>> * LC 25: Reverse Nodes in k-Group
>> * LC 143: Reorder List

### ✅ $Pattern 3 — Merge / Split Lists$

Very common in:
* merging two sorted lists
* merge k sorted lists
* partition list
* split list into halves for merge sort
* odd-even arranging

Merging template:
```cpp
ListNode *dummy = new ListNode(), *tail = dummy;

while (l1 && l2) {
    if (l1->val < l2->val) tail->next = l1, l1 = l1->next;
    else tail->next = l2, l2 = l2->next;
    tail = tail->next;
}
tail->next = l1 ? l1 : l2;
return dummy->next;
```

> Problems:
>> * LC 21: Merge Two Sorted Lists
>> * LC 23: Merge k Sorted Lists
>> * LC 148: Sort List
>> * LC 328: Odd Even Linked List
>> * LC 86: Partition List

### ✅ $Pattern 4 — Pointer Manipulation (Deletion / Insertion Tricks)$

Used for:
* removing node when only pointer to node is given
* delete duplicates in sorted list
* remove Nth
* swap nodes
* reorder

Template (removal):

```cpp
ListNode *dummy = new ListNode(0, head);
ListNode *cur = dummy;

while (cur->next) {
    if (shouldDelete(cur->next))
        cur->next = cur->next->next;
    else
        cur = cur->next;
}
return dummy->next;
```

> Problems:
>> * LC 237: Delete Node in Linked List
>> * LC 83: Remove Duplicates
>> * LC 82: Remove Duplicates II
>> * LC 19: Remove Nth
>> * LC 24: Swap Nodes

### ✅ $Pattern 5 — Using Extra Structure (HashSet / HashMap)$

Used when:
* detecting cycles with memory
* deep copy list with random pointer
* remove loops
* caching linked list states

HashSet template:

```cpp
unordered_set<ListNode*> seen;

while (node) {
    if (seen.count(node)) return true;
    seen.insert(node);
    node = node->next;
}
```

> Problems:
>> * LC 138: Copy List with Random Pointer
>> * Detect cycle (non-Floyd)
>> * Remove loop

### ✅ $Pattern 6 — Simulation with Multiple Pointers$

This pattern includes:
* rotating list
* interleaving nodes
* zig-zag lists
* pointer weaving / splitting

Template:

```cpp
ListNode *cur = head;
while (cur) {
    // connect cur->next->something
    // jump cur = cur->next->next
}
```

> Problems:
>> * LC 138: Copy Random List (interleave nodes)
>> * LC 61: Rotate List
>> * LC 143: Reorder List
>> * LC 725: Split Linked List in Parts

---

### <span style="color:yellow">HOW TO RECOGNIZE LINKED LIST PATTERNS?</span>

Ask:

✔️ Need middle? → fast/slow <br>
✔️ Need end-of-list or k-th from end? → fast/slow <br>
✔️ Need to reverse? → reverse pattern<br>
✔️ Need to rearrange groups/chunks? → reversal or merging<br>
✔️ Need to merge lists? → merging template<br>
✔️ Need to duplicate or track nodes? → hash map<br>
✔️ Complex pointer dance? → simulation pattern<br>

If ANY of these appear → linked list pattern detected.

**LINKED LIST CHEAT CODE**

* If pointers interact → simulate
* If two halves matter → fast/slow
* If ordering matters → merge
* If reversing direction → reverse pattern
* If deep coping needed → interleaving nodes trick

---

### <span style="color:yellow">PROBLEMS</span>

🟢 Easy:

> LC 21: Merge Two Lists
> 
> LC 83: Remove Duplicates
> 
> LC 206: Reverse List
> 
> LC 141: Detect Cycle

🟡 Medium:

> LC 2: Add Two Numbers
> 
> LC 19: Remove Nth Node
> 
> LC 24: Swap Pairs
> 
> LC 86: Partition List
> 
> LC 138: Copy Random List
> 
> LC 143: Reorder List

🔥 Hard:

> LC 25: Reverse Nodes in K-Group
> 
> LC 23: Merge K Sorted Lists
> 
> LC 148: Sort List
> 
> LC 61: Rotate List