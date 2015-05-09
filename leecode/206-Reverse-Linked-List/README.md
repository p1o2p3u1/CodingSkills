# 	206	Reverse Linked List


# Solution
iteration
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
    ListNode* reverseList(ListNode* head) {
        if(head == NULL || head -> next == NULL) return head;
        ListNode *tmp = new ListNode(-1);
        ListNode *p = head, *q = tmp -> next;
        while(p){
            tmp -> next = p;
            p = p -> next;
            tmp -> next -> next = q;
            q = tmp -> next;
        }
        delete tmp;
        return q;
    }
};
```