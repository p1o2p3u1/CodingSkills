## 237	Delete Node in a Linked List

Write a function to delete a node (except the tail) in a singly linked list, given only access to that node.

Supposed the linked list is 1 -> 2 -> 3 -> 4 and you are given the third node with value 3, the linked list should become 1 -> 2 -> 4 after calling your function.

## Solution

感觉本题有bug
```C++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    void deleteNode(ListNode* node) {
        if(node == NULL) return;
        ListNode *cur = node;
        ListNode *next = cur->next;
        while(next && next -> next){
            node -> val = next -> val;
            node = next;
            next = next -> next;
        }
        node -> val = next -> val;
        node -> next = NULL;
        delete next;
    }
};
```