Given a sorted linked list, delete all duplicates such that each element appear only once.

Example 1:
	
	Input: 1->1->2
	Output: 1->2

Example 2:

	Input: 1->1->2->3->3
	Output: 1->2->3

#注意点：
>1.简单的链表删除，注意好边界判断就OK。

	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	struct ListNode* deleteDuplicates(struct ListNode* head) {
	    if(!head || !head->next) { return head; }
	    struct ListNode *p = head, *q = p->next;
	    while(q) {
	        if(p->val == q->val) {
	            p->next = q->next;
	            free(q);
	            q = p->next;
	        } else {
	            p = p->next;
	            q = p->next;
	        }
	    }
	    return head;
	}