## 19	Remove Nth Node From End of List

Given a linked list, remove the nth node from the end of list and return its head.

For example,

   Given linked list: `1->2->3->4->5, and n = 2`.

   After removing the second node from the end, the linked list becomes `1->2->3->5`.
Note:
Given n will always be valid.
Try to do this in one pass.

## Solution

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
    ListNode *removeNthFromEnd(ListNode *head, int n) {
        if(n==0 || head == NULL) return head;
        ListNode *pre = new ListNode(-1);
        pre -> next = head;
        ListNode *p = head, *q = pre;
        while(p && n--) p = p -> next;
        if(p == NULL && n > 0) return NULL; // invalid n
        while(p){
        	p = p -> next;
        	q = q -> next;
    	}
    	ListNode *tmp = q -> next; // the node to delete
    	q -> next = tmp -> next;
    	delete tmp;
    	q = pre -> next; // the original head
    	delete pre; // and delete the pre
    	return q;
    }
};
```