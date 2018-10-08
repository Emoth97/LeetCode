Reverse a linked list from position m to n. Do it in one-pass.

Note: 1 ≤ m ≤ n ≤ length of list.

Example:

	Input: 1->2->3->4->5->NULL, m = 2, n = 4
	Output: 1->4->3->2->5->NULL

#注意点：
>1.还是熟悉头插法倒置链表。
>
>2.头插法记得最后释放头结点。
>
>3.这道题与一般的头插法倒置链表不同的地方是只倒置一部分链表。所以还需要一个尾指针指向倒置的末尾，将其与倒置尾部后面的链表连接起来。

	/**
	 * Definition for singly-linked list.
	 * struct ListNode {
	 *     int val;
	 *     struct ListNode *next;
	 * };
	 */
	static struct ListNode* emothReverse(struct ListNode* head, int m){
	    struct ListNode *newhead = (struct ListNode *)malloc(sizeof(struct ListNode)), *tmp, *tail = head;
	    newhead->next = head;
	    head = head->next;
	    while(0 < m--) {
	        tmp = head->next;
	        head->next = newhead->next;
	        newhead->next = head;
	        head = tmp;
	    }
	    tail->next = head;
	    tmp = newhead->next;
	    free(newhead);
	    return tmp;
	}
	struct ListNode* reverseBetween(struct ListNode* head, int m, int n) {
	    struct ListNode *newhead = (struct ListNode *)malloc(sizeof(struct ListNode)), *cur = newhead;
	    newhead->next = head;
	    n -= m;
	    while(0 < --m) { cur = cur->next; }
	    cur->next = emothReverse(cur->next, n);
	    cur = newhead->next;
	    free(newhead);
	    return cur;
	}