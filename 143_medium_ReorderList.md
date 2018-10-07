Given a singly linked list L: L0→L1→…→Ln-1→Ln,
reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

You may not modify the values in the list's nodes, only nodes itself may be changed.

Example 1:
	
	Given 1->2->3->4, reorder it to 1->4->2->3.

Example 2:
	
	Given 1->2->3->4->5, reorder it to 1->5->2->4->3.

#注意点：
>1.这道题有一定的难度，需要综合运用快慢指针法求中值，头插法倒序等方法求解。
>
>2.首先使用快慢指针来得到中值指针。
>
>3.根据结点奇偶性判断中值指针是否需要进行运算：若fast为NULL，则说明偶数个结点，中值指针需要运算，否则为奇数个，中值结点不需要运算。记第一个不需要运算的指针为dst。
>
>4.其次通过头插法逆序后半部分链表，使用static加快编译速度。
>
>5.对前半部分链表依次进行后半部分链表的插入，当下一个结点为dst时，则说明结束。
>
>6.最后不要忘记将中值指针的next置为NULL。

	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	static struct ListNode* reverse(struct ListNode *head)
	{
	    struct ListNode *head2 = NULL;
	    struct ListNode *n = head;
	    while (n) {
	        struct ListNode *next = n->next;
	        n->next = head2;
	        head2 = n;
	        n = next;
	    }
	    return head2;
	}
	void reorderList(struct ListNode* head) {
	    if(!head) { return; }
	    struct ListNode *fast = head, *slow = head, *p = head, *q, *dst;
	    while(fast && fast->next) {
	        fast = fast->next->next;
	        slow = slow->next;
	    }
	    dst = fast ? slow->next : slow;
	    q = reverse(dst);
	    while(p->next != dst) {
	        struct ListNode *tmp1 = p->next, *tmp2 = q->next;
	        p->next = q;
	        q->next = tmp1;
	        q = tmp2;
	        p = p->next->next;
	    }
	    slow->next = NULL;
	}