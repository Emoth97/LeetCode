Remove all elements from a linked list of integers that have value val.

Example:

	Input:  1->2->6->3->4->5->6, val = 6
	Output: 1->2->3->4->5

#注意点：
>1.现要判断头结点是否为空。
>
>2.若头结点的值为要删除的值，则要删除头结点。
>
>3.头结点和链中结点处理方式不一样。因此可以考虑增设一个头结点，统一操作。


#未增设头结点：
	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	struct ListNode* removeElements(struct ListNode* head, int val) {
	    while(head && head->val == val) { 
	        struct ListNode *p = head;   
	        head = head->next;
	        free(p);
	    }
	    struct ListNode *t = head;
	    while(t) {
	        if(t->next && t->next->val == val){
	            struct ListNode *p = t->next;   
	            t->next = p->next;
	            free(p);
	        } else {         
	            t = t->next;
	        }
	    }
	    return head;
	}

#增设头结点：
	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	struct ListNode* removeElements(struct ListNode* head, int val) {
	    struct ListNode *newhead = (struct ListNode *)malloc(sizeof(struct ListNode)),  *t = newhead;
	    newhead->next = head;
	    while(t->next) {
	        if(t->next->val == val){
	            struct ListNode *p = t->next;   
	            t->next = p->next;
	            free(p);
	        } else {         
	            t = t->next;
	        }
	    }
	    return newhead->next;
	}