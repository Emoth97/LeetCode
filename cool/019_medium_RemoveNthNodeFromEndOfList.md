Given a linked list, remove the n-th node from the end of list and return its head.

Example:
	
	Given linked list: 1->2->3->4->5, and n = 2.
	
	After removing the second node from the end, the linked list becomes 1->2->3->5.

Note:

Given n will always be valid.

Follow up:

Could you do this in one pass?


#注意点：
>1.思路：设置双指针，令快指针首先向后遍历n个位置，然后快慢指针同时遍历，当快指针遍历到结尾时，慢指针即指向倒数第n个位置，只需删除其就OK。
>
>2.为了简单起见，依然增设一个头结点，使用结束时记得释放新增的头结点。

	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	struct ListNode* removeNthFromEnd(struct ListNode* head, int n) {
	    struct ListNode *newhead = (struct ListNode *)malloc(sizeof(struct ListNode)), *fast = newhead, *slow = newhead;
	    newhead->next = head;
	    while(fast && n-- > 0){ fast = fast->next; }
	    while(fast && fast->next) {
	        fast = fast->next;
	        slow = slow->next;
	    }
	    if(slow->next){
	        struct ListNode *tmp = slow->next;
	        slow->next = tmp->next;
	        free(tmp);
	    }
	    head = newhead->next;
	    free(newhead);
	    return head;
	}