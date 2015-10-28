## 141	Linked List Cycle	

Given a linked list, determine if it has a cycle in it.

Follow up:
Can you solve it without using extra space?

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
    bool hasCycle(ListNode *head) {
    	if(head == NULL || head -> next == NULL) return false;
    	ListNode *p = head, *q = head -> next -> next;
       	while(q && q -> next){
       		if(p == q) return true;
       		p = p -> next;
       		q = q -> next -> next;
   	    }
   	    return false;
   	}
};

```