Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:
	
	Input: 1->2->4, 1->3->4
	Output: 1->1->2->3->4->4

#注意点：
>1.C语言使用结构体要加上struct 切记！！！  
>2.参数中的链表为无头结点的链表  
>3.当两个链表中有一个为空时可直接使L指向另一个链表
	
	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	struct ListNode* mergeTwoLists(struct ListNode* l1, struct ListNode* l2) {
	    struct ListNode *head = (struct ListNode *)malloc(sizeof(struct ListNode)), *L = head;
	    while(l1 != NULL && l2 != NULL){
	        L->next = (struct ListNode *)malloc(sizeof(struct ListNode));
	        L = L->next;
	        if(l1->val > l2->val){
	            L->val = l2->val;
	            l2 = l2->next;
	        } else {
	            L->val = l1->val;
	            l1 = l1->next;
	        }
	    }
	    L->next = l1 != NULL ? l1 : l2;
	    return head->next;
	}