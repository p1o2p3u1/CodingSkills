## 61	Rotate List

Given a list, rotate the list to the right by k places, where k is non-negative.

For example:
Given `1->2->3->4->5->NULL` and `k = 2`,
return `4->5->1->2->3->NULL`.

## Solution

尾插法
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
    ListNode *rotateRight(ListNode *head, int k) {
        if(head == NULL || head -> next == NULL || k == 0) return head;
        int len = 0;
        ListNode *p = head, *pre, *q;
        while(p){
            ++len;
            pre = p;
            p = p -> next;
        }
        p = head;
        k = k % len;
        k = len - k;
        while(k--){
            q = p -> next;
            pre -> next = p;
            p -> next = NULL;
            pre = p;
            p = q;
        }
        return p;
    }
};
```
