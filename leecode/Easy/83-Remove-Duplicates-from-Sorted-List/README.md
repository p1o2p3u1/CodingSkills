## 83	Remove Duplicates from Sorted List
Given a sorted linked list, delete all duplicates such that each element appear only once.

For example,
Given `1->1->2`, return `1->2`.
Given `1->1->2->3->3`, return `1->2->3`.

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
    ListNode* deleteDuplicates(ListNode* head) {
    	if(head == NULL || head -> next == NULL) return head;
    	ListNode *pre = head, *p = head -> next, *q;
    	while(p){
    		if(p -> val == pre -> val){
    			q = p -> next;
    			delete p;
    			pre->next = NULL; // 这个地方不能少，否则最后一个节点指向一个被delete掉的空间，会RE
    			p = q;
    		}else{
    			pre -> next = p;
    			pre = p;
    			p = p -> next;
    		}
    	}
    	return head;    
    }
};
```
另一个简便的解法
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
    ListNode *deleteDuplicates(ListNode *head) {
        if(head == NULL || head -> next == NULL) return head;
        ListNode *p = head, *q;
        while(p -> next){
        	q = p -> next;
        	if(p -> val == q -> val){
        		p -> next = q -> next;
        		delete q;
        	}else{
        		p = p -> next;
        	}
    	}
    	return head;
    }
};
```