Given a singly linked list L: L0→L1→…→Ln-1→Ln,
reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

You may not modify the values in the list's nodes, only nodes itself may be changed.

Example 1:
	
	Given 1->2->3->4, reorder it to 1->4->2->3.

Example 2:
	
	Given 1->2->3->4->5, reorder it to 1->5->2->4->3.

#注意点：
>1.由于题目给出的链表没有头结点，因此可以考虑增设一个头结点，这样可以简便许多边界判断。
>
>2.当遍历到第一个大于等于target的节点时，只需从该点继续向后遍历找到该点之后第一个比target小的节点，然后修改指针使比target小的结点位置放到大于等于target的节点前。（类似于链表的头插法）

	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	struct ListNode* partition(struct ListNode* head, int x) {
	    struct ListNode *newhead = (struct ListNode *)malloc(sizeof(struct ListNode)), *p = newhead, *q;
	    newhead->next = head;
	    while(p->next && p->next->val < x) { p = p->next; }
	    q = p;
	    while(q->next) {
	        while(q->next && q->next->val >= x) { q = q->next; }
	        if(q->next){
	            struct ListNode *tmp = q->next;
	            q->next = tmp->next;
	            tmp->next = p->next;
	            p->next = tmp;
	            p = p->next;
	        }
	    }
	    return newhead->next;
	}

