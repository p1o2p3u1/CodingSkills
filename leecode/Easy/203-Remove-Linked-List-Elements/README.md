# 	203	Remove Linked List Elements

Remove all elements from a linked list of integers that have value val.

**Example**
**Given:** 
```
1 --> 2 --> 6 --> 3 --> 4 --> 5 --> 6
val = 6
```
**Return:** 
```
1 --> 2 --> 3 --> 4 --> 5
```

# Solution
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
    ListNode* removeElements(ListNode* head, int val) {
        ListNode *tmp = new ListNode(-1);
        tmp -> next = head;
        ListNode *pre = tmp, *p = head;
        while(p){
            if(p -> val == val){
                pre -> next = p -> next;
                delete p;
                p = pre-> next;
            }else{
                pre = p;
                p = p-> next;
            }
        }
        return tmp -> next;
    }
};
```